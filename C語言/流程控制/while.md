## while 述句
- while (表示式) {程式片段}
- 當「表示式」成立時，就執行「程式片段」。
```
#include <stdio.h>
int main() {
  int count = 0;
  while(count < 10) {
    count = count + 1;
    printf("%d\n", count);
  }
  return 0;
}
```
