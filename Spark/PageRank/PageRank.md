PageRank


1. Introduction




<img width="326" alt="199075533-ecaf0d4d-45d7-4133-b285-05b0efca2edb" src="https://user-images.githubusercontent.com/68774929/199285933-9cbb8fe5-ef22-49e6-870a-07228251b4b0.png">






1. If The initial PageRank value for each webpage is 1.

    PR(A) = 1
    
    PR(B) = 1
    
    PR(C) = 1
    
    Page B has a link to pages C and A
    
    Page C has a link to page A
    
    Page D has links to all three pages
  

2. Then

  A's PageRank is: PR(A) = (1-d) + d * (PR(B) / 2 + PR(C) / 1 + PR(D) / 3)
  B's PageRank is: PR(B) = (1-d) + d * (PR(D) / 3)
  C's PageRank is: PR(C) = (1-d) + d * (PR(B) / 2 + PR(D) / 3)
  D's PageRank is: PR(D) = 1-d
  Damping factor is 0.85
  

3. Then after 1st iteration

  Page B would transfer half of its existing value, or 0.5, to page A and the other half, or 0.5, to page C.
  Page C would transfer all of its existing value, 1, to the only page it links to, A.
  Since D had three outbound links, it would transfer one third of its existing value, or approximately 0.33, to A.
  PR(A)= (1-d) + d * (PR(B) / 2 + PR(C) / 1 + PR(D) / 3) = (1-0.85) + 0.85 * (0.5 + 1 + 0.33) = 1.71
  PR(B)= (1-d) + d * (PR(D) / 3)= (1-0.85) + 0.85 * 0.33 = 0.43
  PR(C)= (1-d) + d * (PR(B) / 2 + PR(D) / 3)= (1-0.85) + 0.85 * (0.5 + 0.33)= 0.86
  PR(D)= 1-d= 0.15
  
4. You can keep iterate
....
