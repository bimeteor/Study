1. passRetained & passUnretained
    passRetained: init from an object and retain it  
    passUnretained: init from an object without retaining it  
    passRetained  
    equel to:  
    passUnretained and retain
2. fromOpaque  
    init from a pointers
3. toOpaque  
    get the pointer
4. takeRetainedValue & takeUnretainedValue  
    takeRetainedValue: get the object assuming that passRetained or retain's called  
    takeUnretainedValue: get the object assuming that passRetained or retain's not called
5. retain & release & autorelease
