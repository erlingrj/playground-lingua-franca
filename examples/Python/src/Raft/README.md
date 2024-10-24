# A reactor-implementation of the Raft consensus algorithm
Raft is a distributed consensus algorithm based on a leader election and log replication.

## Reactors
How do we efficiently use logical time to do this?
- Each node will get a different election timeout and thus send out voteRequests at different logical tags.
- There is this thing where we want to stay at the logical tag until we have received either:
  A. A majority vote
  B. We receive another `voteRequest` with a higher term
  C. ?
How do we do this conveniently with the reactors? 

STA=How long to wait at each tag? => 0, we dont want to wait at all to commit to a tag. (might get problems if we receive on that actually was earlier (then we cancel and go to follower))
STAA=How long will we additionally wait after we have commited to executing that tag.

Now, we probably want to do this with zero-delay cycles and banks? But we should only wait for the majority, how will we do this?

It is actually not that simple. We can of course do this with physical code.


### ZDC with STAA
- We can
