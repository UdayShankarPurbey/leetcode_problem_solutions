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