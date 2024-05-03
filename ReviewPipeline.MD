# The Description of the Backend Pipeline
1. Prepare the textract output.  We have all the results for uploaded register books.
2. Autocheck and prepare the image shown in UI:  
   1. The input is the textract output.  After autochecking，we will have a new csv file. The *only* change is the score, I set the score to 0 for the cell having obvious issues. The page that has less columns will not be reviewed.  Call function **check_csv** in the processss_csv_prepare_pdf_input.py to do the check.
   2. Divide each register page into 3 different parts saving as image in s3 bucket. The rotate direction for each image is saved in a csv file.
   3.  Todo: Need to rewrite the code as a function.
3. Create job 
   1.  The important information is saved in yaml file, such as **id** for the job and the **output path**. Call function **create_job_in_given_folder** in file human_loop.py.
   2.  Todo: finish filtering-related functions. Update GUI.
4. Process the correction results 
   1. Read json output and save them in csv file. Each page will have a corresponding csv file. We can add meta data of the book after this step.  Call function **copy_completed_works** in file process_verified_res.py