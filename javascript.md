### 1189. Maximum Number of Balloons
```js
/**
 * @param {string} text
 * @return {number}
 */
var maxNumberOfBalloons = function(text) {
    const desiredWord = 'balloon';
    const textWordCount = distinctWordCount(text);
    const desiredWordCount = distinctWordCount(desiredWord);
    const formedWord = {}

    for (let i in desiredWordCount) {
        if(Object.keys(textWordCount).indexOf(i) == -1) {
            return 0;
        } else {
            formedWord[i] = Math.floor(textWordCount[i] /desiredWordCount[i])
        }
    }
    return Math.min(...Object.values(formedWord));
};

function distinctWordCount(word) {
    const countWord = {};
    for (i = 0; i < word.length; i++) {
        const char = word[i];
        if (Object.keys(countWord).indexOf(char) != -1) {
            countWord[char] += 1;
        } else {
            countWord[char] = 1;
        }
    }
    return countWord
}
```

### 1. Two Sum

```js
 var twoSum = function(nums, target) {
    let first_val = null
    let second_val = null;
    const remainder_num = {};

    for(let i = 0 ; i< nums.length ; i++) {
         if(remainder_num[nums[i]] !== undefined){
           first_val = remainder_num[nums[i]];
           second_val = i
           break;
         }
        const rem = target - nums[i];


        if(remainder_num[rem] === undefined) {
            remainder_num[rem] = i
        }
    }
    return first_val !== null && second_val !== null ? [first_val,second_val] : []
    
};
```