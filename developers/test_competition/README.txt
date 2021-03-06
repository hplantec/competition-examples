Test Codalab Competitions
Author: Isabelle Guyon
Date: October 2014 (last revised Oct 2017)
=========================================

This is a small self-contained example to test various aspects of Codalab competitions.
The example includes 2 datasets (ada and arcene). The participants are supposed to train a predictive model on training data for a supervised learning task for which training data is supplied with labels. They are then supposed to use the trained model to make predictions on a validation set (in phase 1) or on a test set (on phase 2) for which the labels are hidden (but available to the scoring program).

WARNINGS: 
- To make this example fast, we included fake data: the data files contain a simple vector, not the real data matrix. The example program making predictions outputs random values and simply uses the input vector to dimension the output.
- Last tested on https://competitions.codalab.org/.

==================================  BASIC ==================================  

Drill #1: Get familiar with the competition bundle
==================================================
Unzip Example_compet_bundle.zip into a directory Example_compet_bundle/
Make some small changes to the files it contains, for example:
- Change the name of the competition in the competition.yaml file (to identify your version). 
- Change the dates to make sure you start in phase 1. 
- Change the icon test.jpg to your own icon.
- Change the contents of some of the html files. 
Rezip the contents of the directory Example_compet_bundle (not the directory itself, just its contents).

Drill #2: Create a competition
==============================
Upload Example_compet_bundle.zip to https://competitions.codalab.org/competitions/create.
Make a note of the competition number NNN (the numbers appearing in the competition URL).
Go to the created competition and check that:
	- you are in phase 1
	- the pages in learn_the_details are all there and in the desired order
	- the phases are all there and in order (at the top of the page, in the phases page, and in the Results page.
Notice that there is a “secret URL” that allows you to share this competition with others without making it publicly available.

Drill #3: Submit results
========================
Go to the submission page http://competitions.codalab.org/competitions/NNN#participate-submit_results
Submit the sample_submission.zip file. Refresh until finished. Check:
Download your submission
View scoring output log
View scoring error log
View detailed results
Download evaluation output from scoring step
Download private output from scoring step
Goto http://competitions.codalab.org/competitions/NNN#results
and check the leaderboard. The leaderboard displays the average rank and the results on set1 and set2. 
Note: The execution time should be 0. We provide a sample submission, which includes both results and code. With the original settings of the YAML file, in phase 1, the code is not executed because “Results Scoring Only” is checked.

Drill #4: Upload competition data
=================================
The datasets of the competition can either be bundled in the competition zip file or uploaded separately to Codalab.
Go to https://competitions.codalab.org/my/datasets/create and create datasets from input_zipped/ada.zip and input_zipped/arcene.zip and call them ada and arcene. Those are of type “input data”.
Then create a meta dataset grouping the two and call it demo_input.

Drill #5: Use the editor
========================
Go to the editor http://competitions.codalab.org/competitions/edit_competition/NNN and uncheck “Results Scoring Only” in phase 1. Now you can submit code. But for code to run, you need input data.
Change “Input data” in phase 1 to demo_input. 
Save your changes (scroll down and click “Submit”).

Drill #6: Check code execution
==============================
Go to the submission page http://competitions.codalab.org/competitions/NNN#participate-submit_results
Submit the sample_submission.zip file again. Refresh until finished and check again the results and the leaderboard. Reminder: the example includes both code and results. Now that “Results Scoring Only” is unchecked, code is executed. The execution time should be about 2 seconds (check the leaderboard).

==================================  ADVANCED ==================================  

Drill #7: Check code migration
==============================
A code submitted in one phase can be submitted automatically (without intervention of the user) to the next phase, if that phase has the “Auto migration” flag checked.
Go to the editor http://competitions.codalab.org/competitions/edit_competition/NNN to change the dates to current dates such that phase 2 starts in 5 minutes (the time of the server is UTC). Wait 5 minutes and watch auto-migration (automatic submission of the last submission of phase 1 to phase 2).
Check again the results and the leaderboard of both phases.
Note 1: The YAML file is set up to execute code in phase 2. However, you can also migrate plain result submissions. For instance: the participants submit in phase 1 results both on validation and test data, but in phase 1, they are scored on validation data only and in phase 2 on test data only.
Note 2: The YAML file is set up to prevent participants to make additional submissions (once auto-migration has occurred): only 1 submission is allowed.

Drill #8: Admin tasks
=====================
Go to:
http://competitions.codalab.org/my/#manage
Under your competition, you can try the buttons:
- Delete: delete this competition.
- Edit: go to the editor. In the editor, under “Admins” more administrators can be added, having the privilege of editing the competition.
- Publish: make the competition public (note, this can be reverted by going to the editor and unchecking “Publicly available”). A published competition cannot be deleted, it should be unpublished first, then click on “Delete”.
- Participants: list of participants. If in the editor “registration required” is checked, the participant must be approved before they can enter the competition. The participants can also be revoked. Mail can be sent to all participants.
- Submissions: A table recapitulating all submissions.

Drill #9: Understanding the scoring program
===========================================
Example_competition_bundle contains a scoring program bundle scoring_program.zip. Unzip this bundle in a directory scoring_program/. The program score.py must be called with 2 arguments: input_dir and output_dir.
Go to scoring_program/ and at the shell prompt type:
python score.py ../../scoring_input/ ../../scoring_output/
Check ../../scoring_output/score.txt: theses are the scores shown on the leaderboard.

In this example, the scoring program computes the MSE between the solution files and the predicted files. The results are displayed as set1 and set2 in the leaderboard, corresponding to the results on the validation data for phase 1 and on the test data for phase 2. The sets are ordered in alphabetical order (set1=ada, set2=arcene). So other datasets may be provided and they will always be called set1 and set1.

In the competition bundle Example_compet_bundle.zip, the reference data (solution files) are given in 2 zip files: ref_valid.zip for phase 1 and ref_test.zip for phase 2. So, even though the scoring program remains the same, the scores computed differ: the scores are computed on validation data in phase 1 and on test data in phase 2.

Note: the leaderboard remains unchanged for both phases.

Drill #10: Understanding the sample code
========================================
Sample code to be submitted in found in sample_submission.zip. Unzip in a directory sample_submission/. The code to generate predictions is called run.py. Usage:
python run.py <input_dir> <output_dir>
Go to the directory sample_submission/ and type at the shell prompt:
python run.py ../sample_input/ .
The program outputs the results of prediction xxx.predict.

Drill #11: Working with starting_kits
=====================================

Edit the competition.yaml and include the field starting_kit on a phase or all of them. The value should be a file within the bundle zip. Example: starting_kit: starting_kit.zip. Upload the competition and ensure under the participate category of a competition view, there is a  Get Starting Kit(s) tab with a table of phases with starting_kits. You should be able to click the download link and be returned a zip file.

Now modify the competition.yaml so that the starting_kit file you defined before, is instead the URI key pointing to the starting_kit you uploaded previously. You should be able to find it in  My Competitions, My Datasets. Re-upload the competition and verify that the competition still grabs the starting_kit correctly.

Drill #12: Competition Dumping
==============================

Goto the view page of a competition you are running, any should do as long as you have the original bundle to compare. Click the dumps button under admin features. If no dumps are existant, click the create dump button. Your page should be refreshed and a table should display with a status and other info on your competition dump. Upon completion you should be able to download the dump. The file structure should be similar to the original.

Compare the original YAML and the new YAML. Notice that the created on may have some !!Python tags. These do not affect the interpretation of the data. You should be able to re-upload this dump zip and get a new competition out of it. Edit the values for testing as you see fit.

Drill #13: Competition Static Assets
====================================

Relative static files may now be uploaded and easily served with a competition. Simply create a directory assets in your competition bundle. Include any files you wish to imbed in your HTML files, such as images.

To actually access these files once the competition is uploaded, simply use the {{ ASSET_BASE_URL }} tag in your html. For example, to serve a file named test.png, reference it in this way:  <img class="img-responsive" src="{{ ASSET_BASE_URL }}/test.png">. The tag will be placed with the correct base url for your competition. Upon uploading your bundle, you should be able to view any images/assets you referenced in this way.

Drill #14: Ingestion program
============================
+ Go to My Competitions>My Datasets>Create Dataset.
+ Upload ingestion_program.zip
+ Choose type: Ingestion program
+ Go back to your test competition and open the editor.
	- In both phases, change the ingestion program to the one you just uploaded.
	- make sure that you have unchecked “result scoring only” (so you are set up for code submission) AND that you have input data (see DRILL 4) — or you can set input data to the same think as in the second phase.
+ Go to Participate>Submit/View results and upload submission4ingestion.zip

This should show you how an ingestion program works. It runs first when a user makes a submission. It has access to the submission of the user and can do whatever it wants with it to produce the predictions. This includes the following scenarios:
- Organizers want to be able to receive a variety of types of submissions, par them and check their validity, then do a bunch of different things; this may include receiving functions or libraries and execute them on various datasets. Users would not need to submit executables. User may also submit data that the organizers use to test code (reverse challenge). Organizers may also run cross-validation experiments (without exposing the truth values).
- Organizers want to feed data little by little to the programs, like for time series predictions, on-line learning, active learning. The submissions can interact with the ingestion program and query data. The ingestion program can even be a data generating process.

There are variants of types of submissions that can be made and ways they are treated:
- no metadata: this is considered a result submission, it is passed directly to the scoring program.
- metadata give an execution command:
command: python $program/run.py $input $output $shared
The submission is exected in parallel to the ingestion program. The submission of the participant and the ingestion program share a directory $shared in which the exchange information.
- metadata gives no execution command:
description: Provides prediction model to be executed by the ingestion program
The submission is passed on the the ingestion program that does whatever it wants with it.




