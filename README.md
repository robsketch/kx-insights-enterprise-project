# KX Insights Enterprise Project
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
- static: some historical OHLC data saved as a splayed table.
- hloc: High/Low/Open/Close analytics for AAPL.
<img width="1115" height="302" alt="image" src="https://github.com/user-attachments/assets/72c83b96-469b-418a-9fdf-386c87dd163d" />

# Pipelines
This package contains 2 pipelines:
1. A pipeline called 'equities-rt' to consume and run analytics on raw AAPL trade data.
<img width="2250" height="840" alt="image" src="https://github.com/user-attachments/assets/e5aa027e-c196-405b-945b-dc2d405784f9" />
This pipeline writes the raw data to a kdb insights database, and splits off to utilize a timer window to generate HLOC stats with a 10 second interval.
These HLOC stats are then also written to a kdb insights database as a partitioned table.

2. A simple pipeline called 'static' to generate read historical OHCL data from KX's industry example. I adjusted the data via map to make some dummy data for AAPL.
<img width="1392" height="780" alt="image" src="https://github.com/user-attachments/assets/ffdb85c3-f9a9-4819-9452-df071925d0d3" />


# Scratchpad
A scratchpad was used to explore the dummy data, and generate a query to generate the HLOC real-time analytic.
<img width="2248" height="1208" alt="image" src="https://github.com/user-attachments/assets/3f18a07a-a606-4e6d-bec0-1d93d46973a8" />

# Views
I utilized the subscriber nodes to generate real-time views of the HLOC data as a candlestick canvas chart, along with some raw trades in a table.
<img width="2242" height="1206" alt="image" src="https://github.com/user-attachments/assets/65bf5353-7c9c-49a4-aceb-40bd5f361093" />



