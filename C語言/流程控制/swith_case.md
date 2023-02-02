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
## break 述句
- 中斷目前所屬的重複執行述句
-![image](https://user-images.githubusercontent.com/122972916/216249173-1e2f551c-4ab4-41be-ac88-3f432b4d6669.png)

## continue 述句
- 在重複執行述句中跳過後面的程式區塊
![image](https://user-images.githubusercontent.com/122972916/216249454-518edabe-423e-4a92-8934-f3806f9e7adc.png)

### 四則運算
```
#include <stdio.h>
int main() {
  int num1, num2;
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
  printf("ANS : %.1f\n", answer);
  return 0;
}
```
### ID查詢
```
#include <stdio.h>
int main(){
    int id;
    printf("ID: ");
    scanf("%d", &id);
    switch (id){
        case 2:
        case 3:
        case 4:
            printf("John\n");
            break;
        case 13:
            printf("Mary\n");
            break;
        case 16:
            printf("Amy\n");
            break;
        default:
            printf("Not found\n");
    }
    return 0;
}
```
- 可以讓不同的 case 共用同一段程式碼
