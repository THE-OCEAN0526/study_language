## switch 述句

```
switch (整數值) {
  case 整數常數:
  程式片段;
  break;
  default:
  程式片段;
}
```
- 可以指定多個不同的 case
- break 結束 switch
- 可以設定 default ，在所有 case 都不符合時執行
### 四則運算
```
#intclud <stdio.h>
int main() {
  int unm1, num2;
  char op;
  float answer;
  scanf("%d%c%d", &num1, &op, &num2);
  switch (op) {
    case '+':
      answer = num1 + num2;
      break;
    case '-':
      answer = num1 - num2;
      break;
    case '*':
      answer = num1 * num2;
      break;
    case '/':
      answer = (float) num1 / num2;
      break;
  }
  printf("ANS : %f\n", answer);
  return 0;
}
```
