### day2_1_计算
```python
def calc(a,b,c):
    if a==1:
        return b+c
    if a==2:
        return b*c

Intcode="1,12,2,3,1,1,2,3,1,3,4,3,1,5,0,3,2,6,1,19,1,5,19,23,2,6,23,27,1,27,5,31,2,9,31,35,1,5,35,39,2,6,39,43,2,6,43,47,1,5,47,51,2,9,51,55,1,5,55,59,1,10,59,63,1,63,6,67,1,9,67,71,1,71,6,75,1,75,13,79,2,79,13,83,2,9,83,87,1,87,5,91,1,9,91,95,2,10,95,99,1,5,99,103,1,103,9,107,1,13,107,111,2,111,10,115,1,115,5,119,2,13,119,123,1,9,123,127,1,5,127,131,2,131,6,135,1,135,5,139,1,139,6,143,1,143,6,147,1,2,147,151,1,151,5,0,99,2,14,0,0"
smokes=[int(c) for c in Intcode.split(",")]
for i in range(0,len(smokes),4):
    if smokes[i]==99:
        break
    val=calc(smokes[i],smokes[smokes[i+1]],smokes[smokes[i+2]])
    smokes[smokes[i+3]]=val
print(smokes[0])
```

### day2_2_遍历 深拷贝

```python
#1-noun
#2-verb
#between 0 and 99
#Find the input noun and verb that cause the program to produce
#  the output 19690720. 
# What is 100 * noun + verb? 
#遍历，深拷贝
import copy
def calc(a,b,c):
    # print(a,b,c)
    if a==1:
        return b+c
    if a==2:
        return b*c

Intcode="1,12,2,3,1,1,2,3,1,3,4,3,1,5,0,3,2,6,1,19,1,5,19,23,2,6,23,27,1,27,5,31,2,9,31,35,1,5,35,39,2,6,39,43,2,6,43,47,1,5,47,51,2,9,51,55,1,5,55,59,1,10,59,63,1,63,6,67,1,9,67,71,1,71,6,75,1,75,13,79,2,79,13,83,2,9,83,87,1,87,5,91,1,9,91,95,2,10,95,99,1,5,99,103,1,103,9,107,1,13,107,111,2,111,10,115,1,115,5,119,2,13,119,123,1,9,123,127,1,5,127,131,2,131,6,135,1,135,5,139,1,139,6,143,1,143,6,147,1,2,147,151,1,151,5,0,99,2,14,0,0"
smokes=[int(c) for c in Intcode.split(",")]
smokes2=copy.deepcopy(smokes)
# print(smokes2)
flag=0
for a in range(0,100):
    for b in range(0,100):
        smokes[1]=a
        smokes[2]=b
        for i in range(0,len(smokes),4):
            if smokes[i]==99:
                break
            # print(i)
            val=calc(smokes[i],smokes[smokes[i+1]],smokes[smokes[i+2]])
            smokes[smokes[i+3]]=val
        if(smokes[0]==19690720):
            print(100*a+b)
            flag=1
        smokes=copy.deepcopy(smokes2)
        # print(smokes)
    if flag==1:
        break
```
