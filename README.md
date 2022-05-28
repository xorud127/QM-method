# QM-method
2022 논회설 선택과제

## Table of Contents
* [1. Version](#1.-Version)
* [2. TestCase](#2.-TestCase)
* [3. Algorithm](#3.-Algorithm)
    + ?
* [4. Result](#4.-Result)

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
answer.sort(key = lambda x:-x.count("2"))

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
2.TestCase의 실행 결과 정리

```swift
minterm :  [4, 5, 0, 1, 5, 6, 7] 

[['0000', 1, '0002'], ['0001', 2, '0002', '0201'], ['0101', 2, '0201', '0121'], ['0110', 1, '0112'], ['0111', 2, '0121', '0112']] pis
---------------------------------------------------------------------
[['0101', 2, '0201', '0121']] cul
[['0101', 2, '0201', '0121']] after cul

[['0002', 0], ['0112', 0], ['0201', 1, '0101'], ['0121', 1, '0101']] row
[['0101', 1, '0121']] after row
---------------------------------------------------------------------
middle :  ['000-', '011-', '01-1', '0-01', 'EPI', '000-', '011-']
final :  ['000-', '011-', '01-1']



minterm :  [4, 8, 0, 4, 8, 10, 11, 12, 13, 15] 

[['0000', 1, '2200'], ['0100', 1, '2200'], ['1000', 2, '2200', '1020'], ['1010', 2, '1020', '1012'], ['1011', 2, '1012', '1211'], 
['1100', 2, '2200', '1102'], ['1101', 2, '1102', '1121'], ['1111', 2, '1121', '1211']] pis
---------------------------------------------------------------------
[['1111', 2, '1121', '1211'], ['1101', 2, '1102', '1121'], ['1011', 2, '1012', '1211'], ['1010', 2, '1020', '1012']] cul
[['1111', 2, '1121', '1211'], ['1010', 2, '1020', '1012'], ['1011', 2, '1012', '1211'], ['1101', 2, '1102', '1121']] after cul

[['2200', 0], ['1020', 1, '1010'], ['1102', 1, '1101'], ['1012', 2, '1010', '1011'], ['1121', 2, '1111', '1101'], ['1211', 2, '1111', '1011']] row
[['1111', 2, '1121', '1211'], ['1010', 1, '1012'], ['1011', 2, '1012', '1211'], ['1101', 1, '1121']] after row
---------------------------------------------------------------------
middle :  ['101-', '10-0', '110-', '11-1', '1-11', '--00', 'EPI', '--00']
final :  ['101-', '11-1', '--00']



minterm :  [4, 12, 0, 1, 3, 4, 5, 7, 10, 11, 12, 13, 14, 15] 

[['0000', 1, '0202'], ['0001', 2, '0202', '0221'], ['0011', 2, '0221', '2211'], ['0100', 2, '0202', '2102'], 
['0101', 4, '0202', '2102', '0221', '2121'], ['0111', 3, '0221', '2121', '2211'], ['1010', 1, '1212'], ['1011', 2, '1212', '2211'], 
['1100', 2, '2102', '1122'], ['1101', 3, '2102', '1122', '2121'], ['1110', 2, '1122', '1212'], ['1111', 4, '1122', '1212', '2121', '2211']] pis
---------------------------------------------------------------------
[['1100', 2, '2102', '1122'], ['0011', 2, '0221', '2211'], ['1101', 3, '2102', '1122', '2121'], ['0111', 3, '0221', '2121', '2211']] cul
[['1100', 2, '2102', '1122'], ['0011', 2, '0221', '2211']] after cul

[['0202', 0], ['1212', 0], ['2121', 0], ['2102', 1, '1100'], ['0221', 1, '0011'], ['1122', 1, '1100'], ['2211', 1, '0011']] row
[['1100', 1, '1122'], ['0011', 1, '2211']] after row
---------------------------------------------------------------------
middle :  ['0-0-', '0--1', '11--', '1-1-', '-10-', '-1-1', '--11', 'EPI', '0-0-', '1-1-']
final :  ['0-0-', '11--', '1-1-', '--11']



minterm :  [4, 10, 0, 2, 3, 4, 6, 7, 9, 11, 13, 15] 

[['0000', 1, '0220'], ['0010', 2, '0220', '0212'], ['0011', 2, '0212', '2211'], ['0100', 1, '0220'], ['0110', 2, '0220', '0212'], 
['0111', 2, '0212', '2211'], ['1001', 1, '1221'], ['1011', 2, '1221', '2211'], ['1101', 1, '1221'], ['1111', 2, '1221', '2211']] pis
---------------------------------------------------------------------
[['0111', 2, '0212', '2211'], ['0011', 2, '0212', '2211']] cul
[['0111', 2, '0212', '2211']] after cul

[['0220', 0], ['1221', 0], ['0212', 1, '0111'], ['2211', 1, '0111']] row
[['0111', 1, '2211']] after row
---------------------------------------------------------------------
middle :  ['0-1-', '0--0', '1--1', '--11', 'EPI', '0--0', '1--1']
final :  ['0--0', '1--1', '--11']



minterm :  [4, 12, 0, 1, 2, 5, 6, 7, 8, 10, 11, 12, 13, 15] 

[['0000', 2, '2020', '0002'], ['0001', 2, '0002', '0201'], ['0010', 2, '2020', '0210'], ['0101', 2, '2121', '0201'], 
['0110', 2, '0210', '0112'], ['0111', 2, '2121', '0112'], ['1000', 2, '2020', '1200'], ['1010', 2, '2020', '1012'], 
['1011', 2, '1012', '1211'], ['1100', 2, '1200', '1102'], ['1101', 2, '2121', '1102'], ['1111', 2, '2121', '1211']] pis
---------------------------------------------------------------------
[['1111', 2, '2121', '1211'], ['1101', 2, '2121', '1102'], ['1100', 2, '1200', '1102'], ['1011', 2, '1012', '1211'], 
['1010', 2, '2020', '1012'], ['1000', 2, '2020', '1200'], ['0111', 2, '2121', '0112'], ['0110', 2, '0210', '0112'], 
['0101', 2, '2121', '0201'], ['0010', 2, '2020', '0210'], ['0001', 2, '0002', '0201'], ['0000', 2, '2020', '0002']] cul
[['1111', 2, '2121', '1211'], ['0000', 2, '2020', '0002'], ['0001', 2, '0002', '0201'], ['0010', 2, '2020', '0210'], 
['0101', 2, '2121', '0201'], ['0110', 2, '0210', '0112'], ['0111', 2, '2121', '0112'], ['1000', 2, '2020', '1200'],
['1010', 2, '2020', '1012'], ['1011', 2, '1012', '1211'], ['1100', 2, '1200', '1102'], ['1101', 2, '2121', '1102']] after cul

[['0002', 2, '0000', '0001'], ['1200', 2, '1000', '1100'], ['0210', 2, '0010', '0110'], ['0201', 2, '0001', '0101'], 
['1102', 2, '1100', '1101'], ['1012', 2, '1010', '1011'], ['0112', 2, '0110', '0111'], ['1211', 2, '1111', '1011'], 
['2020', 4, '0000', '0010', '1000', '1010'], ['2121', 4, '1111', '0101', '0111', '1101']] row
[['1111', 2, '2121', '1211'], ['0000', 2, '2020', '0002'], ['0001', 2, '0002', '0201'], ['0010', 2, '2020', '0210'],
['0101', 2, '2121', '0201'], ['0110', 2, '0210', '0112'], ['0111', 2, '2121', '0112'], ['1000', 2, '2020', '1200'], 
['1010', 2, '2020', '1012'], ['1011', 2, '1012', '1211'], ['1100', 2, '1200', '1102'], ['1101', 2, '2121', '1102']] after row

2121 petrick
---------------------------------------------------------------------
[['1100', 2, '1200', '1102'], ['1011', 2, '1012', '1211'], ['1010', 2, '2020', '1012'], ['1000', 2, '2020', '1200'], 
['0110', 2, '0210', '0112'], ['0010', 2, '2020', '0210'], ['0001', 2, '0002', '0201'], ['0000', 2, '2020', '0002']] cul
[['1100', 2, '1200', '1102'], ['0000', 2, '2020', '0002'], ['0001', 2, '0002', '0201'], ['0010', 2, '2020', '0210'], 
['0110', 2, '0210', '0112'], ['1000', 2, '2020', '1200'], ['1010', 2, '2020', '1012'], ['1011', 2, '1012', '1211']] after cul

[['2121', 0], ['0201', 1, '0001'], ['1102', 1, '1100'], ['0112', 1, '0110'], ['1211', 1, '1011'], ['0002', 2, '0000', '0001'], 
['1200', 2, '1100', '1000'], ['0210', 2, '0010', '0110'], ['1012', 2, '1010', '1011'], ['2020', 4, '0000', '0010', '1000', '1010']] row
[['1100', 1, '1200'], ['0000', 2, '2020', '0002'], ['0001', 1, '0002'], ['0010', 2, '2020', '0210'], ['0110', 1, '0210'], 
['1000', 2, '2020', '1200'], ['1010', 2, '2020', '1012'], ['1011', 1, '1012']] after row
---------------------------------------------------------------------
middle :  ['000-', '011-', '0-01', '0-10', '101-', '110-', '1-00', '1-11', '-0-0', '-1-1', 'EPI']
final :  ['000-', '0-10', '101-', '1-00', '-1-1']



minterm :  [3, 6, 0, 1, 2, 5, 6, 7] 

[['000', 2, '020', '002'], ['001', 2, '002', '201'], ['010', 2, '020', '210'], ['101', 2, '201', '121'], 
['110', 2, '210', '112'], ['111', 2, '121', '112']] pis
---------------------------------------------------------------------
[['111', 2, '121', '112'], ['110', 2, '210', '112'], ['101', 2, '201', '121'], ['010', 2, '020', '210'],
['001', 2, '002', '201'], ['000', 2, '020', '002']] cul
[['111', 2, '121', '112'], ['000', 2, '020', '002'], ['001', 2, '002', '201'], ['010', 2, '020', '210'], 
['101', 2, '201', '121'], ['110', 2, '210', '112']] after cul

[['020', 2, '000', '010'], ['002', 2, '000', '001'], ['201', 2, '001', '101'], ['210', 2, '010', '110'], 
['121', 2, '111', '101'], ['112', 2, '111', '110']] row
[['111', 2, '121', '112'], ['000', 2, '020', '002'], ['001', 2, '002', '201'], ['010', 2, '020', '210'], 
['101', 2, '201', '121'], ['110', 2, '210', '112']] after row

121 petrick
---------------------------------------------------------------------
[['110', 2, '210', '112'], ['010', 2, '020', '210'], ['001', 2, '002', '201'], ['000', 2, '020', '002']] cul
[['110', 2, '210', '112'], ['000', 2, '020', '002'], ['001', 2, '002', '201'], ['010', 2, '020', '210']] after cul

[['121', 0], ['201', 1, '001'], ['112', 1, '110'], ['020', 2, '000', '010'], ['002', 2, '000', '001'], ['210', 2, '110', '010']] row
[['110', 1, '210'], ['000', 2, '020', '002'], ['001', 1, '002'], ['010', 2, '020', '210']] after row
---------------------------------------------------------------------
middle :  ['00-', '0-0', '11-', '1-1', '-01', '-10', 'EPI']
final :  ['00-', '1-1', '-10']
```
