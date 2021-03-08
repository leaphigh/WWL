```java
import java.util.Stack;

class Solution {
    public int calculate(String s) {
        Stack<Integer> stk = new Stack<>();
        int number = 0;
        char op = '+';
				
				// 1. 문자열로 구성된 식을 순회하면서 처리한다
        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) number = (number * 10) + (c - 48);
            else if (!Character.isWhitespace(c)) {
                stk.push(evaluate(stk, op, number));
                op = c;
                number = 0;
            }
        }
        stk.push(evaluate(stk, op, number));
        
				// 2. 스택에서 하나씩 꺼내면서 모두 더한다
        int ret = 0;
        while (!stk.isEmpty()) {
            ret += stk.pop();  
        }

        return ret;
    }
    
    int evaluate(Stack<Integer> stk, final char opration, final int operand) {
        int ret = 0;
        if (opration == '+')      ret = operand;
        else if (opration == '-') ret = -1 * operand;
        else if (opration == '*') ret = stk.pop() * operand; 
        else if (opration == '/') ret = stk.pop() / operand;
        return ret;
    }
}
```