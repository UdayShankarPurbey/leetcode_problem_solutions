### 9. Palindrome Number

```ts
function isPalindrome(x: number): boolean {
    if(x<0) return false 
    const arrayofx = x.toString().split('');
    const lenghtOfArrayofX = arrayofx.length;
    for (let i = 0 ; i< lenghtOfArrayofX;i++) {
        const left = arrayofx[i];
        const right = arrayofx[(lenghtOfArrayofX - 1)- i]
        if(left !== right) return false
    }
    return true
};
```

### 1464. Maximum Product of Two Elements in an Array

```ts
function maxProduct(nums: number[]): number {
    const numLength = nums.length;
    const possiblePair = [];
    let max = 0;

    for(let i = 0 ; i<numLength;i++) {
        const num = nums[i]
        for(let j= i+1; j<numLength;j++) {
            possiblePair.push([num , nums[j]])
        }
    }

    for(let pp of possiblePair) {
        const left = pp[0] 
        const right = pp[1]
        const productValue = (left-1)*(right-1)
        if(max<productValue) {
            max = productValue
        }
    }
    return max;
};
```

### 3731. Find Missing Elements

```ts
function findMissingElements(nums: number[]): number[] {
    if(nums.length < 1 ) return [];

    let min = nums[0];
    let max = 0;
    const elementPresenSet = new Set();
    const missingNumber = [];

    for(let i = 0 ;i < nums.length; i++) {
        const num = nums[i];
        elementPresenSet.add(num)
        if(max < num ) max = num;
        if(num < min) min = num
    }
    
    for(let i = min; i < max; i++ ) {
        if(!elementPresenSet.has(i)) {
            missingNumber.push(i)
        }
    }
    return missingNumber
    
};
```

### 58. Length of Last Word

```ts
function lengthOfLastWord(s: string): number {
    const words = s.replace(/\s+/g , " ").split(' ');
    console.log(words);
    const lastWord = words[words.length - 1] ? words[words.length - 1] : words[words.length - 2];
    return lastWord.length;
    
};
```

### 263. Ugly Number

```ts
function isUgly(n: number): boolean {
    if(n <1) return false;
    let num = n;
    while(num >= 2) {
        if(num%2 === 0) num /= 2;
        else if(num%3 === 0) num /= 3;
        else if(num%5 === 0) num /= 5;
        else return false;
    }
    return true;
    
};
```

### 509. Fibonacci Number

```ts
function fib(n: number): number {
    if(n===0) return 0;
    if(n===1) return 1;
    return fib(n -1) + fib(n-2);
};
```