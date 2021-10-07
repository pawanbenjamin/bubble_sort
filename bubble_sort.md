### Basic Sorting Algorithms

## 1. Bubble Sort

Not that efficient. Not commonly used, but it has a fun name!

We have an array and we are sorting in ascending order, from smallest to greatest. The larger values will end up bubbling to the top, one at a time.

#Example

```
    bubbleSort([6,4,7,1,2])  // returns ==> [1,2,4,6,7]
    bubbleSort([44,33,22,11]) // returns ==> [11,22,33,44]
```

Walk through the conceptual idea. We compare each adjacent number in an array, and move the one who's value is larger to the right, until the last element ends up being the larget. We then iterate over the entire array again, this time, ending one index earlier (because we already determined this was the largest value with our first pass through the array

# Things to Keep in Mind

Do we need nested loops? How do we switch around the numbers?

# The Swap Function

There are two possible ways to do it:

```
function swap(arr, idx1, idx2){
    let temp = arr[idx1]
    arr[idx1] = arr[idx2]
    arr[idx2] = temp
}
```

or Es6 deconstructed:

```
const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]]
}
```

## Full Solution

```
// Less Optimal Solution

function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      if (arr[j] > arr[j + 1]) {
        swap(arr, i, j);
      }
    }
  }
  return arr;
}

// Helper Function
function swap(arr, idx1, idx2) {
  let temp = arr[idx1];
  arr[idx1] = arr[idx2];
  arr[idx2] = temp;
}
```

## Can it be more Optimal??

Since we already know that the last value is sorted, we can make the length of the outer loop, one less every time. So the outer loop will decriment on each pass, and the inner loop will always go until one index less that the outer loop's index.

```
// More Optimal Solution

const bubbleSort = (arr) => {

    // i will start at the end and go backwards
  for (let i = arr.length; i > 0; i--) {

    // j will now loop forward until the element before i
    for (let j = 0; j < i-1; j++) {

        //this will compare left and right values
      if (arr[j] > arr[j + 1]) {

          // SWAP!
        swap(arr, i, j);
      }
    }
  }
  return arr;
};

// Helper Function
const swap = (arr, idx1, idx2) => {
  [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
};
```

## But wait there's more!

What if the array is almost completely sorted? Well, we can check if the over the last pass, we didn't swap anything. If we went through all the elements and didn't swap anything, we're done! No need to continue to loop through the array. The swappage is over. The war is won.

```

// With variable that holds wether or not we have any swaps on the last pass

function bubbleSort(arr){
    let noSwaps;
    for(let i=arr.length; i>0; i--){
        noSwaps = true;
        for(let j=0; j< i-1; j++){
            if(arr[j]>arr[j+1]){
                swap(arr, i, j)
                noSwaps = false
            }
        }
        if(noSwaps) break;
    }
    return arr
}

// Helper Function
function swap(arr, idx1, idx2) {
  let temp = arr[idx1];
  arr[idx1] = arr[idx2];
  arr[idx2] = temp;
}

```
