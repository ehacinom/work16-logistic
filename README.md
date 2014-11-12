This is the workspace to deal with our first data set. Real log data to play with from Colin Borys on day 2, 2014-07-08. The file, is called cj_all.csv.gz. The file contains data from a 9 day period in early June 2014 from ORIX Life Insurance, Japan. Conversion is counted as anyone who fills out an online form requesting more information. It contains entries from these two types of logs:

1. standard logs.  Websites visited that had ads.
2. conversion logs. These are from the web server that handles the information form (conversion).

Key columns:
t:		POSIX time (in seconds)
userID:		a unique cookie ID (user).  The file is grouped by user, and sorted in time order for each user.
ConversionTagID: 0 if this is a standard log entry, non zero if they converted 1+ times.
EventTypeID:	1 = ad impression  2 = ad click  3 = search engine result
Site/Placement: IDs of the web sites, and where on the page the ad was placed.
BrowserCode/OSCode: numbers correspond to a lookup table provided here as attachments.

To get file onto local machine:
scp -l 5000 -P 626 mhe@10.1.0.208:/home/cborys/cj_all.csv.gz ./

To browse the data use a subsection of the data:
head -n 500 cj_all.csv > cj_small.csv

On 208, this will generate entryCount.csv that has a list of all users and how many entries they have in the file:
cat cj_all.csv | awk -F',' '{print $2}' | aq_cnt -f,+1 - -d s:userID -kX entryCount.csv key userID


