# QAC-Apprenticeship
This repository includes code and some of the data (can't give more sorry) that I wrote while working as a QAC apprentice under Professor Oleinikov and the Wesleyan Media Project.

More specifically, the goal was to greatly reduce the cost of extracting the displayed text in videos. The idea was that the text that is displayed on the screen will contain most of the ideas of the ad, so taking just that text would already give a pretty good summary of the content of the video. Google provides a service that is VERY good for this, but it costs way too much to be feasible (it would cost thousdands of dollars for the Wesleyan Media Project). 

Thus, there needed to be some way to bring the cost down. The idea Professor Oleinikov and I came up with was to identify key frames in the video that will contain all of the text that occurs in the video. From there, the challenge becaming defining a metric that would separate these key frames from other ones. We ended up settling on corners in the frame, as text had far more corners than any other feature of the advertisements. Calculating the corner count for each frame was quick and efficient, and the key frames were the local maxima. At that point, the key frames could be considered to contain the same amount of information as the entire video. To go even further, the frames were able to be stacked vertically to boil down an entire video to just one image. This simple change of representation allowed Google OCR to be used but at about one hundredth of the price with the same efficacy!

The next part of the project was to take the output of Google OCR and produce the text of the video in chronological order. This process was accomplished by first grouping frames by Levenshtein distance, taking the most sensical phrase from each group (see code for meaning of "sensical"), and then reordering the groups so that the text is output in the order that it occured in the video.

Once implemented, the algorithm was perfect on 50 videos that it was tested on.

#### A few notes on Weeks7_8_Final_Code.ipynb:
- Don't run the part of the notebook that says Not Final Version. It's not the final version
- The first part will take a directory of videos, the directory to which the stacked images will be stored, and where a bookkeeping file will be kept to help with post-processing
- The videos should be mp4 format and have unique names
- There will be a small investment required by a human to take the results of the Google OCR and feed them back to the second part by pointing to where those OCR results are stored
- The second part takes the output from Google OCR as well as the bookkeeping file and produces the text that occured in the video
