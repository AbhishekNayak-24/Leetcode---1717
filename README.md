# Leetcode---1717
Maximum Score From Removing Substrings
//code in java 
import java.util.Stack;

class Solution {
    public int maximumGain(String s, int x, int y) {
        int totalScore = 0;
        String firstPair, secondPair;
        int firstScore, secondScore;

        // Determine which pair to prioritize based on scores
        if (x > y) {
            firstPair = "ab";
            firstScore = x;
            secondPair = "ba";
            secondScore = y;
        } else {
            firstPair = "ba";
            firstScore = y;
            secondPair = "ab";
            secondScore = x;
        }

        // First pass: remove the higher-scoring pair
        Stack<Character> stack = new Stack<>();
        for (char c : s.toCharArray()) {
            if (!stack.isEmpty() && stack.peek() == firstPair.charAt(0) && c == firstPair.charAt(1)) {
                stack.pop();
                totalScore += firstScore;
            } else {
                stack.push(c);
            }
        }

        // Convert remaining characters in stack to a new string for the second pass
        StringBuilder remainingString = new StringBuilder();
        while (!stack.isEmpty()) {
            remainingString.append(stack.pop());
        }
        remainingString.reverse(); // Reverse to maintain original order

        // Second pass: remove the lower-scoring pair from the remaining string
        Stack<Character> newStack = new Stack<>();
        for (char c : remainingString.toString().toCharArray()) {
            if (!newStack.isEmpty() && newStack.peek() == secondPair.charAt(0) && c == secondPair.charAt(1)) {
                newStack.pop();
                totalScore += secondScore;
            } else {
                newStack.push(c);
            }
        }

        return totalScore;
    }
}
