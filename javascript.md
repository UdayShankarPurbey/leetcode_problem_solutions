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

