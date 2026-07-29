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

### 1732. Find the Highest Altitude

```ts
function largestAltitude(gain: number[]): number {
    let highestAltitude = 0;
    let baseAltitude = 0;


    for(let g of gain) {
        baseAltitude += g
        if(highestAltitude < baseAltitude) highestAltitude = baseAltitude
    }

    return highestAltitude
    
};
```

### 3432. Count Partitions with Even Sum Difference

```ts
function countPartitions(nums: number[]): number {
    let sumOfLeft = 0;
    let sumOfRight = nums.reduce((a : number,b : number) => a+b , 0);
    let countOfEvenPartion = 0;

    for(let i = 0; i< (nums.length - 1) ; i++) {
        const num = nums[i];
        sumOfLeft += num;
        sumOfRight -= num;
        if((sumOfLeft - sumOfRight) % 2 === 0 ) countOfEvenPartion++;
    }
    return countOfEvenPartion
};
```

### 3028. Ant on the Boundary

```ts
function returnToBoundaryCount(nums: number[]): number {
    let numberOfCountAntAtBoundary = 0;
    let positionOfAnt = 0 ;
    for(let num of nums) {
        positionOfAnt+= num;
        if(positionOfAnt === 0) numberOfCountAntAtBoundary++;
    }

    return numberOfCountAntAtBoundary;
};
```

### 1310. XOR Queries of a Subarray

```ts
function xorQueries(arr: number[], queries: number[][]): number[] {
    const queryResponse = [];
   
    const xorOutput : number[] = [0];
    let answer = 0;

    for(let i = 0 ; i< arr.length ; i++) {
        const num = arr[i];
        xorOutput[i+ 1] = xorOutput[i] ^ num
    }

    for(let [left , right] of queries) {
        
       if(left === 0){
            answer = xorOutput[right + 1]
       } else {
          answer = xorOutput[right + 1] ^ xorOutput[left]
       }
       queryResponse.push(answer);
       answer = 0;

        
    }

    
    return queryResponse
};
```

### 2574. Left and Right Sum Differences\

```ts
function leftRightDifference(nums: number[]): number[] {
    const numsLength : number = nums.length;
    const leftSum : number[] = new Array(numsLength).fill(0);
    const rightSum : number[] = new Array(numsLength).fill(0);
    const differenceArray : number[] = [];

    for(let i = 1 ; i< numsLength; i++) {
        const num = nums[i - 1];
        leftSum[i] = leftSum[i-1] + num;
    }

    for(let i = (numsLength -1 ) ; i > 0; i--) {
        const num = nums[i];
        rightSum[i -1] = rightSum[i] + num;
    }

    for(let i = 0 ; i<numsLength ; i++ ) {
        const left = leftSum[i];
        const right = rightSum[i]
        const ans = Math.abs(left - right)
        differenceArray.push(ans)
    }

    return differenceArray
};
```

### 2485. Find the Pivot Integer

```ts
function pivotInteger(n: number): number {
    const sumofNFromLeft = new Array(n+1).fill(0);
    const sumofNFromRight = new Array(n+1).fill(0);

    for(let i = 1 ; i<= n ; i++) {
        sumofNFromLeft[i] = sumofNFromLeft[i-1] + i 
    }

    for(let i = n ; i> 0; i--) {
        sumofNFromRight[ i - 1] = sumofNFromRight[i] + i
    }

    for(let i = 0 ; i<(n+1); i++) {
        if(sumofNFromLeft[i+1] === sumofNFromRight[i]) return (i + 1)
    }

    return -1;
};
```

### 1991. Find the Middle Index in Array

```js
function findMiddleIndex(nums: number[]): number {
    const numLength =  nums.length;
    const sumFromLeft = new Array(numLength + 1).fill(0);
    const sumFromRight = new Array(numLength + 1).fill(0);


    for(let i = 0 ; i< numLength ; i++) {
        const num = nums[i]
        sumFromLeft[i+1] = sumFromLeft[i] + num;
    }

    for(let i = (numLength)  ; i > 0 ; i--) {
        const num = nums[i -1 ]
        sumFromRight[i -1] = sumFromRight[i] + num;
    }

    for(let i = 0 ; i< numLength ; i++) {
        if(sumFromLeft[i+1] == sumFromRight[i]) return i
    }

    return -1
};
```

### 3427. Sum of Variable Length Subarrays

```js
function subarraySum(nums: number[]): number {
    const sum = new Array(nums.length + 1).fill(0);

    for(let i = 0 ; i<nums.length; i++) {
        const num = nums[i];
        sum[i+1] = sum[i] + num
    }

    let totalSum = 0;

    for(let i = 0 ; i<nums.length; i++) {
        const start = Math.max(0, i - nums[i]);
        totalSum += sum[i + 1] -  sum[start];
    }

    return totalSum;
};
```