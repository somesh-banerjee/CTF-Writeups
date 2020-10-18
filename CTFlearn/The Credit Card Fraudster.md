[**Problem**](https://ctflearn.com/challenge/970) (Easy,Programming)

We have to find the number which satisfies the following conditions:
- divisible by 123457
- satisfy [luhn algorithm](https://www.youtube.com/watch?v=PNXXqzU4YnM)
- similar to 543210******1234

Just run a loop from 1 to 999999 in place of ****** and check for which number it satisfies all three conditions.

Try to do it by yourself

My code:
```
#include <iostream>

using namespace std;

bool luhn(long long n){
  int nSum = 0, isSecond = false;
  while (n>0) {
    int d=n%10;
    if (isSecond == true)
      d = d * 2;
    nSum += d / 10;
    nSum += d % 10;
    isSecond = !isSecond;
    n=n/10;
  }
  return (nSum % 10 == 0);
}

int main(int argc, char const *argv[]) {
  long long p,s,n,i=0;
  p=543210;
  s=1234;
  while(i<=999999){
    n=p*10000000000 + i*10000 + s;
    if(n%123457 == 0){
      if(luhn(n))
        cout<<n<<endl;
    }
    i++;
  }
  return 0;
}

```
