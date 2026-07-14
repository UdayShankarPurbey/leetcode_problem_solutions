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

### 1588. Sum of All Odd Length Subarrays

```ts
function sumOddLengthSubarrays(arr: number[]): number {
    const arrayLength = arr.length;
    const sumofArray= new Array(arrayLength + 1).fill(0)
    let sum = 0;

    for(let i = 0; i< arrayLength; i++) {
        sumofArray[i+1] = sumofArray[i] + arr[i]
    }

    for(let i =1 ; i<= arrayLength ; i+=2 ) {
        for(let j= 0; j<= arrayLength; j++) {
            const left = j
            const right = j + (i -1 );
            if(right > (arrayLength -1 )) continue;

            sum += sumofArray[right + 1] - sumofArray[left]
            
        }
    }

    return sum;
    
};
```