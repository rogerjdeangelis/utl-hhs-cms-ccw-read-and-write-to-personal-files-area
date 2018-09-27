# utl-hhs-cms-ccw-read-and-write-to-personal-files-area
HHS CCW read and write to personal files area.  

    HHS CCW read and write to personal files area

    https://vrdc.ccwdata.org/

    see github
    https://tinyurl.com/y8ajewdb
    https://github.com/rogerjdeangelis/utl-hhs-cms-ccw-read-and-write-to-personal-files-area

    How to read and write SAS datsets to your personal CCW files area
    instead of userId SL libref

    Steps

      1. Get the location of your files area
      2. Create a folder for your SAS datasets under files
      3. Write and read SAS datasets in thatr folder


    1. Get the location of your files area
    --------------------------------------

       You can use your CCW 'files' area to create folders and subfolders.
       You are not have to be restricted to the userSL space.

       You can read and write SAS datasets to these folders.

       To get the full path to your files folder, just
       drag any sas program from any folder under files into
       the EG editor and run the program

       In your log you will see the path to your files area

       This appears in the log

        %LET _SASPROGRAMFILE='/xxx/xxxx/xxxxx/xxxxxx/files/oto/unx.sas';


    2. Create a folder for your SAS datasets under files
    ----------------------------------------------------

       To create the folder 'sd1' right click on files
       and select 'new folder'.You do not
       get the pop up to name the folder but
       s folder called 'new folder' is created.
       Right click and rename to sd1.
       Now you can create a sas dataset in '...files/sd1'


    3. Write and read SAS datasets in thatr folder
    ----------------------------------------------

       Libname sd1 "'/xxx/xxxx/xxxxx/xxxxxx/files/sd1";
       data sd1.class;
          set sashelp.class;
       run;quit;


       17         Libname sd1 "/xxx/xxxx/xxxxx/xxxxxx/files/sd1";
       NOTE: Libref SD1 was successfully assigned as follows:
             Engine:        V9
             Physical Name: /xxx/xxxx/xxxxx/xxxxxx/files/sd1
       18         data sd1.class;
       19            set sashelp.class;
       20         run;

       NOTE: There were 19 observations read from the data set SASHELP.CLASS.
       NOTE: The data set SD1.CLASS has 19 observations and 5 variables.
       NOTE: Compressing data set SD1.CLASS increased size by 100.00 percent.
             Compressed is 2 pages; un-compressed would require 1 pages.
       NOTE: DATA statement used (Total process time):
             real time           0.00 seconds
             cpu time            0.00 seconds

       20       !     quit;

       What really  nice about this it is fairly easy to leave
       the EG server for the Win 7 VM Classic 64bit SAS workstation and
       share this data.

       This gets you out tof the very restrictive EG Server.

       Useful macro on CCW

       %macro unx(unxcmd);
         filename xeq pipe "&unxcmd";
         data _null_;
           infile xeq;
           input;
           putlog _infile_;
         run;quit;
       %mend unx;

       %unx(ls -l /xxx/xxxx/xxxxx/xxxxxx/files);



