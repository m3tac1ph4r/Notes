# Gas Stations

There are `n` gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return _the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return_ `-1`. If there exists a solution, it is **guaranteed** to be **unique**

**Example 1:**

**Input:** gas = [ 1,2,3,4,5], cost = [3,4,5,1,2]
**Output:** 3
**Explanation:**
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.

**Example 2:**

**Input:** gas = [2,3,4], cost = [3,4,3]
**Output:** -1
**Explanation:**
You can't start at station 0 or 1, as there is not enough gas to travel to the next station.
Let's start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 0. Your tank = 4 - 3 + 2 = 3
Travel to station 1. Your tank = 3 - 3 + 3 = 3
You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3.
Therefore, you can't travel around the circuit once no matter where you start.


### Approach :

![[gas_stations_app.png]]

1. We will start a for loop from 0 to n-1 and **take variable balance for storing the curent fuel balance** and start for storing the starting index and deficit variable for storing the negative index. 
	1. We have to start from that index such that we can successfully return again.
	2. So we will get **balance by subtracting gas[i] (refilled gas) - cost[i] (how much gas will be consumed to reach next station)**.
	3. So if **consumed_gas - gas_available is less than 0 means we need that much extra gas in returning to come at that index. Means we can't start from that index. So start_index=i+1**
	4. And will update balance=0 because we will not start from index i
2. In last **check the available_balance gas will cover the gas which will be required in returing to that index**. If it's true means answer is that index else no such index is present.

```cpp
int canCompleteCircuit(vector<int> &gas, vector<int> &cost)
{
    int deficit = 0; // kami
    int balance = 0;
    int start = 0;
    int n = gas.size();
    for (int i = 0; i < n; i++)
    {
        balance += gas[i] - cost[i];
        if (balance < 0)
        {
            deficit += balance;
            start = i + 1;
            balance = 0;
        }
    }
    if (deficit + balance >= 0)
        return start;
    else
        return -1;
}
```


### Question :
https://leetcode.com/problems/gas-station/


### Reference :
https://youtu.be/HQpDS9wuzws