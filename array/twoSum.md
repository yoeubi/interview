# [two sum](https://leetcode.com/problems/two-sum/)

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

## 브루트포스

배열을 2번 반복하여 모든 조합을 확인

시간 복잡도 O(n^2)

```js
var twoSum = function (nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }
};
```

## 탐색

모든 조합을 비교하지 않음

타켓에서 첫 번째 값을 뺀 값이 존재하는지 탐색

시간복잡도 O(n^2)

```js
var twoSum = function (nums, target) {
  for (let i = 0; i < nums.length; i++) {
    const component = target - nums[i];
    const index = nums.slice(i + 1).indexOf(component);
    if (index !== -1) {
      return [i, index + i + 1];
    }
  }
};
```

## 뺀 수를 키 조회

시간 복잡도 O(n)

```js
var twoSum = function (nums, target) {
  const map = {};
  for (let i = 0; i < nums.length; i++) {
    map[nums[i]] = i;
  }
  for (let i = 0; i < nums.length; i++) {
    const rest = target - nums[i];
    if (map[rest] && i !== map[rest]) {
      return [i, map[rest]];
    }
  }
};
```

## 조회 최적화

```js
var twoSum = function (nums, target) {
  const map = {};
  for (let i = 0; i < nums.length; i++) {
    const rest = target - nums[i];
    if (map[rest]) {
      return [map[rest], i];
    }
    map[nums[i]] = i;
  }
};
```

## 투 포인터

```js
var twoSum = function (nums, target) {
  let left = 0;
  let right = nums.length - 1;
  while (left !== right) {
    if (nums[left] + nums[right] < target) {
      left += 1;
    } else if (nums[left] + nums[right] > target) {
      right -= 1;
    } else {
      return [left, right];
    }
  }
};
```
