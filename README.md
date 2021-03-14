# ETL with Luigi

Imagine we have a project that gathering the data from particular platform (currently, we are using zomato) and store them into our database system (PostgreSQL) with a clean format for doing an analysis. Our goal is want to extract all raw data from scrapping method and doing several transformation like cleaning the data and feature extraction for better understanding in future analysis by building our pipelines. So, our data scientist easy to analyze the data.

![alt text](https://miro.medium.com/max/2000/1*fU3HV_CBmvO6XPJIhb0vkA.png)

## Luigi overview

Luigi is an execution framework that allows you to write data pipelines in Python. This workflow engine supports tasks dependencies and includes a central scheduler that provides a detailed library for helpers to build data pipes in PostgreSQL, MySQL, AWS, and Hadoop. Not only is it easy to depend on the tasks defined in its repos, you can easily fork execution paths and use output of one task as the input of the second task. This framework was written by Spotify and became open source in 2012. Many popular companies such as Stripe, Foursquare, and Asana use this Luigi workflow engine.

![alt text](https://miro.medium.com/max/2000/1*fU3HV_CBmvO6XPJIhb0vkA.png)

### Prerequisites

I recommend that you install Luigi in any particular environment. For this case, i use my ‘bigdata’ environment. 

![alt text](https://miro.medium.com/max/1400/1*VnBI4YtgXPsOdlt1d6vkbw.png)

So, activate your environment first. Here, we go, Since Luigi is written in Python, you just install it using pip:

```
pip install luigi
```

## Running the tests

As we build before that the dependencies Task between Transform and Load. So, we need to execute first Task that store the raw data into our local PostgreSQL. Go to your pipelines file directory, then activate your environment and follow this command :

First, commmand!

```
PYTHONPATH='.' luigi --module luigitutorial extract_data
```

If you are successful run first command, you will get response from terminal like this:

```
DEBUG: Checking if extract_data() is complete
INFO: Informed scheduler that task   extract_data__99914b932b   has status   PENDING
INFO: Done scheduling tasks
INFO: Running Worker with 1 processes
DEBUG: Asking scheduler for work...
DEBUG: Pending tasks: 1
INFO: [pid 18294] Worker Worker(salt=845978677, workers=1, host=MacBooks-MacBook-Pro.local, username=macbookpro, pid=18294) running   extract_data()
INFO: [pid 18294] Worker Worker(salt=845978677, workers=1, host=MacBooks-MacBook-Pro.local, username=macbookpro, pid=18294) done      extract_data()
DEBUG: 1 running tasks, waiting for next task to finish
INFO: Informed scheduler that task   extract_data__99914b932b   has status   DONE
DEBUG: Asking scheduler for work...
DEBUG: Done
DEBUG: There are no more tasks to run at this time
INFO: Worker Worker(salt=845978677, workers=1, host=MacBooks-MacBook-Pro.local, username=macbookpro, pid=18294) was stopped. Shutting down Keep-Alive thread
INFO:
===== Luigi Execution Summary =====
Scheduled 1 tasks of which:
* 1 ran successfully:
- 1 extract_data()
This progress looks :) because there were no failed tasks or missing dependencies
===== Luigi Execution Summary =====
```
Second, commmand!

```
PYTHONPATH='.' luigi --module luigitutorial load_data
```

If you are successful run second command, you will get response from terminal like this:

```
DEBUG: Checking if load_data() is complete
DEBUG: Checking if transform_data() is complete
INFO: Informed scheduler that task   load_data__99914b932b   has status   PENDING
INFO: Informed scheduler that task   transform_data__99914b932b   has status   DONE
INFO: Done scheduling tasks
INFO: Running Worker with 1 processes
DEBUG: Asking scheduler for work...
DEBUG: Pending tasks: 1
INFO: [pid 18324] Worker Worker(salt=315842906, workers=1, host=MacBooks-MacBook-Pro.local, username=macbookpro, pid=18324) running   load_data()
INFO: [pid 18324] Worker Worker(salt=315842906, workers=1, host=MacBooks-MacBook-Pro.local, username=macbookpro, pid=18324) done      load_data()
DEBUG: 1 running tasks, waiting for next task to finish
INFO: Informed scheduler that task   load_data__99914b932b   has status   DONE
DEBUG: Asking scheduler for work...
DEBUG: Done
DEBUG: There are no more tasks to run at this time
INFO: Worker Worker(salt=315842906, workers=1, host=MacBooks-MacBook-Pro.local, username=macbookpro, pid=18324) was stopped. Shutting down Keep-Alive thread
INFO:
===== Luigi Execution Summary =====
Scheduled 2 tasks of which:
* 1 complete ones were encountered:
- 1 transform_data()
* 1 ran successfully:
- 1 load_data()
This progress looks :) because there were no failed tasks or missing dependencies
===== Luigi Execution Summary =====
```

As we can see above that dependencies task already executed!

![alt text](https://miro.medium.com/max/2000/1*iMrvAQ-xm2PYRvq9vdQKNA.png)

## Objective

The purpose of this project is to explore the use of orchestration tools which are implemented on the ETL concept. If you are facing and error, please contact me on email mulianaraul@gmail.com . 


