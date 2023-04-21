

<template>
  <header>
  </header>
  <main>
    <Q1 v-show="selectedQuestionNo == 1" :answer-function="answerFunction_Q1" @go-to-next="goToNext" />
    <Q2 v-show="selectedQuestionNo == 2" :answer-function="answerFunction_Q2" @go-to-next="goToNext" />
    <Q3 v-show="selectedQuestionNo == 3" :answer-function="answerFunction_Q3" @go-to-next="goToNext" />
    <Q4 v-show="selectedQuestionNo == 4" :answer-function="answerFunction_Q4" @go-to-next="goToNext" />
    <Q5 v-show="selectedQuestionNo == 5" :answer-function="answerFunction_Q5" @go-to-next="goToNext" />
  </main>
</template>

<script setup lang="ts">

import { reactive, ref, computed, onMounted, watch } from 'vue'
import Q1 from '@/components/question/Q1.vue';
import Q2 from '@/components/question/Q2.vue';
import Q3 from '@/components/question/Q3.vue';
import Q4 from '@/components/question/Q4.vue';
import Q5 from '@/components/question/Q5.vue';

const selectedQuestionNo = ref<number>(1);

function answerFunction_Q1(inputArray: Array<string>) {
  let name = inputArray[1];
  let age = inputArray[0];
  
  //第一題請填這裡

  return ``;
}

function answerFunction_Q2(inputArray: Array<string>) {
  let endNumber: number = +inputArray[0];
  
  //第二題請填這裡

  return ``;
}

function answerFunction_Q3(inputArray: Array<string>) {
  let endNumber: number = +inputArray[0];
  
  //第三題請填這裡
  
  return ``;
}

function answerFunction_Q4(inputArray: Array<string>) {
  let friendHands: string = inputArray[0];

  //第四題請填這裡
  
  return ``;
}

function answerFunction_Q5(inputArray: Array<string>) {
  let validData: Array<string> = [];
  //把input的陣列確認是否為可以比大小的數字，只留下可以比大小的數字
  for (var i: number = 0; i < inputArray.length; i++) {
    let convertedData = _convertToValidData(inputArray[i]);
    if (convertedData) {
      validData.push(convertedData);
    }
  }
  // 請把validData資料做排序
  validData.sort(function (a, b) {
    let realA: number = _toRealNumber(a);
    let realB: number = _toRealNumber(b);

    //第五題請填這裡

    //提示：當a>b 回傳值＝1 ，a<b時，回傳值＝-1 
    return 1;
  });
  return validData.join(',')
}

/** Q5 使用
 * 是否為中文數字 */
function _isTextNumber(c: string) {
  return '零一二三四五六七八九'.includes(c);
}

/** Q5 使用
 *  是否為數字 */
function _isPureNumber(c: string) {
  return '0123456789'.includes(c);
}

/** Q5 使用
 *  轉換成沒有 0或零開頭的阿拉伯數字或中文數字，異常資料會回傳空字串
 */
function _convertToValidData(rawData: string) {
  let isPure = false; // 偵測是否為純數字
  let isText = false; // 偵測是否為文字數字
  let isHeadingZero = true; // 偵測最前面的0或零
  let result = '';
  for (var i: number = 0; i < rawData.length; i++) {
    if (_isPureNumber(rawData[i])) {
      if (isText) {
        return '';
      }
      isPure = true;
      if (rawData[i] != '0') {
        isHeadingZero = false;
      } else if (isHeadingZero) {
        continue;
      }
      result += rawData[i];
    } else if (_isTextNumber(rawData[i])) {
      if (isPure) {
        return '';
      }
      isText = true;
      if (rawData[i] != '零') {
        isHeadingZero = false;
      } else if (isHeadingZero) {
        continue;
      }
      result += rawData[i];
    } else {
      return '';
    }
  }
  if (!result) {
    return isText ? '零' : '0';
  }
  return result;
}

/** Q5 使用 */
function _toRealNumber(convertedData: string) {
  let pureNumber = '';
  if (_isTextNumber(convertedData[0])) {
    for (var i: number = 0; i < convertedData.length; i++) {
      pureNumber += '0123456789'['零一二三四五六七八九'.indexOf(convertedData[i])];
    }
  } else {
    pureNumber = convertedData;
  }
  return +pureNumber;
}

function goToNext() {
  if (selectedQuestionNo.value >= 5) {
    selectedQuestionNo.value = 1;
  } else {
    selectedQuestionNo.value++;
  }
}
</script>

<style scoped></style>
