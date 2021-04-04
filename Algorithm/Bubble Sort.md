### :game_die: Bubble Sort 
##### 두 인접한 데이터를 비교해서, 앞에 있는 데이터가 뒤에 있는 데이터보다 크면, 자기를 바꾸는 정렬 알고리즘
* ###### 참고 : [Bubble Sort 눈으로 이해하기](https://visualgo.net/en/sorting)

<br>

#### :triangular_flag_on_post: 이해하기 
     ex) data_list = [1,9,5,2]
##### 1.  1차 로직 적용
  - ##### 1 와 9 비교, 자리바꿈없음 [1, 9, 5, 2]
  - ##### 9 와 5 비교, 자리바꿈 [1, 5, 9, 2]
  - ##### 9 와 2 비교, 자리바꿈 [1, 5, 2, 9]
##### 2.  2차 로직 적용
  - ##### 1 와 5 비교, 자리바꿈없음 [1, 5, 2, 9]
  -  ##### 5 과 2 비교, 자리바꿈 [1, 2, 5, 9]
  -  ##### 5 와 9 비교, 자리바꿈없음 [1, 2, 5, 9]
##### 2.  3차 로직 적용
  - ##### 1 과 2 비교, 자리바꿈없음 [1, 2, 5, 9]
  - ##### 2 과 5 비교, 자리바꿈없음 [1, 2, 5, 9]
  - ##### 5 과 9 비교, 자리바꿈없음 [1, 2, 5, 9]

<br>

#### :triangular_flag_on_post: 알고리즘 특이점 찾아보기
* ##### n개의 리스트가 있는 경우, 최대 n-1번의 로직을 적용한다.
* ##### 로직을 1번 적용할 때 마다 가장 큰 숫자가 뒤에서부터 1개씩 결정된다.
* ##### 로직이 경우에 따라 일찍 끝날 수도 있다. 따라서 로직을 적용할 때 한번도 데이터가 교환된 적이 없다면 이미 정렬된 상태이미로 더 이상 로직을 반복 적용할 필요가 없다. 


<br>

#### 💻 직접 해보기.java
```java
public class Question1 {

	public static void main(String[] args) {
		Scanner sInput = new Scanner(System.in);
		int[] inputInt = new int[5];
		
		for(int i=0; i<inputInt.length; i++) {
			System.out.print((i+1)+"번째 정수를 입력: ");
			inputInt[i] = sInput.nextInt();
		}
		
	//Bubble Sort
		for (int i = 0; i < inputInt.length; i++) {
            for (int j = 0; j < inputInt.length-1; j++) { //맨 끝은 제일 큰수가 자리하므로 -1
                if (inputInt[j]> inputInt[j+1]) { //비교 후 작은 수를 
                    int bubbleSort = inputInt[j]; // 변수에 담고
                    inputInt[j] = inputInt[j+1]; //그 다음 수를 넣기 
                    inputInt[j+1] = bubbleSort;
                }
            }
           
        }
		
		System.out.print("정렬된 결과: ");
		for(int bSortInt : inputInt) {
			System.out.print(bSortInt+" ");
		}
		System.out.println();
		System.out.print("정렬 후 첫번째 수와 마지막 수의 합: ");
		System.out.println(inputInt[0]+inputInt[inputInt.length-1]);
		System.out.print("정렬 후 두번째 수와 마지막 수의 곱: ");
		System.out.println(inputInt[1]*inputInt[inputInt.length-1]);
		
	
	}

}

```
