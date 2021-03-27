<h1>첫 기술블로그</h1>
----
- 소풍
- 문제

    안드로메다 유치원 익스프레스반에서는 다음 주에 율동공원으로 소풍을 갑니다. 원석 선생님은 소풍 때 학생들을 두 명씩 짝을 지어 행동하게 하려고 합니다. 그런데 서로 친구가 아닌 학생들끼리 짝을 지어 주면 서로 싸우거나 같이 돌아다니지 않기 때문에, 항상 서로 친구인 학생들끼리만 짝을 지어 줘야 합니다.

    각 학생들의 쌍에 대해 이들이 서로 친구인지 여부가 주어질 때, 학생들을 짝지어줄 수 있는 방법의 수를 계산하는 프로그램을 작성하세요. 짝이 되는 학생들이 일부만 다르더라도 다른 방법이라고 봅니다. 예를 들어 다음 두 가지 방법은 서로 다른 방법입니다.

    (태연,제시카) (써니,티파니) (효연,유리)
    (태연,제시카) (써니,유리) (효연,티파니)

- 입력

    입력의 첫 줄에는 테스트 케이스의 수 C (C <= 50) 가 주어집니다. 각 테스트 케이스의 첫 줄에는 학생의 수 n (2 <= n <= 10) 과 친구 쌍의 수 m (0 <= m <= n*(n-1)/2) 이 주어집니다. 그 다음 줄에 m 개의 정수 쌍으로 서로 친구인 두 학생의 번호가 주어집니다. 번호는 모두 0 부터 n-1 사이의 정수이고, 같은 쌍은 입력에 두 번 주어지지 않습니다. 학생들의 수는 짝수입니다.

    - ex)

        ```
        3
        2 1
        0 1
        4 6
        0 1 1 2 2 3 3 0 0 2 1 3
        6 10
        0 1 0 2 1 2 1 3 1 4 2 3 2 4 3 4 3 5 4 5
        ```

- 출력

    각 테스트 케이스마다한 에 모든학생을 친구끼리만짝지어줄수 있는방법 
    의수를출력합니다.

    - ex)

        ```
        1
        3
        4
        ```

- 코드

    ```java
    package algo;

    import java.util.Scanner;

    public class picnic {
    	public static boolean [][] areFriends= new boolean [10][10]; 
    	public static boolean []taken = new boolean[10];
    	public static int ret = 0; 
    	public static int countPairings(boolean taken[]) { 
    		int firstFree = -1; 
    		for(int i = 0; i < 4; i++) { 
    			if(!taken[i]) {
    				firstFree = i;
    				System.out.println("FF"+i);
    				break; 
    			} 
    		} 
    		if(firstFree == -1) {
    			return 1; 
    		}
    		for(int pairWith=firstFree+1;pairWith< 4; pairWith++) {  
    			if(!taken[pairWith] && areFriends[firstFree][pairWith]){
    				System.out.println("왜안돼");
    				taken[firstFree] = true;
    				taken[pairWith] = true; 
    				ret+=countPairings(taken); 
    				taken[firstFree] = false;
    				taken[pairWith] = false; 
    		} 
    			System.out.println(ret);
    	}return ret;
    	}
    	public static void init() {
    		for(int i=0;i<10;i++) {
    	    	for(int j=0;j<10;j++) {
    	    	    areFriends[i][j]=false;
    	    	}taken[i]=false;
    	    }
    	}
    	public static void main(String[] args) {
    		Scanner scan = new Scanner(System.in);
    	    int C = scan.nextInt();
    	    for(int i=0;i<C;i++) {
    	    	int n = scan.nextInt();
    		    int m = scan.nextInt();
    		    init();
    		    for(int j=0;j<m;j++) {
    		    	int first = scan.nextInt();
    			    int second = scan.nextInt();
    			    areFriends[first][second]=true;
    			    areFriends[second][first]=true;
    		    }
    		    System.out.println(countPairings(taken));
    	    }
    	}
    }
    ```

- 풀이
    - 입력 예제를 해석하는 것에 시간이 걸렸는데 아래와 같이 첫째줄, 둘째,셋째줄, 넷째 다섯째 줄, 여섯 일곱째줄로 끊어서 봐야 한다

        ```
        3
        -------
        2 1
        0 1
        --------
        4 6
        0 1 1 2 2 3 3 0 0 2 1 3
        ---------------------------------------------
        6 10
        0 1 0 2 1 2 1 3 1 4 2 3 2 4 3 4 3 5 4 5
        ```

    - 제일 앞의 학생이 가질 수 있는 짝궁의 수를 구하고, 그때 다음 학생이 가질 수 있는 학생의 수를 재귀적으로 구해 곱해가는 방식으로 구한다.
    - 재귀적으로 함수를 호출하므로 이미 짝궁을 구한 학생을 제외한 학생들 중 가장 빠른 학생의 번호를 구하는 함수가 필요한데, 이때 학생들이 모두 짝을 구했으면 함수를 종료하고 경우의 수를 출력한다.
    - 서로 친한 친구인지를 담는 자료형은 boolean 2차원 배열로 학생 수는 최대 10명이므로 10x10의 배열로 생성한다
- 질문
    - 근데 왜 안돌아가지..