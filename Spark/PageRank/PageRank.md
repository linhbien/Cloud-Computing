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

II. Observation of page rank

A web page does not have input will have:

        Constant PageRank: 1-d
        The smallest PageRank Input Web Pages' impact to the PageRank of a web page:
        The more Input Web Pages the better.
        The higher PageRank of an Input Web Page the better.
        

III. PageRank + PySpark + GCP

Set up PySpark on GCP

        Enable the Google Cloud Compute Engine API
        Create, Configure and Launch a Google Cloud Dataproc cluster








![image](https://user-images.githubusercontent.com/68774929/200699970-e4f07050-0bb0-4b67-b311-bca2cdb1bce8.png)



        Connecting to the Master Node using Secure Shell (ssh)

![image](https://user-images.githubusercontent.com/68774929/200700536-c3c71d2f-27fb-4e92-8dd0-402e34c4f9cc.png)



<img width="161" alt="pagerank" src="https://user-images.githubusercontent.com/68774929/200702987-44b1568e-f8af-43f9-9b46-167f55c7b9f4.png">



    Manually calculate the first 2 iteration of the PageRank
    
        Fỉst iteration A = 1 B = (1/2) = 0.5 C = 1 + (1/2) = 1.5 PageRank (A) = 1 – 0.85 + 0.85 * 1 = 1 PageRank (B) = 1 – 0.85 + 0.85 * 1 = 0.575 PageRank           (C) = 1 – 0.85 + 0.85 * 1.5 = 1.425

        Second iteration A = 1 B = (1/2) = 0.5 C = 0.575 + (1/2) = 1.075 PageRank (A) = 1 – 0.85 + 0.85 * 1.425 = 1.36125 PageRank (B) = 1 – 0.85 + 0.85 *           0.5 = 0.575 PageRank (C) = 1 – 0.85 + 0.85 * 1.075 = 1.06375

    Prepare Data in HDFS
    
    Manual input data
    
    
    Prepare Data in HDFS
    
Manual input data

        vi pagerank_data.txt
        
Data

        A B
        A C
        B C
        C A
        
create a directory (folder) to store the data:

        hdfs dfs -mkdir hdfs:///mydata 
        hdfs dfs -put pagerank_data.txt hdfs:///mydata
        
To verify that the file is indeed located in the mydata folder, run the following command:

        hdfs dfs -ls hdfs:///mydata 
        
Prepare the program

The code is on the above py file.

        vi pagerank.py

Running the program with Pyspark

        spark-submit pagerank.py hdfs:///mydata/pagerank_data.txt 1
        
1 is the iteration count


![image](https://user-images.githubusercontent.com/68774929/200712355-eb2804c2-fbf0-4ab8-891a-f25caedaedda.png)



2nd iteration


![image](https://user-images.githubusercontent.com/68774929/200712633-df07bc20-7da8-4434-b553-ac41e791d197.png)



10 iteration


![image](https://user-images.githubusercontent.com/68774929/200712800-74c380c5-0917-464a-ace9-d69129dfcc1e.png)




IV. PageRank + Scala + GCP


Scala



Install Scala

        $ curl -fL https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-linux.gz | gzip -d > cs && chmod +x cs && ./cs setup
        $ export SCALA_HOME=/usr/local/share/scala 
        $ export PATH=$PATH:$SCALA_HOME/ 



1.Prepare data

Manual input data

        vi pagerank_data.txt
        
Data

        A B
        A C
        B C
        C A
create a directory (folder) to store the data:

        hdfs dfs -mkdir hdfs:///mydata 
        hdfs dfs -put pagerank_data.txt hdfs:///mydata
        
        
To verify that the file is indeed located in the mydata folder, run the following command:

        hdfs dfs -ls hdfs:///mydata 
        
Prepare the program and Runing the program

        spark-shell

1st iteration


![image](https://user-images.githubusercontent.com/68774929/200714474-59a3e0b1-7771-42e9-b8a0-1c66e418be35.png)




2nd iteration


![image](https://user-images.githubusercontent.com/68774929/200714560-eca455f8-9239-404f-9c46-a614234ff0f5.png)






10 iteration

![image](https://user-images.githubusercontent.com/68774929/200714264-4fe450db-86e2-4324-8905-f0a2673040dc.png)
