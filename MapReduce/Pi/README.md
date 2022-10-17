Description about Pi:

Throw N darts on the board. Each dart lands at a random position (x,y) on the board.

Note if each dart landed inside the circle or not:

            x² + y² < r²
            
            
Take the total number of dart that landed in the circle as S




<img width="750" alt="194803849-7c4c723f-81a1-48ef-b068-12dd25496823" src="https://user-images.githubusercontent.com/68774929/195969471-d959b5c7-c0a5-452a-ba08-880e69a10b24.png">



Design





            Step 1: Generate an input file to the Pi MapReduce program

            Step 2: Create a MapReduce program to calculate the numbers of inside darts and outside darts.

            Step 3: Use the file generated in Step 1.2 as the input to execute the MapReduce program created in Step 2

            Step 4: Calculate Pi in the driver program based on the numbers of inside darts and outside darts.






Implement





GCP environment





![image](https://user-images.githubusercontent.com/68774929/195970095-b7ac4eef-a83c-4aff-9c13-e44f3ab97163.png)






Hadoop environment





![image](https://user-images.githubusercontent.com/68774929/195969525-c5193d0a-57bc-4deb-ab6f-5f8b83b4502f.png)



Java environment



Input data



      $ mkdir PiCalculation

      $ cd PiCalculation

      $ vi GenerateRandomNumbers.java

      $ javac GenerateRandomNumbers.java

      $ java -cp . GenerateRandomNumbers
  
  
  
Make HDFS directory



      $ bin/hdfs dfs -mkdir /user

      $ bin/hdfs dfs -mkdir /user/tbien

      $ bin/hdfs dfs -mkdir /user/tbien/picalculate

      $ bin/hdfs dfs -mkdir /user/tbien/picalculate/input2

      $ bin/hdfs dfs -put ../PiCalculation1/PiCalculationInput /user/tbien/picalculate/input2
  
  

Complile PiCaculation.java


  
      $ bin/hadoop com.sun.tools.javac.Main PiCalculation.java

      $ jar cf wc.jar PiCalculation*class  

  
 Run
 
 
  
      $ bin/hadoop jar wc.jar PiCalculation /user/tbien/picalculate/input /user/tbien/picalculate/output3

  
  
Output


  
      $ bin/hdfs dfs -ls /user/tbien/picalculate/output3

      $ bin/hdfs dfs -cat /user/tbien/picalculate/output3/part-r-00000 


  

Test result




<img width="900" alt="test" src="https://user-images.githubusercontent.com/68774929/196011751-eb0be8bb-f97c-4294-b168-44dc42cb3111.png">


