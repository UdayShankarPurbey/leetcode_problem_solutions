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

```ts
function maxProduct(nums: number[]): number { 
    if(nums.length<2) return 0;
    nums.sort((a : number , b: number) => b - a);
    return (nums[0] - 1) * (nums[1] -1);
}
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

### 344. Reverse String

```ts
function reverseString(s: string[]): void {
    if(s.length < 1) return ;
    let left = 0 ; 
    let right = s.length -1;
    
   while(left < right) {
        const val =  s[left];
        s[left] = s[right];
        s[right] = val
        left++;
        right --;
   }
};
```

### 3760. Maximum Substrings With Distinct Start

```ts
function maxDistinct(s: string): number {
    return new Set(s.split('')).size
};
```

### 3069. Distribute Elements Into Two Arrays I

```ts
function resultArray(nums: number[]): number[] {
    const arr1 = [];
    const arr2 = [];
    for(let i = 0; i<nums.length; i++) {
        const num = nums[i];
        let arr1LastNum = arr1[arr1.length - 1]
        let arr2LastNum = arr2[arr2.length - 1]
        if(arr1LastNum === undefined) {
            arr1.push(num);
            continue;
        }

        if(arr2LastNum === undefined) {
            arr2.push(num);
            continue;
        }

        if(arr1LastNum > arr2LastNum) arr1.push(num);
        else arr2.push(num);
    }

    return [...arr1 , ...arr2]
};
```

### 3718. Smallest Missing Multiple of K

```ts
function missingMultiple(nums: number[], k: number): number {
    const number = new Set(nums);
    for(let i= 1 ; i<=nums.length;i++) {
        const reqNum = k*i;
        if(!number.has(reqNum)) return reqNum;
    }
    return k * (nums.length + 1)
};
```

### 258. Add Digits

```ts
function addDigits(num: number): number {
    if(num<10) return num;
    return addDigits(num.toString().split('').reduce((a,b) => Number(a)+Number(b) , 0))
};
```



### 48. Rotate Image

```ts
function rotate(matrix: number[][]): void {
    const rotatedMatrix = [];

    for (let i = 0; i < matrix.length; i++) {
        const row = [];
        for (let j = 0; j < matrix.length; j++) {
            row.push(matrix[j][i])
        }
        rotatedMatrix.push(row.reverse())
    }

    for (let i = 0; i < matrix.length; i++) {
        for (let j = 0; j < matrix.length; j++) {
            matrix[i][j] = rotatedMatrix[i][j]
        }
    }
};
```

### 383. Ransom Note

```ts
function canConstruct(ransomNote: string, magazine: string): boolean {
    const magazineCharCount = new Map();

    for(let i = 0 ; i< magazine.length; i++) {
        if(magazineCharCount.has(magazine[i])) {
            magazineCharCount.set(magazine[i] , magazineCharCount.get(magazine[i]) + 1);
        } else {
            magazineCharCount.set(magazine[i] , 1)
        }
    }

    for(let i = 0 ; i< ransomNote.length; i++) {
        if(magazineCharCount.has(ransomNote[i]) && magazineCharCount.get(ransomNote[i]) > 0 ) {
            magazineCharCount.set(ransomNote[i] , magazineCharCount.get(ransomNote[i]) - 1);
        }else {
            return false;
        }

    }
    return true;
};
```