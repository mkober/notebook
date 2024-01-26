#+TITLE: C++ Snippets

#+NAME: Convert Decimal Number to Binary
#+BEGIN_SRC cpp
int binary = 0, decimal = 53;
int remainder, product = 1;
while (decimal != 0) {
    remainder = decimal % 2;
    binary += remainder * product;
    decimal = decimal / 2;
    product *= 10;
}
#+END_SRC

#+NAME: Find out if the Given Number is a Palindrome
#+BEGIN_SRC cpp
int number = 2002;
int remainder = 0, reverse = 0;
int temp = number;
while (temp != 0) {
    remainder = temp % 10;
    reverse = reverse * 10 + remainder;
    temp = temp / 10;
}
if (reverse == number) {
    cout << "is palindrome";
}
else {
    cout << "not a palindrome";
}
#+END_SRC

#+NAME: Lambda Functions
#+BEGIN_SRC cpp
#include <functional>
std::function<int(int)> makeLambda(int a){
    return [a](int b){ return a + b; };
}
int addFunc(int a, int b){ return a + b; }
int main(){
    auto add5 = makeLambda(5);
    auto add10 = makeLambda(10);
    add5(10) == add10(5);

    auto addObj = [](int a, int b){ return a + b; };
    addObj(3, 4) == addFunc(3, 4);
}
#+END_SRC

#+NAME: Power of a Number Recursively
#+BEGIN_SRC cpp
int power (int base , int exponent ) {
    if (exponent == 0) {
        return 1;
    }
    return base * power(base, exponent - 1);
}
#+END_SRC

#+NAME: Count Number of Digits Recursively
#+BEGIN_SRC cpp
int count_digits(int number) {
  if (number == 0) {
    return 0;
  }
  return 1 + count_digits(number / 10);
}
#+END_SRC

#+NAME: Find Fibonacci Number Recursively
#+BEGIN_SRC cpp
int fibonacci(int n) {
  if (n == 0) {
    return 0;
  }
  else if (n == 1) {
    return 1;
  }
  return fibonacci(n - 1) + fibonacci(n - 2);
}
#+END_SRC

#+NAME: Sort Array by Decending Order
#+BEGIN_SRC cpp
void sort_elements(int arr[], int size) {
  for (int i=0; i < size; i++) {
    for (int j= i + 1; j < size; j++) {
      if (arr[i] < arr[j]) {
        int temp = arr[j];
        arr[j] = arr[i];
        arr[i] = temp;
      }
    }
  }
}
#+END_SRC

#+NAME: Multiply Two Matrices
#+BEGIN_SRC cpp
void multiplication(int arr1[][2], int row1, int col1, int arr2[][2], int row2, int col2 , int result[][2]) {
  if (col1 == row2) {
    for (int x=0; x < row1; x++) {
      for (int y=0; y < col2; y++) {
        result[x][y] = 0;
        for (int z=0; z < col1; z++) {
          result[x][y] += arr1[x][z] * arr2[z][y];
        }
      }
    }
  }
  else {
    for (int x = 0; x < row1; x++) {
      for (int y = 0; y < col2; y++) {
        result[x][y] = -1;
      }
    }
  }
}
#+END_SRC

#+NAME: Calculate standard deviation
#+BEGIN_SRC cpp
float stdDev = 0;
for(int i = 0 ; i < size; i++){
    stdDev += pow(Array[i] - mean, 2);
}
stdDev = sqrt(stdDev / size);
#+END_SRC
