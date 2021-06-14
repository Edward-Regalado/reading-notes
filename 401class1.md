## Pain vs. Suffering 
- The price is pain, the pain of growth.
- Pain does not feel good. Duh.
- You'll be punished mentally, having to think your way through problems that you had only even heard about a few hours beforehand.
- You'll have to forge your own path toward a solution.
- You'll have to research for hours on end.
- You'll be punished emotionally, constantly confronted with your own lack of understanding of a topic.
- You'll constantly be having to figure out how to collaborate with new people and deal with their (and your own) emotional quirks.
- You'll constantly be thrust far outside of your comfort zone with the exception that you'll survive for the next push forward.
- You'll constantly be dealing with uncertainty of what awaits you at the end of the 10 weeks. 
- You'll be pushed pyhsically, and while sittin gin a chair and staring at your screen isn't the most strenous exercise in the world, the consecutive hours of it will take its toll.
- You'll lose sleep, you'll forget to work out, and you'll feel exhausted all while being filled with information day after day. 
- All growth comes with some degreee of pain, as it pulls you out of your comfort zone. 
- Do not confuse this with suffering. Suffering is pain without purpose. Pain with no higher goal. Pain with no dreams, no ambition or aspiration.
1. What's your perspective?
2. Why are you doing this?
3. Do you want what comes at the end of this journey?
4. Are you doing this for you?
- Seek remedy and ask questions that bridge the gap between what you know and what you need to be able to do. Research!

## Big O Notation
- Big O notation is used in Computer Science to describe the performance or complexity of an alogrithm, sepcifically it describes the worst-case scenario, and can be used to describe the execution time required or the space used (in memory or on disk) by an alogrithm.
- O(1) desribes an algo that will always execute in the same time (or space) regardless of the size of the input data set.
- O(N) describes an algo whose performance will grow linearly an din direct proportion to the size of the input data set.
- O(N2) represents an algo whose performance is directly proportional to the square of the size of the input data set. This is common wiht algo that involve nested iterations over the data set. Deeper nested iterations will result in O(N3), O(N4), etc.
- O(2^N) denotes an algo whose growth doubles with each addition to the input data set. The growth curve of an O(2^N) function is exponential - starting off very shallow, then rising meteorically.
## Logarithms
- Binary search is a technique used to search sorted data sets. It works by selecting the middle element of the data set, essentially the median, and compares it against a target value. If the values match, it will return success. If the target value is higher than the value of the probe element, it will take the upper half of the data set and perform the same operation against it. The same goes if the target value is lower and goes until it can no longer split the data set.
- O(logN) the iterative halving of data sets described in the binary search example produces a growth curse that peaks at the beginning and slowly flattens otu as the size of the data set increse e.g. an input data set containing 10 items takes one second to complete, a data set containing 100 items takes two seconds, and a data set containing 1,000 items will take three seconds. 
- Doubling the size of the input data set has little effect on its growth as after a single iteration of the alog the data set will be halved and therefor on a par with an input data set half the size.
- This makes algorithms like binary search extremely efficient when dealing with large data sets.