# The Basic Algorithm

[link](https://www.youtube.com/watch?v=_zbGhovjYhs)

- if the symbol has not occurred in the context
  1. an **escape symbol** is encoded
  2. attempts to use the next **smaller context**
  3. each time a symbol is encountered, the count corresponding to that symbol is updated (in all  tables)



# Example

encode the sequence: 

![image-20200111094516474](ppm.assets/image-20200111094516474.png)

## assumption

1. we already encode some initial seven symbols "this /bis” 
2. assume the most high order context is 2
3. assume that the word length for arithmetic coding is 6, 所以 
   - l (lower bound) = 000 000B
   - u (upper bound) = 111 111B = 63
4. 

## order tables

### -1 order context

- cum_count: cumulative count
- 一个个字母看, 之前数过的就跳过
- 因为 /b 不是字母, 所以把它放最后

![image-20200111095628343](ppm.assets/image-20200111095628343.png)

- encode context

  <img src="ppm.assets/image-20200111095828244.png" alt="image-20200111095828244" style="zoom:50%;" />

### 0 order context

- 看总的context有多少个这样的字母

![image-20200111095708415](ppm.assets/image-20200111095708415.png)

### 1 order context

<img src="ppm.assets/image-20200111100855455.png" alt="image-20200111100855455" style="zoom: 67%;" />

![image-20200111100959124](ppm.assets/image-20200111100959124.png)

### 2 order context

<img src="ppm.assets/image-20200111101346030.png" alt="image-20200111101346030" style="zoom: 33%;" />

- formula for calculate the lower order limit and upper order limit

  u公式最后是 -1
  
  ![image-20200111101556453](ppm.assets/image-20200111101556453.png)

## further encode

![image-20200112171634932](ppm.assets/image-20200112171634932.png)

1. next letter is /b, 2 order context is "is”

   check the 2 order table 

   ![image-20200112171923288](ppm.assets/image-20200112171923288.png)

   cum-count = 1, TC (total count) = 2

- then use two formulas to calculate the next lower and upper order limit

- $l^0 = 000 000B, u^0 = 111 111B = 63$

- $cum-count(x_n-1) = 1-1=0?$

- update value of $l$ and $u$

  - $l$![image-20200112173001688](ppm.assets/image-20200112173001688.png)
  - $u$![image-20200112173048999](ppm.assets/image-20200112173048999.png)

- MSB (the Most Significant Bit 二进制的第一位?) of $l$ and $u$ is $0$, so we send the $0$ and update $l$ and $u$ by shifting left

  $l=000000B, u=111111B?$

- need to update all tables for that particular letter

  - 2 order table

    ![image-20200112191833067](ppm.assets/image-20200112191833067.png)

  - 1 order table

    ![image-20200112191925056](ppm.assets/image-20200112191925056.png)

  - 0 order table

    ![image-20200112192003059](ppm.assets/image-20200112192003059.png)