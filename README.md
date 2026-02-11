# kx-insights-enterprise-project
This is an example of a KXI Enterprise project to achieve the official fundamentals certification from KX.

# Overview
In this example of using KXI Enterprise, I opted to generate a dummy feed of AAPL trade data to generate some HLOC interval stats.  There are two reasons for this choice:
1. Simplicity for reproducing this pipeline in anyone's environment
2. Difficult to find good free real-time data online, so just making my own for this proof of concept.

# Deploy
Authenticate and set up your KXI instance on your machine via the steps from the official KX docs, then run the following kxi pm push command to push this package to your environment:

```
rob@sketchPC:~/kx-insights-enterprise-project$ ls -lrt
total 8
-rw-r--r-- 1 rob rob  120 Feb  9 14:07 README.md
drwxr-xr-x 8 rob rob 4096 Feb 10 17:30 equities
rob@sketchPC:~/kx-insights-enterprise-project$ kxi pm push equities
## note: if you have already pushed this version of this package, use the --force option, or iterate the version, whichever makes more sense
```

# Package
The name of the package is called 'equities' -- the package will be the main container for a simple dummy feed of AAPL trade data, along with static data and HLOC analytics.

# Database
The database is called 'equities' and contains 3 tables:
- trade: raw trade data for AAPL.
- static: some static data information for a few securities, including AAPL.
- hloc: High/Low/Open/Close analytics for AAPL.
<img width="1284" height="321" alt="image" src="https://github.com/user-attachments/assets/6a6b4061-31f3-4a51-bb9f-aab7367a4dde" />

# Pipelines
This package contains 2 pipelines:
1. A pipeline called 'equities-rt' to consume and run analytics on raw AAPL trade data.
<img width="2250" height="840" alt="image" src="https://github.com/user-attachments/assets/e5aa027e-c196-405b-945b-dc2d405784f9" />
This pipeline writes the raw data to a kdb insights database, and splits off to utilize a timer window to generate HLOC stats with a 10 second interval.
These HLOC stats are then also written to a kdb insights database as a partitioned table.

3. A simple pipeline called 'static' to generate and write some simple static data to a kdb Insights Database for some securities.
<img width="2227" height="786" alt="image" src="https://github.com/user-attachments/assets/1c38be18-315d-4616-96d4-f2bc57cfea09" />


# Scratchpad
A scratchpad was used to explore the dummy data, and generate a query to generate the HLOC real-time analytic.
<img width="2248" height="1208" alt="image" src="https://github.com/user-attachments/assets/3f18a07a-a606-4e6d-bec0-1d93d46973a8" />

# Views
I utilized the subscriber nodes to generate real-time views of the HLOC data as a candlestick canvas chart, along with some raw trades in a table.
<img width="2251" height="1147" alt="image" src="https://github.com/user-attachments/assets/1d2cffd6-10c6-497c-bd65-77ccb4942b56" />


