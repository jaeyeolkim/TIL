# [Iterations]
# 1. BinaryGap
Task description
A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

class Solution { public int solution(int N); }

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Assume that:

N is an integer within the range [1..2,147,483,647].
Complexity:

expected worst-case time complexity is O(log(N));
expected worst-case space complexity is O(1).

```
class Solution {
    public int solution(int N) {
        String binary = Integer.toBinaryString(N);
        int gap = 0;
        String[] binarys = binary.split("1");
        for (String zeros : binarys) {
            String match = "1"+zeros+"1";
            if(binary.indexOf(match) > -1){
                gap = (zeros.length() > gap)? zeros.length(): gap;
            }
        }
        return gap;
    }
}
```

# [Arrays]
# 2-1. CyclicRotation

Task description
An array A consisting of N integers is given. Rotation of the array means that each element is shifted right by one index, and the last element of the array is moved to the first place. For example, the rotation of array A = [3, 8, 9, 7, 6] is [6, 3, 8, 9, 7] (elements are shifted right by one index and 6 is moved to the first place).

The goal is to rotate array A K times; that is, each element of A will be shifted to the right K times.

Write a function:

class Solution { public int[] solution(int[] A, int K); }

that, given an array A consisting of N integers and an integer K, returns the array A rotated K times.

For example, given

    A = [3, 8, 9, 7, 6]
    K = 3
the function should return [9, 7, 6, 3, 8]. Three rotations were made:

    [3, 8, 9, 7, 6] -> [6, 3, 8, 9, 7]
    [6, 3, 8, 9, 7] -> [7, 6, 3, 8, 9]
    [7, 6, 3, 8, 9] -> [9, 7, 6, 3, 8]
For another example, given

    A = [0, 0, 0]
    K = 1
the function should return [0, 0, 0]

Given

    A = [1, 2, 3, 4]
    K = 4
the function should return [1, 2, 3, 4]

Assume that:

N and K are integers within the range [0..100];
each element of array A is an integer within the range [−1,000..1,000].
In your solution, focus on correctness. The performance of your solution will not be the focus of the assessment.

```
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

class Solution {
    public int[] solution(int[] A, int K) {
        //empty test error
        if(A.length == 0 || K == 0){
            return A;
        }
        
        int mod = K % A.length;
        //int array to list
        List<Integer> list = Arrays.stream(A).boxed().collect(Collectors.toList());

        int index = A.length-1;
        for(int i=mod; i > 0; i--){
            list.add(0, A[index--]);
            list.remove(list.size()-1);
        }
        
        //list to int array
        return list.stream().mapToInt(i->i).toArray();
    }
}
```

# 2-2 OddOccurrencesInArray
A non-empty array A consisting of N integers is given. The array contains an odd number of elements, and each element of the array can be paired with another element that has the same value, except for one element that is left unpaired.

For example, in array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9
  A[3] = 3  A[4] = 9  A[5] = 7
  A[6] = 9
the elements at indexes 0 and 2 have value 9,
the elements at indexes 1 and 3 have value 3,
the elements at indexes 4 and 6 have value 9,
the element at index 5 has value 7 and is unpaired.
Write a function:

class Solution { public int solution(int[] A); }

that, given an array A consisting of N integers fulfilling the above conditions, returns the value of the unpaired element.

For example, given array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9
  A[3] = 3  A[4] = 9  A[5] = 7
  A[6] = 9
the function should return 7, as explained in the example above.

Assume that:

N is an odd integer within the range [1..1,000,000];
each element of array A is an integer within the range [1..1,000,000,000];
all but one of the values in A occur an even number of times.

```
import java.util.Map;
import java.util.HashMap;

class Solution {
    public int solution(int[] A) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        int unpaired = 0;
        
        for(int i=0; i < A.length; i++){
            int count = 1;
            if(map.get(A[i]) != null && map.get(A[i]) != 2){
                count = 2;
            }
            map.put(A[i], count);
        }
        
        for(int key : map.keySet()){
            if(map.get(key) == 1){
                unpaired = key;
                break;
            }
        }
        
        return unpaired;
    }
}
```

# [Time Complexity]
# 3-1 FrogJmp
Count minimal number of jumps from position X to Y.

A small frog wants to get to the other side of the road. The frog is currently located at position X and wants to get to a position greater than or equal to Y. The small frog always jumps a fixed distance, D.

Count the minimal number of jumps that the small frog must perform to reach its target.

Write a function:

class Solution { public int solution(int X, int Y, int D); }

that, given three integers X, Y and D, returns the minimal number of jumps from position X to a position equal to or greater than Y.

For example, given:

  X = 10
  Y = 85
  D = 30
the function should return 3, because the frog will be positioned as follows:

after the first jump, at position 10 + 30 = 40
after the second jump, at position 10 + 30 + 30 = 70
after the third jump, at position 10 + 30 + 30 + 30 = 100
Assume that:

X, Y and D are integers within the range [1..1,000,000,000];
X ≤ Y.

```
class Solution {
    public int solution(int X, int Y, int D) {
        int distance = Y-X;
        int mod = distance % D;
        if(mod == 0){
            return distance / D;
        }else{
            return (distance / D) + 1;
        }
    }
}
```

# 3-2 PermMissingElem
An array A consisting of N different integers is given. The array contains integers in the range [1..(N + 1)], which means that exactly one element is missing.

Your goal is to find that missing element.

Write a function:

class Solution { public int solution(int[] A); }

that, given an array A, returns the value of the missing element.

For example, given array A such that:

  A[0] = 2
  A[1] = 3
  A[2] = 1
  A[3] = 5
the function should return 4, as it is the missing element.

Assume that:

N is an integer within the range [0..100,000];
the elements of A are all distinct;
each element of array A is an integer within the range [1..(N + 1)].

```
import java.util.Arrays;

class Solution {
    public int solution(int[] A) {
        if(A == null || A.length == 0){
            return 1;
        }
        if(A.length == 1 && A[0] == 1){
            return 2;
        }
        
        Arrays.sort(A);
        
        if(A[0] != 1){
            return 1;
        }
        
        int missing = A[0];
        for(int i : A){
            if(i == missing){
                missing++;
                continue;
            }
            break;
        }
        return missing;
    }
}
```

# 3-3 TapeEquilibrium

A non-empty array A consisting of N integers is given. Array A represents numbers on a tape.

Any integer P, such that 0 < P < N, splits this tape into two non-empty parts: A[0], A[1], ..., A[P − 1] and A[P], A[P + 1], ..., A[N − 1].

The difference between the two parts is the value of: |(A[0] + A[1] + ... + A[P − 1]) − (A[P] + A[P + 1] + ... + A[N − 1])|

In other words, it is the absolute difference between the sum of the first part and the sum of the second part.

For example, consider array A such that:

  A[0] = 3
  A[1] = 1
  A[2] = 2
  A[3] = 4
  A[4] = 3
We can split this tape in four places:

P = 1, difference = |3 − 10| = 7 
P = 2, difference = |4 − 9| = 5 
P = 3, difference = |6 − 7| = 1 
P = 4, difference = |10 − 3| = 7 
Write a function:

class Solution { public int solution(int[] A); }

that, given a non-empty array A of N integers, returns the minimal difference that can be achieved.

For example, given:

  A[0] = 3
  A[1] = 1
  A[2] = 2
  A[3] = 4
  A[4] = 3
the function should return 1, as explained above.

Assume that:

N is an integer within the range [2..100,000];
each element of array A is an integer within the range [−1,000..1,000].
Complexity:

expected worst-case time complexity is O(N);
expected worst-case space complexity is O(N) (not counting the storage required for input arguments).

```
풀고 있는 중...

class Solution {
    public int solution(int[] A) {
        int abs = 0;
        for(int i=0; i<A.length; i++){
            int left = 0;
            int right = 0;
            
            for(int j=0; j<=i; j++){
                left += A[j];
            }
            for(int j=i+1; j<A.length; j++){
                right += A[j];
            }
            
            if(abs < Math.abs(left - right)){
                abs = Math.abs(left - right);
            }
        }
        return abs;
    }
}
```
