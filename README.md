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


### Quick examples

So for eg, if you choose 1003100 as your method, this means that for any fixed trial, if the seed fails more than 3 times, +10% is applied to the trial in question until success is achieved.

In comparison, 11003100, is meant to indicate that the same trial at which this seed has failed, will have its probability multiplied by 1.1 continuously, until success.
