Run the ipynb file on Colab

Step 1: Study PySpark Collaborative Filtering with ALS

Step 2: Study Colab


Google is quite aggressive in AI research. Over many years, Google developed AI framework called TensorFlow and a development tool called Colaboratory. Today TensorFlow is open-sourced and since 2017, Google made Colaboratory free for public use. Colaboratory is now known as Google Colab or simply Colab.

Another attractive feature that Google offers to the developers is the use of GPU. Colab supports GPU and it is totally free. The reasons for making it free for public could be to make its software a standard in the academics for teaching machine learning and data science. It may also have a long term perspective of building a customer base for Google Cloud APIs which are sold per-use basis.

Irrespective of the reasons, the introduction of Colab has eased the learning and development of machine learning applications.
    
    
    
    
Step 3: Experiment Pyspark code (ipynb) of PySpark Collaborative Filtering with ALS



    1. First upload the data to the running space, then install pyspark in Google Colab
    
    
    
![image](https://user-images.githubusercontent.com/68774929/203478687-676ebc18-d11a-4f0d-ad23-97b12399ccb9.png)




![image](https://user-images.githubusercontent.com/68774929/203478986-9dbe41c1-b595-47f5-8d1c-0669710220d8.png)





![image](https://user-images.githubusercontent.com/68774929/203479568-6b9db717-7830-47f9-9f41-3860d2c9eb20.png)





![image](https://user-images.githubusercontent.com/68774929/203479681-916782bd-1ad8-4cce-989b-ada0ff08a91b.png)





![image](https://user-images.githubusercontent.com/68774929/203479839-55a0467c-e277-4a60-82dc-019201e792cf.png)





![image](https://user-images.githubusercontent.com/68774929/203479940-94b312a3-fa21-42f7-a8b6-5fbca702164e.png)





2. Result



![image](https://user-images.githubusercontent.com/68774929/203480134-4ad81dd6-00bd-4580-ad5d-3867ed160761.png)




3. Save the modified ipynb file as py format



4. Save the modified ipynb file as HTML format which can be used on Step 5 of this project



Run the py file saved on GCP



1.Set up PySpark on GCP


Steps:


    1. Enable the Google Cloud Compute Engine API

    2. Create, Configure and Launch a Google Cloud Dataproc cluster
    
    
    
    
    
![image](https://user-images.githubusercontent.com/68774929/203480838-80a1be22-d068-4072-9826-fc60231ff367.png)





    3. Connecting to the Master Node using Secure Shell (ssh)
    
    
    
2. Prepare Data in HDFS



    movies.csv
    
    rating.csv
    
    tags.csv
    
    recommendation_engine_movielens.py
    
    
    
    1.Upload movies.csv and ratings.csv files at GCP
    
    
    
    
    
    ![image](https://user-images.githubusercontent.com/68774929/203481098-89e808a0-c265-433b-aabe-e7c66e3b3b94.png)
    
    
    
    
    
    2. Create a directory (folder) to store the data:
    
    
        hdfs dfs -mkdir hdfs:///mydata 
        hdfs dfs -put movies.csv hdfs:///mydata
        hdfs dfs -put ratings.csv hdfs:///mydata
        
        
        
        
To verify that the file is indeed located in the mydata folder, run the following command:


        hdfs dfs -ls hdfs:///mydata 
        
        
        
        
        
 ![image](https://user-images.githubusercontent.com/68774929/203481303-6acf91ee-afe5-4fd7-9dc3-1ff841e51306.png)




    3.Prepare the program
    
    
The code is on the above py file. Upload the file to GCP.


        vi recommendation_engine_movielens.py
        
        
        
        
![image](https://user-images.githubusercontent.com/68774929/203481431-89161ff9-960e-463b-9d69-dac32e8817f0.png)




4.Running the program with Pyspark



        spark-submit recommendation_engine_movielens.py
        
        
        
 5. Result
    
    
    
    
   <img width="885" alt="movieresult" src="https://user-images.githubusercontent.com/68774929/204102753-6502f3b5-8493-4204-8fcc-942a48402c17.png">









    
    
    
