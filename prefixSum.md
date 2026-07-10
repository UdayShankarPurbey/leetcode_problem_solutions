### 1480. Running Sum of 1d Array

```ts
function runningSum(nums: number[]): number[] {
    const sumofArray = [];
    let previousSum = 0;
    for (let i = 0 ; i< nums.length ; i++) {
        const num = nums[i];
        previousSum += num;
        sumofArray[i] = previousSum
    }
    return sumofArray
};
```