```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {

        /*
            - prerequisites[i][0]: a
            - prerequisites[i][1]: b
            - indegrees[i]: i번째 코스의 indegree
            - outsOfEachCourses.get(i): i번째 코스가 선수 과목인 과목들의 리스트(LinkedList)
        */
        
        int[] indegrees = new int[numCourses];
        List<Integer>[] outsOfEachCourses = new LinkedList[numCourses];
        
        for (int i = 0; i < outsOfEachCourses.length; i++) {
            outsOfEachCourses[i] = new LinkedList<>();
        }
        
        for (int[] pre : prerequisites) {
            // b -> a
            int a = pre[0];
            int b = pre[1];
            indegrees[a]++; 
            List<Integer> outsOfCourse = outsOfEachCourses[b];
            outsOfCourse.add(a); // b -> a
        }
        
        Queue<List<Integer>> queue = new LinkedList<>();

        for (int i = 0; i < indegrees.length; i++) {
            if (indegrees[i] == 0) {
                queue.offer(outsOfEachCourses[i]);
            }
        }
        
        int cntCompleted = 0;
        
        while (!queue.isEmpty()) {
            List<Integer> outsOfCourse = queue.poll();
            cntCompleted++;
            for (Integer out : outsOfCourse) {
                indegrees[out]--;
                if (indegrees[out] == 0) {
                    queue.offer(outsOfEachCourses[out]);
                }
            }
        }
        
        return (cntCompleted == numCourses);
    }
}
```