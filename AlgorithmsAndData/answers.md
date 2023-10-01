# Answers

## Use recursion to find path through a maze
```js
const maze = [
  ['w','w', 'w', 'e', 'w'],
  ['w','o', 'w', 'o', 'w'],
  ['w','o', 'o', 'o', 'w'],
  ['w','o', 'w', 'e', 'w'],
  ['w','s', 'w', 'e', 'w']
];

const path = [];

// Top, right, bottom, left
const dirs = [ [-1, 0], [0, 1], [1, 0], [0, -1]];

const start = [4, 1];

function solve(startPoint) {
  let currentY = startPoint.y;
  let currentX = startPoint.x;
  if (maze[currentY][currentX] === 'e') {
    return true;
  }
  
  for (let j = 0; j < dirs.length; j++) {
    const nextPoint = {x: currentX + dirs[j][1] , y: currentY + dirs[j][0]};
    if (isOutOfBounds(nextPoint) || isWall(nextPoint) || isAlreadyVisited(nextPoint)) {
      if (j === dirs.length - 1) {
        // no joy! None of the directions work. 
        // therefore, we need to backtrack to the last point on our path
         const lastPointOnPath = path.pop();
         return solve(lastPointOnPath);
      } else {
         continue;
      }
    
    } else {
      // The nextPoint must be a possibility!
    
      // mark the current point as visited
      maze[currentY][currentX] = 'v';
      path.push({x: currentX, y: currentY});
     
      // now recurse with the new point
      return solve(nextPoint)
    }
  }
      
  return false;

}

const x = solve({y: 4, x: 1})
console.log(x);


function isAlreadyVisited({x, y}) {
  return maze[y][x] === 'v';
}

function isOutOfBounds({x, y}) {
    if (y < 0 || y >= maze.length || x < 0 || x >= maze[0].length) {
      return true;
    } else {
      return false;
    }
}

  function isWall({x, y}) {
    return maze[y][x] === 'w';
  }
```
