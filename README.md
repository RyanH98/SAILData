# IJCAI 2019 AIMA4EDU Workshop Dataset Documentation 

## I. Overview

This dataset contains data from students using the Squirrel AI Learning system at 2 learning centers in China. Squirrel AI Learning (SAIL) is an AI-based adaptive learning system that delivers afterschool tutoring to K-12 students. It covers a number of academic subjects, including mathematics, English, Physics, and Chemistry.

For this dataset, while students were using SAIL, they were asked to wear a brainwave headset (BrainCo) and to have the webcam camera turned on. Thus, there are 3 main data sources for each student:

1. User records (from Squirrel AI Learning&#39;s learner records store). This contains the question level log (where each row is a question) of student responses in the learning system.
2. Brainwave data (from BrainCo). For each second of wear, this contains the raw EEG values and the derived &quot;attention&quot; values provided by BrainCo. Each row is a second of time.
3. Webcam data (containing relevant features extracted by SRI International)

The data are organized into 4 folders, each is described in more detail in the following sections.

1. [Synced](#ii-synced)
2. [User records](#iii-user-records)
3. [Brainwave](#iv-brainwave)
4. [Webcam](#v-webcam-videos)

## II. Synced

This folder contains the synced results from all three data sources. There are 2 .txt files, one for each school: (1) schooln.txt from students at School N and (2) schoolg.txt from students at school G.

There are 11 columns in each file: the first 7 columns contain information from user records, and the last 4 columns contain the associated brainwave and/or webcam data file paths. The base for synchronization is user records, where the corresponding brainwave and/or webcam data files are appended each question response, whenever there is a match.

Please note: due to difficulties during data collection and with data synchronization, not all user records have corresponding brainwave and webcam data. If the question ctime (the answer submit timestamp of the question) is within the time window of the webcam videos, we assign the corresponding video file path to that question. If the question ctime is in the time window of the brainwave files, we assign the brainwave triplets (attention, EEG, events – more info in Brainwave section) to that question.

The fields/columns are:

1. _Index_: the unique row index, one per row
2. _Subjects_: subject area of study.
  1. &#39;phy&#39; = physics
  2. &#39;en&#39; = English (as a second language)
  3. &#39;en\_reading&quot; = English reading
  4. &#39;math&#39; = mathematics
  5. &#39;chem&#39; = chemistry
  6. &#39;cn&#39; = Chinese (as language arts)
3. _Question\_id_: unique question identifier in SAIL
4. _user\_id_: user identifier, unique for each student
5. _School\_id_: school identifier, unique for each school
  1. schoolg: school\_id = 196
  2. schooln: school\_id = 290
6. _Stime_: timestamp when question appears on the screen (more info in the User Records section)
7. _Ctime_: timestamp when student submits a response (more info in the User Records section)
8. _Video_\__id_: video identifier of the webcam video for the corresponding student (more info in Webcam Video section)
9. _brainwave\_file\_path\_attention_: attention log file path for the corresponding student (more info in Brainwave section)
10. _brainwave\_file\_path\_EEG_: EEG log file path for the corresponding student (more info in Brainwave section)
11. _brainwave\_file\_path\_events_: events log file path for the corresponding student (more info in Brainwave section)

## III. User Records

This folder contains 6 files, one for each of the subject area of study.

Typical flow: Each afterschool tutoring session is approximately 2 hours long. In each session, students focus on a particular set of knowledge points (tag\_code) for a specific course/subject. They typically start with a pretest or review, then view instructional videos and work on learning and practice questions, until the knowledge points have been &quot;mastered&quot;. Pretest questions do not have immediate corrective feedback, but students can view the answer and the explanations of the answer after they completed the pretest. The learning and practice questions contain hints and corrective feedback. Students can activate different levels of hints and view the answer explanation for each question, before or after submitting the response.

After each learning and practice question, SAIL computes and updates each student&#39;s proficiency level on each knowledge point to determine the next question to present. When the proficiency estimates reach a certain threshold, that knowledge point is considered &quot;learned&quot; and will be queued for review at a later time.

The user records contain student response data at the question level.

### 1. math\_record\_cleaned: Mathematics user records

- student\_index
  - indicates different students in math\_record (not real student&#39;s id)
  - there are 114 different students learning math in this dataset
- user\_id
  - user identifier, unique for each student

- school\_index
  - indicates which school those students come from
  - there are 2 schools
  - Schoolg is 1 which equals to school\_id 196
  - Schooln is 2 which equals to school\_id 290
- course\_id
  - indicates which course those students worked on
  - there are 8 different courses in math (e.g. 1206,1252,1253)
  - Each course\_name has a course\_id. For example, 1206 is Grade 8 math (Shanghai Version). Please find more details in column &quot;course\_name&quot;.
- section\_id
  - indicates which section those students worked on
  - there are 55 different sections in math (e.g. 35225,38679)
  - Each section\_id has its corresponding section\_name. For example, 35225 is congruent triangles. Please find more details in column &quot;section\_name&quot;.
- topic\_id
  - indicates which topic those students worked on
  - there are 54 different topics in math (e.g. 10368,22687)
  - Under each section, students work on one topic
- module\_type
  - indicates which part of product those students worked on
  - there are 6 different module\_type in math (1,2,3,5,15,16)
  - 1: pretest
  - 2: if module\_type is 2, there are two kinds of submodule\_type: 1 means High-efficiency learning, 2 means test of learning (still in learning mode)
  - 3: there is one submodule\_type 0 means last test item (still in learning mode)
  - 5: there is one submodule\_type 0 means final or Mid-term test (still in learning mode)
  - 15: there are two submodule\_type 1 and 2. 1 means pre-pretest. 2 means pretest. If the student does not meet the standard, it will skip submodule\_type 2
  - 16: there are two submodule\_type 1 and 2. 1 means pre-learning: study questions about the prerequisites of the corresponding topic. 2 means study question about the corresponding topic.
- submodule\_type
  - indicates sub-parts of the different parts of module\_type
  - there are 3 different submodule\_type in math (0,1,2)
  - Please refer to module\_type
- grandson\_module\_type
  - indicates lower granularity of the different parts of submodule\_type
  - all grandson\_module\_type is 0 in math
- tag\_code
  - indicates which knowledge point those students worked on
  - there are 291 different tag\_codes in math (e.g. &#39;c230205&#39;,&#39;c230208&#39;)
- question\_id
  - indicates which question those students answered
  - there are 2856 different questions in math
- difficulty
  - indicates how difficult each question is. This is a subjective rating by curriculum specialist.
  - 1 (Easiest) to 9 (Hardest)
- right\_answer
  - the expected correct answer for each question
- user\_answer
  - the response/answer provided by the student for each question
- is\_right
  - indicates if the user\_answer is correct
  - 1 = correct; 0 = incorrect
- is\_view\_answer
  - indicates if a student viewed question answer when she worked on that question
  - 1 = yes; 0 = no
- is\_view\_analyze
  - indicates if a student viewed question analysis when she worked on that question
  - 1 = yes; 0 = no
- cost\_time
  - response time; indicates how many seconds the student used to answer each question
  - cost\_time = ctime - stime
  - min cost\_time of math is 1s; max cost\_time is 3556s
- stime
  - indicates when the student receives each question (i.e. the timestamp when the question appears on the screen)
- ctime
  - indicates when each record is created (i.e. when student submits the answer)

### 2. en\_record\_cleaned: English user records

- student\_index
  - indicates different students in en\_record (not real student&#39;s id)
  - there are 85 different students in English product

- user\_id
  - user identifier, unique for each student

- school\_index
  - indicates which school those students come from
  - students come from 2 different schools in English
- course\_id
  - indicates which course those students worked on
  - there are 4 different courses in English product (877,1183,1184,1185)
- section\_id
  - indicates which section those students worked on
  - there are 52 different sections in English (e.g. 33473,33478,33479)
- topic\_id
  - indicates which topic those students worked on
  - there are 156 different sections in English (e.g. 16729,16733,16734)
- module\_type
  - there are 3 different module\_type in English (e.g. 0,2,4)
- tag\_code
  - indicates which knowledge point those students worked on
  - there are 760 different tag\_code in English (e.g. &#39;evyy\_2017tb\_r\_8au5.2&#39;)
- question\_title\_id
  - there are 275 different question\_title\_id in English (e.g. 26788)
- question\_id
  - indicates which question those students answered
  - there are 4919 different questions in English
- question\_type
  - indicates what kind of type each question belong
  - there are 3 different question\_type in English (1,3,8)
- module\_id
  - there are 5 different module\_id in English (0,5,6,7,8)
- difficulty
  - indicates how difficult each question is, as rated subjectively by curriculum specialists
  - 1 (Easiest) to 9 (Hardest)
- right\_answer
  - the expected correct answer for each question
- user\_answer
  - the response/answer provided by the student for each question
- is\_right
  - indicates if the user\_answer is correct
  - 1 = correct; 0 = incorrect; -1 = no answer (cost\_time = 0s)
- cost\_time
  - response time; indicates how many seconds the student used to answer each question
  - cost\_time = ctime - stime
  - min cost\_time of English is 1s; max cost\_time is 16899s
- stime
  - indicates when the student receives each question (i.e. the timestamp when the question appears on the screen)
- ctime
  - indicates when each record is created (i.e. about when student submits the answer)

### 3. cn\_record\_cleaned: Chinese subject user records

- student\_index
  - indicates different students in cn\_record (not real student&#39;s id)
  - there are 68 different students in Chinese product

- user\_id
  - user identifier, unique for each student

- school\_index
  - indicates which school those students come from
  - all students come from school 1 in Chinese

  - Schoolg is 1 which equals to school\_id 196

- course\_id
  - indicates which course those students worked on
  - there are 13 different courses in Chinese product (e.g. 382,690)
- section\_id
  - indicates which section those students worked on
  - there are 49 different sections in Chinese (e.g. 40764,30130)
- topic\_id
  - indicates which topic those students worked on
  - there are 46 different topics in Chinese (e.g. 22203,21233,16593)
- module\_type
  - indicates which part of product those students worked on
  - there are 9 different module\_type in Chinese (e.g. 1,2,3,1001,1002)
- submodule\_type
  - indicates sub-parts of the different parts of module\_type
  - there are 2 different submodule\_type in Chinese (0,1)
- tag\_code
  - indicates which knowledge point those students worked on
  - there are 51 different tag\_codes in Chinese (e.g.&#39;yd4\_15&#39;)
- question\_title\_id
  - all question\_title\_id in Chinese are 0 (0 means there is no question title in this subject)
- question\_id
  - indicates which question those students answered
  - there are 561 different questions in Chinese
- q\_forms
  - there are 2 different q\_forms in Chinese
  - 1 = subjective questions; 2 = objective questions
- difficulty
  - indicates how difficult each question is, as rated subjectively by curriculum specialists
  - 1 (Easiest) to 9 (Hardest)
- right\_answer
  - the expected correct answer for each question
- user\_answer
  - the response/answer provided by the student for each question
- is\_right
  - indicates if the user\_answer is correct
  - 1 = correct; 0 = incorrect; -1 = no answer (cost\_time = 0s)
- is\_view\_answer
  - indicates if a student viewed question answer when she worked on that question
  - 1 = yes; 0 = no
- is\_view\_analyze
  - indicates if a student viewed question analysis when she worked on that question
  - 1 = yes; 0 = no
- cost\_time
  - response time; indicates how many seconds the student used to answer each question
  - cost\_time = ctime - stime
- min cost\_time of Chinese is 1s; max cost\_time is 3015s
- stime
  - indicates when the student receives each question (i.e. the timestamp when the question appears on the screen)
- ctime
  - indicates when each record is created (i.e. about when student submits the answer)

### 4. phy\_record\_cleaned: Physics user records

- student\_index
  - indicates different students in phy\_record (not real student&#39;s id)
  - there are 42 different students in physics product

- user\_id
  - user identifier, unique for each student

- school\_index
  - indicates which school those students come from
  - students come from 2 different schools in physics

  - Schoolg is 1 which equals to school\_id 196
  - Schooln is 2 which equals to school\_id 290

- course\_id
  - indicates which course those students worked on
  - there are 2 different courses in physics (1237,1238)
- section\_id
  - indicates which section those students worked on
  - there are 17 different sections in physics (37971,37972,37973)
- topic\_id
  - indicates which topic those students worked on
  - there are 17 different topics in physics (17616,20427,21505)
- module\_type
  - indicates which part of product those students worked on
  - there are 6 different module\_type in physics
    - 2050 = review
    - 2051 = pretest
    - 2052 = learning &amp; practice 1
    - 2053 = learning &amp; practice 2
    - 2055 = learning &amp; practice 1 (the second time)
    - 2058 = interest learning
- submodule\_type
  - indicates sub-parts of the different parts of module\_type
  - all submodule\_type are 0 in physics
- tag\_code
  - indicates which knowledge point those students worked on
  - there are 119 different tag\_codes in physics (e.g.&#39;wl\_dcx\_dlhdl\_15&#39;)
- question\_id
  - indicates which question those students answered
  - there are 1552 different questions in physics
- difficulty
  - indicates how difficult each question is. This is a subjective rating by curriculum specialist.
  - 1 (Easiest) to 9 (Hardest)
- right\_answer
  - the expected correct answer for each question
- user\_answer
  - the response/answer provided by the student for each question
- is\_right
  - indicates if the user\_answer is correct
  - 1 = correct; 0 = incorrect
- is\_view\_answer
  - indicates if a student viewed question answer when she worked on that question
  - 1 = yes; 0 = no
- is\_view\_analyze
  - indicates if a student viewed question analysis when she worked on that question
  - 1 = yes; 0 = no
- cost\_time
  - response time; indicates how many seconds the student used to answer each question
  - cost\_time = ctime - stime
  - min cost\_time of physics is 1s; max cost\_time is 3452s
- stime
  - indicates when the student receives each question (i.e. the timestamp when the question appears on the screen)
- ctime
  - indicates when each record is created (i.e. when student submits the answer)

### 5. chem\_record\_cleaned: Chemistry user records

- student\_index
  - student identifier in chem\_record (not real student&#39;s id)
  - there are 9 different students in chemistry product

- user\_id
  - user identifier, unique for each student

- school\_index
  - indicates which school those students come from
  - all students come from school 1 in chemistry

  - Schoolg is 1 which equals to school\_id 196

- course\_id
  - indicates which course those students worked on
  - all students worked on course &#39;1263&#39; in chemistry
- section\_id
  - indicates which section those students worked on
  - there are 4 different sections in chemistry (40401,40402,40408,40409)
- topic\_id
  - indicates which topic those students worked on
  - there are 4 different topics in chemistry (21810,22210,22647,22648)
- module\_type
  - indicates which part of product those students worked on
  - there are 6 different module\_type in chemistry
    - 2050 = review
    - 2051 = pretest
    - 2052 = learning &amp; practice 1
    - 2053 = learning &amp; practice 2
    - 2055 = learning &amp; practice 1 (the second time)
    - 2058 = interest learning
- submodule\_type
  - indicates sub-parts of the different parts of module\_type
  - all submodule\_type are 0 in chemistry
- tag\_code
  - indicates which knowledge point those students worked on
  - there are 33 different tag\_codes in chemistry (e.g. &#39;hx\_cz\_ll\_fylx\_04&#39;)
- question\_id
  - indicates which question those students answered
  - there are 531 different questions in chemistry
- difficulty
  - indicates how difficult each question is. This is a subjective rating by curriculum specialist.
  - 1 (Easiest) to 9 (Hardest)
- right\_answer
  - the expected correct answer for each question
- user\_answer
  - the response/answer provided by the student for each question
- is\_right
  - indicates if the user\_answer is correct
  - 1 = correct; 0 = incorrect
- is\_view\_answer
  - indicates if a student viewed question answer when she worked on that question
  - 1 = yes; 0 = no
- is\_view\_analyze
  - indicates if a student viewed question analysis when she worked on that question
  - 1 = yes; 0 = no
- cost\_time
  - response time; indicates how many seconds the student used to answer each question
  - cost\_time = ctime - stime
  - min cost\_time of chemistry is 3s; max cost\_time is 3086s
- stime
  - indicates when the student receives each question (i.e. the timestamp when the question appears on the screen)
- ctime
  - indicates when each record is created (i.e. when student submits the answer)

### 6. en\_reading\_record\_cleaned: English Reading user records

- student\_index
  - indicates different students in en\_reading\_record (not real student&#39;s id)
  - there are 6 different students in English reading product

- user\_id
  - user identifier, unique for each student

- school\_index
  - indicates which school those students come from
  - students come from 2 different schools in English reading

  - Schoolg is 1 which equals to school\_id 196
  - Schooln is 2 which equals to school\_id 290

- course\_id
  - indicates which course those students worked on
  - there are 3 different courses in English reading product (1183,1184,1185)
- section\_id
  - indicates which section those students worked on
  - there are 4 different sections in English reading (33473,33508,33525,33533)
- topic\_id
  - indicates which topic those students worked on
  - all questions in English reading comes from topic 9478
- skill
  - similar to knowledge point (as tag\_code in other subjects)
  - there are 5 different skill in English reading (e.g. &#39;read\_lvl\_en.1&#39;, &#39;read\_lvl\_en.2&#39;)
- detail\_skill
  - similar to sub\_knowledge\_point
  - there are 5 different detail\_skill in English reading (e.g. &#39;Level A&#39;, &#39;Level B&#39;)
- question\_title\_id
  - there are 7 different question\_title\_id in English reading (e.g. 0,6971,10120)
- question\_id
  - indicates which question those students answered
  - there are 80 different questions in English reading
- question\_type
  - indicates what kind of type each question belong
  - there are 2 different question\_type in English reading (1,3)
- difficulty
  - indicates how difficult each question is. This is a subjective rating by curriculum specialist.
  - 1 (Easiest) to 9 (Hardest)
- right\_answer
  - the expected correct answer for each question
- user\_answer
  - the response/answer provided by the student for each question
- is\_right
  - indicates if the user\_answer is correct
  - 1 = correct; 0 = incorrect
- cost\_time
  - response time; indicates how many seconds the student used to answer each question
  - cost\_time = ctime - stime
  - min cost\_time of English reading is 3s; max cost\_time is 4099s
- stime
  - indicates when the student receives each question (i.e. the timestamp when the question appears on the screen)
- ctime
  - indicates when each record is created (i.e. when student submits the answer)

## IV. Brainwave

This folder contains the raw brainwave data from two schools: schoolg and school. Each brainwave session outputs 3 file types: attention, EEG, and events.

* attention

    1. This contains the derived attention value by BrainCo (0-100)
    2. Each row is a Unix timestamp followed by its attention value.
    3. Please convert timestamp to Beijing Time (GMT+8) if you need

* EEG

    1. This contains the raw EEG data from BrainCo
    2. Each row has the timestamp, sequence Num, battery, logging label, and EEG array.
    3. Each point represents the difference in potential between the EEG reference point and the acquisition point. There are 160 such points in a minute for uA.
    4. The vector in square brackets [] are the electrical signal output values of the sensors. These electrical signals can be transformed into frequency domain signals or waveforms (alpha, beta, gamma, etc.) by Fourier transform, and the average energy of each wave band can be calculated. BrainCo&#39;s definition: Alpha: 8-12, LowBeta: 12 -22, HighBeta: 22 -32, Gamma: 32-56
    5. Please convert timestamp to Beijing Time (GMT+8) if you need

* Events

    1. This contains the raw events data from BrainCo
    2. Each point has a Unix timestamp followed by the device stage. It indicates whether the device is connected or not in the corresponding time
    3. Please convert timestamp to Beijing Time (GMT+8) if you need

## V. Webcam Videos

In this folder contains the relevant extracted features from each video captured by the Webcam.

The extracted question segments have two files associated with each segment: a json file with metadata of the question and an npy (python numPy) file containing the tracking metadata which should be very easy to load into Python.

1. Question segments filenames name as &quot;school name\_video ids\_segment numbers.
2. Json file with metadata of the question can be retrieved from user records.
3. File named &quot;npy\_key.md&quot; describing the meanings of the various data point included in the numpy file.

Some statistics about webcam videos segments:

1. Original segments by subject: number of question segments and total video length (in seconds):

{&#39;chem&#39;: [36, 3816.0],
&#39;cn&#39;: [83, 44977.0],
&#39;en\_reading&#39;: [0, 0],
&#39;en&#39;: [680, 79960.0],
&#39;math&#39;: [896, 123495.0],
&#39;phy&#39;: [558, 83004.0]}

2. After further filtering, it contains 2170 segments:

  - Percentage of segments that have at least 50% valid tracking: 61.54%
  - Percentage of segments that have at least 70% valid tracking: 49.88%
  - Percentage of segments that have 100% valid tracking: 18.30%
