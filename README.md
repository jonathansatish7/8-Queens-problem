# Hide and Seek

1. In this part we will be working on arranging the pichus 'p' such that no pichu will be on the same row and columnn until or unless there is an obstacle in between pichus. The obstacle can either be the wall 'X' or the person '@'.

2. Like the previous part the first thing I did is that I used the print statements to understand what is entering the fringe and what are getting popped out of the fringe.  

3. The successors function in this case prints out all the possible successors to the initial state which is the initial board setup. The successors function uses the add_pichu method and prints out all the possible successors in the below format

[['p', '.', '.', '.', 'X', 'X', 'X'], ['.', 'X', 'X', 'X', '.', '.', '.'], ['.', '.', '.', '.', 'X', '.', '.'], ['.', 'X', '.', 'X', '.', '.', '.'], ['.', 'X', '.', 'X', '.', 'X', '.'], ['p', 'X', '.', '.', '.', 'X', '@']]
[['.', 'p', '.', '.', 'X', 'X', 'X'], ['.', 'X', 'X', 'X', '.', '.', '.'], ['.', '.', '.', '.', 'X', '.', '.'], ['.', 'X', '.', 'X', '.', '.', '.'], ['.', 'X', '.', 'X', '.', 'X', '.'], ['p', 'X', '.', '.', '.', 'X', '@']]
[['.', '.', 'p', '.', 'X', 'X', 'X'], ['.', 'X', 'X', 'X', '.', '.', '.'], ['.', '.', '.', '.', 'X', '.', '.'], ['.', 'X', '.', 'X', '.', '.', '.'], ['.', 'X', '.', 'X', '.', 'X', '.'], ['p', 'X', '.', '.', '.', 'X', '@']]
[['.', '.', '.', 'p', 'X', 'X', 'X'], ['.', 'X', 'X', 'X', '.', '.', '.'], ['.', '.', '.', '.', 'X', '.', '.'], ['.', 'X', '.', 'X', '.', '.', '.'], ['.', 'X', '.', 'X', '.', 'X', '.'], ['p', 'X', '.', '.', '.', 'X', '@']]

4. So if we look at the above case all the possibilities are being passed on to the fringe even though they are invalid state. initially so in order to eliminate the invalid cases being pushed into the fringe I have defined some set of conditions in the check_before_append function

                    for row in range(0,len(board)):
                        for column in range(0,len(board[0])):
                            if(board[row][column]=='p'):
                                for i in range(row+1,len(board)):
                                    if board[i][column]=='X' or board[i][column]=='@':
                                        break
                                    if board[i][column]=='p':
                                        return False
                                for i in range(row-1,-1,-1):
                                    if board[i][column]=='X' or board[i][column]=='@':
                                        break
                                    if board[i][column]=='p':
                                        return False
                                for i in range(column+1,len(board[0])):
                                    if board[row][i]=='X' or board[row][i]=='@':
                                        break
                                    if board[row][i]=='p':
                                        return False
                                for i in range(column-1,-1,-1):
                                    if board[row][i]=='X' or board[row][i]=='@':
                                        break
                                    if board[row][i]=='p':
                                        return False
                    return True

The above conditions checks for all 'p' on the map on the directions (Up, Down, Left and Right) from the point 'p', if one more 'p' appears before 'X' or '@' The function will return False stating that it is invalid condition and it won't add in the fringe.

5. The is_goal function checks whether the map has number of 'p' which are required then it would return the map and the whole program terminates, but when I directly returned and it throws wrong map as it calls all successors of popped out item in fringe so in order to avoid this we have verify the all the successors using the previous condition.

6. Then I printed the whole fringe and verified. Then I found that there are again invalid states even though they are valid before entering into fringe.

7. I then eliminated the invalid state by including the same condition mentioned above and then ran the program and I got the required map.


* The set of valid states in this problem is the map which has 'p' in such a form that no two 'p' are on the same row and same column until or unless there is wall or man between them.

* The successor function is the function which generates the next map by adding pichus, in this case the successor function is
def successors(board):
    return [ add_pichu(board, r, c) for r in range(0, len(board)) for c in range(0,len(board[0])) if board[r][c] == '.' ] returns all the

* There is no cost function in this case.

* In this case the goal state will be the map with required number of pichus where no pichu can see each other.

* The initial state will be map which we enter before the program runs.
