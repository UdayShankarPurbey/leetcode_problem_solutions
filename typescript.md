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
