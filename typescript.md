### 1. Two Sum

```ts
function twoSum(nums: number[], target: number): number[] {
    const remainder = new Map();

    for(let i = 0 ; i<nums.length;i++) {
        const cur = nums[i];
        const rem = target - cur;
        const s = remainder.get(cur)
        if(s != undefined) {
            return [i ,s];
        }
        remainder.set(rem , i)
    }
};
```

### 136. Single Number

```ts
function singleNumber(nums: number[]): number {
    let newNum : number | undefined ;
    nums.forEach((x : number) => newNum =x^newNum)
    return newNum == undefined ? 0 : Number(newNum)
};
```

### 191. Number of 1 Bits

```ts
function hammingWeight(n: number): number {
    return n.toString(2)?.replaceAll('0','')?.length
};
```

### 20. Valid Parentheses

```ts
function isValid(s: string): boolean {
    const bracketArray = [];

    for(let val of s) {
        if(val == '(' || val == '{' || val == '[') {
            bracketArray.push(val)
        } else {
            const match = bracketArray[bracketArray.length - 1] 
            
            switch (val) {
                case ')':
                    if (match !== '(') return false;
                    bracketArray.pop();
                    break;

                case '}':
                    if (match !== '{') return false;
                    bracketArray.pop();
                    break;

                case ']':
                    if (match !== '[') return false;
                    bracketArray.pop();
                    break;
            }
        }
    }
    return bracketArray.length == 0 ? true : false;
};
```

### 202. Happy Number

```ts
function isHappy(n: number): boolean {
    return numSquareSumAsNewNum(n , new Set<number>());
};

function numSquareSumAsNewNum(n : number , numberSet : Set<number>) : boolean{
    const nvalue = n.toString()
    let newValue = 0;
    for(let val of nvalue) {
        newValue += Number(val) * Number(val)
    }
        console.log(newValue , newValue === 1 ,numberSet)

    if(numberSet.has(newValue)) return false;
    if(newValue === 1) return true;

    numberSet.add(newValue);

    return numSquareSumAsNewNum(newValue , numberSet)
}
```

### 190. Reverse Bits

```ts
function reverseBits(n: number): number {
    const binaryBit = (n >>> 0).toString(2).padStart(32, '0');
    const reveserBinaryBit = binaryBit.split('').reverse().join('');
    return parseInt(reveserBinaryBit , 2) || 0;
};
```

### 217. Contains Duplicate

```ts
function containsDuplicate(nums: number[]): boolean {
    const numMap = new Set();
    for(let num of nums) {
        if(!numMap.has(num)) {
            numMap.add(num)
        } else {
            return true;
        }
    }
    return false;
};
```

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

### 70. Climbing Stairs

```ts
function climbStairs(n: number): number {
    const climbStairMap = new Map();
    for(let i = 0 ; i<= n ; i++) {
        if(i == 0 || i == 1){
            climbStairMap.set(i,1)
        } else {
            climbStairMap.set(i , (climbStairMap.get((i- 2)) + climbStairMap.get((i- 1))))
        }
    }
    return n >= 2?(climbStairMap.get((n- 2)) + climbStairMap.get((n- 1))) : 1
};
```

### 66. Plus One

```ts
function plusOne(digits: number[]): number[] {
    let numberString = '';
    const numberArray = [];
    for(let num of digits) {
        numberString += num
    }
    const number : string =( BigInt(numberString) + BigInt(1) ).toString();
    for(let n of number) {
        numberArray.push(Number(n))
    }
    return numberArray
};
```

### 268. Missing Number

```ts
function missingNumber(nums: number[]): number {
    const numSet = new Set(nums)
    for(let i = 0; i<=nums.length ; i++) {
        if(!numSet.has(i)) return i
    }
};
```