# README
# we create four tables login ,volunteers (who can login post picture and create events) , event ( that created and joinin it by volunteers ) and picture (that can posted by volunteers)
CREATE TABLE LOGIN(
USERID INT PRIMARY KEY,
EMAIL VARCHAR(100) NOT NULL,
PASSWORD VARCHAR(20) NOT NULL);

CREATE TABLE VOLUNTEER(
USERID INT PRIMARY KEY,
USERNAME VARCHAR(100) NOT NULL,
AGE INT NOT NULL,
GENDER CHAR(1) NOT NULL,
FOREIGN KEY (USERID) REFERENCES LOGIN(USERID));

CREATE TABLE EVENT(
USERID INT NOT NULL,
NUMBER INT NOT NULL,
EVENT VARCHAR(200) NOT NULL,
FOREIGN KEY (USERID) REFERENCES VOLUNTEER(USERID));

CREATE TABLE PICTURE(
USERID INT NOT NULL,
NUMBER INT NOT NULL,
PICTURE varbinary(2000),
FOREIGN KEY (USERID) REFERENCES VOLUNTEER(USERID));

# insert the ids and emails and passwords into the login table 
insert into login values(1001, "Fatma.Jamal@gmail.com", "123abcd");
insert into login values(1002, "Sara.Ebrahim@gmail.com", "esbarr6655");
insert into login values(1003, "Mona.Mohammed@gmail.com", "mohMon987");
insert into login values(1004, "Mohammed.Khalid@gmail.com", "mkmk_123");
insert into login values(1005, "Yousef.Ali@gmail.com", "2020Ali");
insert into login values(1006, "Mujbel.AlSahly@gmail.com", "123BBNN");
insert into login values(1007, "Sameer.AlAzmi@gmail.com", "123AASS");
insert into login values(1008, "Mushary.AlHajraf@gmail.com", "444Mushary");
insert into login values(1009, "Salem.Almery@gmail.com", "333Almery");
insert into login values(1010, "Nouf.AlSalem@gmail.com", "222AlSalem");

# insert ids,usernames , age and gender into volunteer table for settinf information
insert into VOLUNTEER values(1001, "Fatma Jamal", 30, "F");
insert into VOLUNTEER values(1002, "Sara Ebrahim", 25, "F");
insert into VOLUNTEER values(1003, "Mona Mohammad", 33, "F");
insert into VOLUNTEER values(1004, "Mohammad Khalid", 40, "M");
insert into VOLUNTEER values(1005, "Yousef Ali", 27, "M");
insert into VOLUNTEER values(1006, "Mujbel alsahly", 45, "M");
insert into VOLUNTEER values(1007, "Sameer Alazmi", 22, "F");
insert into VOLUNTEER values(1008, "Musharry AlHajraf", 29, "M");
insert into VOLUNTEER values(1009, "Salem Almery", 31, "F");
insert into VOLUNTEER values(1010, "Nouf ALSalem", 37, "F");

# insert ids , number of the event and description of the event into table event 
insert into EVENT values(1001, 99001, "New Year Event");
insert into EVENT values(1001, 99002, "NO DESCRIPTION");
insert into EVENT values(1001, 99003, "NO DESCRIPTION");
insert into EVENT values(1004, 99004, "NO DESCRIPTION");
insert into EVENT values(1004, 99005, "NO DESCRIPTION");
insert into EVENT values(1006, 99006, "NO DESCRIPTION");
insert into EVENT values(1006, 99007, "NO DESCRIPTION");
insert into EVENT values(1006, 99008, "NO DESCRIPTION");
insert into EVENT values(1009, 99009, "NO DESCRIPTION");
insert into EVENT values(1010, 99010, "NO DESCRIPTION");

# insert ids, number of the picture and the picture into picture table 
insert into PICTURE values(1001, 887701, "c:\userPhoto\1.jpg");
insert into PICTURE values(1001, 887702, "c:\userPhoto\1.jpg");
insert into PICTURE values(1001, 887703, "c:\userPhoto\1.jpg");
insert into PICTURE values(1004, 887704, "c:\userPhoto\1.jpg");
insert into PICTURE values(1004, 887705, "c:\userPhoto\1.jpg");
insert into PICTURE values(1006, 887706, "c:\userPhoto\1.jpg");
insert into PICTURE values(1006, 887707, "c:\userPhoto\1.jpg");
insert into PICTURE values(1006, 887708, "c:\userPhoto\1.jpg");
insert into PICTURE values(1009, 887709, "c:\userPhoto\1.jpg");
insert into PICTURE values(1010, 887710, "c:\userPhoto\1.jpg");

# delete account 
DELETE FROM LOGIN WHERE USERID = 1003;

# delete picture
DELETE FROM PICTURE WHERE NUMBER <88000;

# delete event
DELETE FROM EVENT WHERE EVENT  LIKE '%KUWAIT%';

# delete account if the age is not accepted
DELETE FROM VOLUNTEER WHERE AGE <=0 OR AGE >=80;

# edit setting information
UPDATE LOGIN 
SET PASSWORD ="KU_201020"
WHERE USERID = 1001;

UPDATE LOGIN 
SET EMAIL="MISHEEL AL-SABAH"
WHERE USERID = 1005;

UPDATE VOLUNTEER
SET USERNAME = "ABOSABAH",
AGE = 49,
GENDER ="M" 
WHERE USERID=1005;

SELECT * 
FROM LOGIN;

# join two table to show the all information in setting page 
SELECT LOGIN.USERID, EMAIL,USERNAME, AGE, GENDER, PASSWORD
FROM LOGIN, VOLUNTEER
WHERE LOGIN.USERID = VOLUNTEER.USERID;

# sort volunteers by their age and gender
SELECT LOGIN.USERID,EMAIL, AGE, GENDER
FROM LOGIN, VOLUNTEER
WHERE LOGIN.USERID = VOLUNTEER.USERID AND AGE >=40;

# show the events that created by female volunteer 
SELECT * 
FROM EVENT
WHERE USERID IN
(SELECT USERID 
FROM VOLUNTEER 
WHERE GENDER ="F");

# count the number of users in application(users+ volunteers)
SELECT COUNT(USERID)
FROM LOGIN;

# show how many users are joind the event
SELECT USERID, COUNT(NUMBER)
FROM EVENT
GROUP BY USERID;

# count the number of volunteers in applicatin
SELECT COUNT(USERID)
FROM VOLUNTEER;

# count how many picture posted by the user 
SELECT USERID, COUNT(NUMBER)
FROM PICTURE
GROUP BY USERID;

# show the avrege age ,maximum and minimum of volunteers in the application
SELECT MAX(AGE), MIN(AGE) , AVG(AGE)
FROM VOLUNTEER; 
