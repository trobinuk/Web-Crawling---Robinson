# Web-Crawling-Robinson
Web Crawling Assesment

Step 1 : Downloading from the webpage warc.paths.gz, wet.paths.gz, etc (I should have used aiohttp library)

Step 2 : Extracting the file and puttting into a folder using gzip.open and shutil.copyfileobj

  This file containts n number of links that will lead into another downloadable .gz file
  Each link will download one .gz file
  I used for loop to read line one by one
  
Step 3 : Read the Link from the text document and insert each downloaded file into a separate folder (third step)
      Each of the file contains the n number of links from which we have to read the text fand check
      But again this files are in .gz extension if we extract we will get .warc extension

Step 4 : Extract the .gz file (from step 3) and this will give us .warc file

Step 5 : Getting the URL links from the .warc file one by one using the for loop

Step 6 : ArchiveIterator, urllib Request, urllib urlopen to iterate through the link one by one 
        Copy the contents and store it in a string 
        Check whether the covid and economics keyword are present in the content of the webpage
          Top -> If both the keyword "covid" and "economics" are present in the content
          Medium -> if atleast one of the keyword is present in the content
          low -> if none of the keyword are present in the content
          Error -> If fail to read the link
        And insert the link into the .xlsx file
        
 Step 7 : Use Threading so that the step1 can run in paralled to step 2
        
Problems Faced:

1. While reading the link my computer anti-virus has blocked many of the sites which made the execution slow.
2. Threading should have done more effectively by me (Like mentioned in the document downloading and reading in parallel) but it is a series of operation So I couldn't figure that out within time
3. I should have also used aiohttp library 
4. Instead of .xlsx file I tried inserting into Oracle DB it worked well but very slow 
        username = 'c##robin'
        password = 'robin'
        dsn = 'localhost/orcl'
        port = 1521
        encoding = 'UTF-8'

        import cx_Oracle
            import config_orcl as cfg

        sql = ('insert into url_link_from_python(link_url, priority) '
                                   'values(:lv_url,:priority)')
                            try:
                                with cx_Oracle.connect(cfg.username,
                                                       cfg.password,
                                                       cfg.dsn,
                                                       encoding=cfg.encoding) as connection:
                                    with connection.cursor() as cursor:
                                        cursor.execute(sql, [lv_url, priority])
                                        connection.commit()
                            except cx_Oracle.Error as error:
                                print('Error occurred:')
                                print(error)
