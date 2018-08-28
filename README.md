# DRIVER-RATING-AND-ACCIDENT-HOTSPOT-PREDICTION-
1)Firstly ,we have removed all the duplicate records in dataset(bangalore-cas-alerts (1).csv)
2)We have assumed various input data ,which is received from CAS system pre-installed in vehicles as:
devc = 864504031502210
latitude1= 12.987503
longtitude1 = 77.740051 
place = 'Hudi' 
alarmtype = 'Overspeed'
speed = 32
timestamp= '2018-02-01T01:48:59.000Z'
tup=[devc,latitude1,longtitude1,place,alarmtype,speed,timestamp]
3)Then we created dummy columns for device_code_alarm_type and concatenated them to our data frame object.Then we have done some analysis in our data frame.
4)Then we created a new data frame consisting of records that are matched with our real time location.And then we find corresponding distance from current location(lat,long) to each location(lat,long) present in our data set.
Formula for distance calculation;
def function_(lat,long):
    # approximate radius of earth in km
    R = 6373.0

    lat1 = radians(loc[0])
    lon1 = radians(loc[1])
    lat2 = radians(lat)
    lon2 = radians(long)

    dlon = lon2 - lon1
    dlat = lat2 - lat1

    a = sin(dlat / 2)**2 + cos(lat1) * cos(lat2) * sin(dlon / 2)**2
    c = 2 * atan2(sqrt(a), sqrt(1 - a))

    distance = R * c
    return distance



Then stored these values in a new series and concatenated this series to our data frame.
5)And then after sorting this series of data frame ,we fetched all records having distance <= 0.5 kilometer from our present vehicle location and stored these records in a new data frame,And from this data frame we retrieved device code alarm type dummy columns i.e. ['FCW', 'HMW', 'LDWL' ,'LDWR','Overspeed','PCW','UFCW']. Then we created a function to count the number of 1 (denoting alarm raised) and 0 correspondingly, and stored these values in the form of list.
6)Then we are calculating the probability of each type of warning and stored  them in the form of series. and then we mapped the probabilities to nearest distance records present in a data frame.
7)And for giving rating of driver behaviour we are using the following simple logic:

          if (dfx[dfx['Probability']==x]['deviceCode_pyld_alarmType'].iloc[0]==alarmtype) or (dfx[dfx['Distance_from_given_location_in_Km']==ym]['deviceCode_pyld_alarmType'].iloc[0]
          ==alarmtype):
                  rating=1
          elif (df_[0][alarmtype])>=0 and (df_[0][alarmtype])<=10:
                  rating=5
          elif (df_[0][alarmtype])>10 and (df_[0][alarmtype])<=20:
                  rating=4
          elif (df_[0][alarmtype])>20 and (df_[0][alarmtype])<=30:
                  rating=3
          elif (df_[0][alarmtype])>30 and (df_[0][alarmtype])<=40:
                  rating=2
          else:
                  rating=1
  
  
*******************************************************************************************************************************
We have given rating to driver on the basis of the number of alarms raised earlier on those location and we also calculated the accident hotspot by finding all hostspot in 0.5km range of radius.
