# QM-method
2022 논회설 선택과제

## 1. Version
* version : python3

## 2. TestCase
변수 개수, 민텀 개수, 민텀...

row
```swift
4 5 0 1 5 6 7
4 8 0 4 8 10 11 12 13 15
```
culumn
```swift
4 12 0 1 3 4 5 7 10 11 12 13 14 15
1 10 0 2 3 4 6 7 9 11 13 15
```
petrick
```swift
4 12 0 1 2 5 6 7 8 10 11 12 13 15
3 6 0 1 2 5 6 7
```
## 3. Algorithm
123
### 3.1. Find PI
asdf
### 3.2. Culumn Dominance
asdf
```swift
    cul = []
    pi_tmp.sort(key = lambda x:x[1]) 
    
    for i in range(len(pi_tmp)-1):
        tmp = pi_tmp.pop()
        tf = 0
        for j in pi_tmp:
            count = 0
            for k in range(j[1]):
                if(j[k+2] in tmp):
                    count += 1
            if(count == j[1]):
                change = 1
                tf = 1
        if(tf == 0):
            cul.append(tmp)
    pi_tmp += cul
```
### 3.3. Row Dominance
```swift
    row = [[i, 0]for i in answer]
    for i in pi_tmp:
        for j in range(len(i)-2):
            for k in row:
                if(i[j+2] in k):
                    k[1] += 1
                    k.append(i[0])
    row.sort(key = lambda x:x[1])
    
    for i in range(len(row)):
        if(row[i][1] == 0):
            continue
        for j in range(len(row)-1-i):
            count = 0
            for k in range(row[i][1]):
                if(row[i][k+2] in row[i+j+1]):
                    count += 1
            if(count == row[i][1]):
                for k in pi_tmp:
                    if(row[i][0] in k):
                        k.remove(row[i][0])
                        k[1] -=1
                        change = 1
```
### 3.4 Petrick Method
```swift
     if(change == 0 and len(pi_tmp) != 0):
        tmp = pi_tmp[0][2]
        for i in range(pi_tmp[0][1]):
            if(tmp.count("2") < pi_tmp[0][2+i].count("2")):
                tmp = pi_tmp[0][2+i]
        print(tmp, "petrick\n")
        ans.append(tmp)
        change = 1
```

## 4. Result
sadf
