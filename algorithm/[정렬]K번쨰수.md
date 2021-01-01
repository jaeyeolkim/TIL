- Arrays.copyOfRange(원본 배열, startIndex, endIndex-1)
```java
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        for(int i=0; i<commands.length; i++){
            int[] copys = Arrays.copyOfRange(array, commands[i][0]-1, commands[i][1]);
            Arrays.sort(copys);
            answer[i] = copys[commands[i][2]-1];
        }
        return answer;
    }
}
```