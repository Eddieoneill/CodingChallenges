# CodingChallenges

## Description
Coding challenges that are not in leetcode

## Hungry Rabbit

```swift
func rb(_ mtx: [[Int]]) -> Int {
    var mtx = mtx
    var result = 0
    var dict: [Int: [Int]] = [:]
    let mtxCount = mtx.count - 1
    let arrCount = mtx[0].count - 1
    var canMove = true
    let x = mtxCount / 2
    let y = mtxCount / 2
    var currentLocation = [Int]()
    
    if mtxCount % 2 != 0 && arrCount % 2 != 0 {
        dict[mtx[x][y]] = [x, y]
    } else if x % 2 == 0 && y % 2 == 0 {
        dict[mtx[x][y]] = [x, y]
        dict[mtx[x + 1][y]] = [x + 1, y]
        dict[mtx[x][y + 1]] = [x, y + 1]
        dict[mtx[x + 1][y + 1]] = [x + 1, y + 1]
    } else if x % 2 == 0 {
        dict[mtx[x + 1][y]] = [x + 1, y]
        dict[mtx[x + 1][y + 1]] = [x + 1, y + 1]
    } else {
        dict[mtx[x][y + 1]] = [x, y + 1]
        dict[mtx[x + 1][y + 1]] = [x + 1, y + 1]
    }
    currentLocation = dict[maxVal(dict)] ?? [0, 0]
    mtx[currentLocation[0]][currentLocation[1]] = 0
    result += maxVal(dict)
    while canMove {
        print(currentLocation)
        guard let nextMove = nextMove(mtx, currentLocation) else {
            canMove = false
            break
        }
        currentLocation = nextMove
        result += mtx[currentLocation[0]][currentLocation[1]]
        mtx[currentLocation[0]][currentLocation[1]] = 0
    }
    
    return result
}

func nextMove(_ mtx: [[Int]],_ current: [Int]) -> [Int]? {
    let currentX = current[0]
    let currentY = current[1]
    var possibleMove = [Int: [Int]]()
    var maxValue = 0
    if currentX != 0 && currentX != mtx.count - 1 && currentY != 0 && currentY != mtx[0].count - 1 {
        print(1)
        possibleMove[mtx[currentX - 1][currentY]] = [currentX - 1, currentY]
        possibleMove[mtx[currentX + 1][currentY]] = [currentX + 1, currentY]
        possibleMove[mtx[currentX][currentY + 1]] = [currentX, currentY + 1]
        possibleMove[mtx[currentX][currentY - 1]] = [currentX, currentY - 1]
        
    } else if currentX == 0 && currentY == 0 {
        print(2)
        possibleMove[mtx[currentX + 1][currentY]] = [currentX + 1, currentY]
        possibleMove[mtx[currentX][currentY + 1]] = [currentX, currentY + 1]
        
    } else if currentX == mtx.count - 1 && currentY == 0 {
        print(3)
        possibleMove[mtx[currentX - 1][currentY]] = [currentX - 1, currentY]
        possibleMove[mtx[currentX][currentY + 1]] = [currentX, currentY + 1]
        
    } else if currentX == 0 && currentY == mtx[0].count - 1 {
        print(4)
        possibleMove[mtx[currentX + 1][currentY]] = [currentX + 1, currentY]
        possibleMove[mtx[currentX][currentY - 1]] = [currentX, currentY - 1]
        
    } else if currentX == mtx.count - 1 && currentY == mtx[0].count - 1 {
        print(5)
        possibleMove[mtx[currentX - 1][currentY]] = [currentX - 1, currentY]
        possibleMove[mtx[currentX][currentY - 1]] = [currentX, currentY - 1]
        
    } else if currentX == 0 {
        print(6)
        possibleMove[mtx[currentX + 1][currentY]] = [currentX + 1, currentY]
        possibleMove[mtx[currentX][currentY + 1]] = [currentX, currentY + 1]
        possibleMove[mtx[currentX][currentY - 1]] = [currentX, currentY - 1]
        
    } else if currentX == mtx.count - 1 {
        print(7)
        possibleMove[mtx[currentX - 1][currentY]] = [currentX - 1, currentY]
        possibleMove[mtx[currentX][currentY + 1]] = [currentX, currentY + 1]
        possibleMove[mtx[currentX][currentY - 1]] = [currentX, currentY - 1]
        
    } else if currentY == 0 {
        print(8)
        possibleMove[mtx[currentX - 1][currentY]] = [currentX - 1, currentY]
        possibleMove[mtx[currentX + 1][currentY]] = [currentX + 1, currentY]
        possibleMove[mtx[currentX][currentY + 1]] = [currentX, currentY + 1]
        
    } else if currentY == mtx[0].count - 1 {
        print(9)
        possibleMove[mtx[currentX - 1][currentY]] = [currentX - 1, currentY]
        possibleMove[mtx[currentX + 1][currentY]] = [currentX + 1, currentY]
        possibleMove[mtx[currentX][currentY - 1]] = [currentX, currentY - 1]
    }
    
    maxValue = Array(possibleMove.keys).max() ?? 0
    
    if maxValue != 0 {
        return possibleMove[maxValue]
    } else {
        return nil
    }
}

func maxVal(_ dict: [Int: [Int]]) -> Int {
    return Array(dict.keys).max() ?? 0
}
```
