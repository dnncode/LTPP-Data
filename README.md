# LTPP-Data
Processed Long-Term Pavement Performance (LTPP) data 

Title: 	Long-Term Pavement Performance (LTPP) from the Federal Highway Administration under U.S. Department of Transportation 
Authors: 	Mohammadmahdi Hajiha, Xiao Liu
Department of Industrial Engineering, University of Arkansas
Contact: 	xl027@uark.edu, liuxiao314923@gmail.com 
Last update: 	July 6, 2019

R Data: 	Biglist.RData ()
Datalist.RData ()
Description: 
The data are processed from the Long-Term Pavement Performance (LTPP) program---a research project managed by Federal Highway Administration under U.S. Department of Transportation (https://highways.dot.gov/long-term-infrastructure-performance/ltpp/long-term-pavement-performance). The LTPP program started in 1987 as part of the Strategic Highway Research Program (SHRP) and it has been studying the performance of in-service pavements. The goal of the program is to answer how and why pavements perform as they do. The pavement performance data is stored in a database open to other researchers and data analysists and it is available on www.infopave.fhwa.dot.gov. The types of data collected are regraded as the most important factors that affect the pavement performance including traffic, climate, pavement profile, distress, deflection, materials, and drainage system for about 1800 road sections across the U.S. and Canada.  
Each of the variables collected fall into one of the following categories or sub-categories.
1.	Pavement Structure and Construction: 
•	General Section Information (experiment history, GPS location, and construction date)
•	Material - Layer Properties and Field Sampling
•	Pavement Layer Types and Thickness
•	Feature - Drainage, Joints, Shoulder, Reinforcement
•	Maintenance and Rehabilitation (M&R)

2.	Climate (Hourly, Daily, Monthly, Yearly):
•	Precipitation
•	Wind
•	Temperature
•	Humidity
•	Solar 

3.	Highway Performance: 
•	Pavement Distress in Asphalt Concrete (AC)  
•	Surface Characteristics
•	Back Calculation and Deflection

4.	Traffic:
•	Validation Information (Basic Roadway Information)
•	Axle Distribution Statistics
•	LTPP Traffic Analysis Software (LTAS) Data 
•	Equivalent Sigle Axis Loads
•	Annual Weigh-in-Motion (WIM) and Annual Vehicle Class (AVC)

The processed data are saved in two R data objects: Biglist.RData and Datalist.RData
•	Conceptually, the Biglist.RData is constructed in the following way:
Biglist=list()
templist=list()
templist[[1]]=IDsorteddata
templist[[2]]=annual_precipitation
templist[[3]]=annual_humidity
templist[[4]]=annual_wind
templist[[5]]=annual_temp
templist[[6]]=monthly_precipitation
templist[[7]]=monthly_humidity
templist[[8]]=monthly_wind
templist[[9]]=monthly_temp
templist[[10]]=traffic_count
templist[[11]]=airvoids
Biglist[[1]]=templist
* IDsorteddata is sorted first by ID and then by date attribute. It also includes the air-void layer numbers and lat/lon/elevation. The other components of the Biglist are sorted by date attribute.
•	Datalist.RData is a list whose components are individual IDs with are corresponding explanatory variables. Conceptually, this is how the list is generated:

for(i in 1: TOTAL_SECTIONS){
  tempid=unique(datalists[[i]]$ID)

  tempdata[[1]]=datalists[[i]]
  tempdata[[2]]=annual_precipitation[which(annual_precipitation$VWS_ID==tempid),]
  tempdata[[3]]=annual_wind[which(annual_wind$VWS_ID==tempid),]
  tempdata[[4]]=annual_humidity[which(annual_humidity$VWS_ID==tempid),]
  tempdata[[5]]=annual_temp[which(annual_temp$VWS_ID==tempid),]
  tempdata[[6]]=monthly_precipitation[which(monthly_precipitation$VWS_ID==tempid),]
  tempdata[[7]]=monthly_humidity[which(monthly_humidity$VWS_ID==tempid),]
  tempdata[[8]]=monthly_wind[which(monthly_wind$VWS_ID==tempid),]
  tempdata[[9]]=monthly_temp[which(monthly_temp$VWS_ID==tempid),]
  tempdata[[10]]=traffic_count[which(traffic_count$ID==tempid),]
  tempdata[[11]]=airvoids[which(airvoids$ID==tempid),]
 
  Data.list[[i]]= tempdata 
}

•	Remark: The yearly climate data (Precipitation, Wind, Temperature, and Humidity) and the Annual Average Daily Traffic (AADT) as one of the sub-categories of Equivalent Sigle Axis Load are regarded as the environmental variables. The AC Cracking Length and Percentage as one the sub-categories in Pavement Distress in Asphalt Concrete are used as the degradation of the road performance. The selected degradation and the selected environmental variables along with the AADT data are appended to a list whose components (sub-lists) include all the selected data for a particular road section. Hence, the list includes 1806 sub-lists. Each road section is identified with an SHRP code which make it easy to track and filter data for a particular road section. The GPS location for each road section is also available.

•	The data has big gaps and missing values. Hence, for each of the road sections, an intersection of time points for which the selected data is available is taken to get a joint dataset for each road section. For example, there are 52 road sections for which at least 5 data points are available for both the crack percent and AADT. This number is so much smaller when the intersection includes all climate variables. 






