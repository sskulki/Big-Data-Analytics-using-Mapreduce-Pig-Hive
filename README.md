# Big-Data-Analytics-using-Mapreduce-Pig-Hive

SQL Commands:
MySql Database: use Test;
Create table:
create table NCHS_DATA (ID int, Year varchar(255), Cause_of_Death varchar(255), State varchar(255),State_Code varchar(255),Region_code varchar(255),Age_Range varchar(255),Locality varchar(255),Observed_Deaths varchar(255),Population varchar(255),Expected_Deaths varchar(255),Potentially_Excess_Deaths varchar(255),Percent_Potentially_Excess_Deaths varchar(255));

#2nd Dtataset
create table NCHS_Cost_Data (Cancer_Type varchar(255), Year varchar(255),Sex varchar(255),Age varchar(255), Annual_Cost_Increase varchar(255),Total_Costs varchar(255), Initial_Year_After_Diagnosis_Cost varchar(255), Continuing_Phase_Cost varchar(255), Last_Year_Life_Cost varchar(255));

Load data  from CSV to MySql:
load data local infile '/home/shridhar/Downloads/NCHS_UPDATED_DATA.csv' into table NCHS_Stats fields terminated by ',' lines terminated by '\n';
load data local infile '/home/shridhar/Downloads/DowloadableDataFull.csv' into table NCHS_Cost_Data fields terminated by ',' lines terminated by '\n';

Load data from MySql to hdfs:
sqoop import --connect jdbc:mysql://127.0.0.1/Test --username root --password 1234 --table NCHS_Stats --target-dir /sqoop/NCHS_Stats -m 1;
sqoop import --connect jdbc:mysql://127.0.0.1/Test --username root --password 1234 --table NCHS_Stats --target-dir /sqoop/NCHS_cost -m 1;

MapReduce Environments:
Scripts are attached separately.
1.	Java -> Mapreduce 1, mapreduce 2, mapreduce3, init program is master program
2.	Pig -> Pig_program.pig
3.	Hive -> Hive_program.sql
4.	
Hadoop File System Access:
Hadoop fs -ls pdafinal/
Load data from hdfs to MySql:
sqoop export --connect jdbc:mysql://127.0.0.1/Test --username root --password 1234 --table res --export-dir /pdafinal/res/ --input-fields-terminated-by '/t';

Export data in CSV from MySql:
SELECT * FROM case1output INTO OUTFILE "/home/hduser/Desktop/PDA_Project/pdaoutput/Outputfile.csv" FIELDS TERMINATED BY ',’ ENCLOSED BY '"' LINES TERMINATED BY '\n’;

Commands to run hive and pig scripts respectively:
hive -f case3script.sql

pig -x local case4script.pig > pigout.csv

