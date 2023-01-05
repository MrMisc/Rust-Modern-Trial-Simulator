# Rust Modern Trial Simulator
 Appended version of earlier trial simulator @ https://github.com/MrMisc/RustyTrialSimulator. Experimental. Contains probability values that increase as part of a modern pity system commonly found in Modern MMOs


Added an M series of methods. Code may or may not be quite buggy to run. 


## M series | Methods

In addition to the logic previously, there is now an additional set of methods that range between 100.000 to 10.000.000+++

The meaning behind these methods are as follows, starting from the left.

The first digit represents whether we use the old pity system - 2 consecutive fails lead to a success. 0 means there is none, 1 means there is. A binary switch, in other words.

The second digit indicates the reinforcement system. The number indicates as before, how many successive successes are required to earn a free success. 

Third digit represents the method class:1,2,3 and 4+ for no method. These are the user behaviours that made up the building block of the original simulator.

The 4th and 5th digit are meant to represent the number of failures required to occur at a fixed level (*) for the version 2 of the pity system to be invoked. If you For eg, in 1003100, you are on method class 1, as previously illustrated, and it takes '03' fails in a row for the pity system to take effect.

Finally, there are either 1,2 or above 3 remaining digits that make up the method number. If there are 1-2 digits left, this means that this is the % probability that is ADDED to the trial that the seed is stuck on attempting. This probability for this trial is continuously increased, free to reach 100%. 

However, if there are more than 2 digits, this tells the code that we are to multiply the trial's probability with the % amount provided.


## Logical guide

Suppose that you are wondering what method to insert if you know you are using the second version of the pity system (pity v2 system). Let's go through the process.

```mermaid
graph TB;
    Method-- Not using <br/>pity v1 system -->0
    Method-- Using pity <br/>v1 system -->1
    0-- Not using <br/>reinforcement system -->00
    0-- Using reinforcement <br/>system, after N fails -->N0
    1-- Using reinforcement <br/>system, after N fails -->N1
    1-- Not using <br/>reinforcement system -->01
    00-- Not using any <br/>user behaviour -->000
    N0-- Not using any <br/>user behaviour -->0N0
    N1-- Not using any <br/>user behaviour -->0N1
    01-- Not using any <br/>user behaviour -->001
    00-- Using one of <br/>user behaviours <br/>M : 1,2,3 -->M00
    N0-- Using one of <br/>user behaviours <br/>M : 1,2,3 -->MN0
    N1-- Using one of <br/>user behaviours <br/>M : 1,2,3 -->MN1
    01-- Using one of <br/>user behaviours <br/>M : 1,2,3 -->M01    
    000-->D[_ _000]
    0N0-->D1[_ _0N0]
    0N1-->D2[_ _0N1]
    001-->D3[_ _001]
    M00-->D4[_ _M00]
    MN0-->D5[_ _MN0]
    MN1-->D6[_ _MN1]
    M01-->D7[_ _M01]
    D-- Adding fixed <br/>probability value-->a[% % _ _000]
    D-- Multiply fixed <br/>probability value-->b[% % % _ _000]
    D1-- Adding fixed <br/>probability value-->c[% % _ _0N0]
    D1-- Multiply fixed <br/>probability value-->d[% % % _ _0N0]    
    D2-- Adding fixed <br/>probability value-->e[% % _ _0N1]
    D2-- Multiply fixed <br/>probability value-->f[% % % _ _0N1]    
    D3-- Adding fixed <br/>probability value-->g[% % _ _001]
    D3-- Multiply fixed <br/>probability value-->h[% % % _ _001]   
    D4-- Adding fixed <br/>probability value-->i[% % _ _M00]
    D4-- Multiply fixed <br/>probability value-->j[% % % _ _M00]   
    D5-- Adding fixed <br/>probability value-->k[% % _ _MN0]
    D5-- Multiply fixed <br/>probability value-->l[% % % _ _MN0]    
    D6-- Adding fixed <br/>probability value-->m[% % _ _MN1]
    D6-- Multiply fixed <br/>probability value-->n[% % % _ _MN1]        
    D7-- Adding fixed <br/>probability value-->o[% % _ _M01]
    D7-- Multiply fixed <br/>probability value-->p[% % % _ _M01]        
```



Please note that it is equally valid to simply give the thousandth digit for the method, any digit OTHER than {1,2,3} to avoid using any user behaviours (method classes) such as 4,5,6 etc. 0 was simply an indicator/example used in this presentation.

% signs reflect the **probability value** of the associated probability/factor added to or multiplied to the original probability of the trial. The reason for this design is because we are exploiting the redundancy of triple or above digit probability values as percentages.  Asking the code to add a probability of 1.2 for instance (by using a method as the following 120_ _ & & &) instantly brings the probability of the trial in question, above 1.0. Assuming that you are equally not attempting to run trivial probability values -namely 0.0. You are never going to need to provide something like 100 _ _ & & & as a method. 99 _ _ & & & as a method would suffice for low enough probability values.



### Quick examples

So for eg, if you choose 1003100 as your method, this means that for any fixed trial, if the seed fails more than 3 times, +10% is applied to the trial in question until success is achieved.

In comparison, 11003100, is meant to indicate that the same trial at which this seed has failed, will have its probability multiplied by 1.1 continuously, until success.






