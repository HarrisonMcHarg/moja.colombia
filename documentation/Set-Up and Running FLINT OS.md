# Setting up a FLINT RUN and Viewing Outputs

This document describes the steps required to set up the running environment, run FLINT, and access the outputs. Data preparation is described in a separate document. 

## Step 1 – Download the required software

QGIS [https://qgis.org](https://qgis.org/) (Alternatively you can use ArcGIS if you have access to it).

**Windows:** Download QGIS Standalone Installer Version 3.22 (64bit) and follow install instructions.

**Mac (Requires OS X 10.13 and newer):** QGIS macOS Installer Version 3.22 (dmg)

To install QGIS from the DMG, hold CTRL down and select Open on the popup menu.

![image alt text](images/image_0.png)

## Step 2 - Install SQLiteStudio

SQLite studio [https://sqlitestudio.pl/index.rvt](https://sqlitestudio.pl)

## Step 3 – Accessing the code from GitHub

1. Go to [https://github.com/MullionGroup/MAI.Colombia](https://github.com/MullionGroup/MAI.Colombia)

2. You should see a list of files. Above these is a ‘Code’ button. Click this button and select download zip. 

3. Download the zipped code to your computer
   ![image alt text](images/image_1.png)**Windows:** Unzip the folder and move the  ‘MAI.Colombia’ to C:\ (in most cases it would have automatically downloaded to the ‘Downloads’ folder and needs to be moved). 

4. **Mac**: Generally will download to your 'Downloads' folder. Move this to your Desktop by dragging it in a Finder window. Once on    your desktop, double click or right click and use the Archive Utility. This should UnZip it in to the ‘MAI.Colombia’ folder.

5. Rename ‘MAI.Colombia-main’ to ‘MAI.Colombia’
   
   - This will match the file names in the GitHub repository (C:\MAI.Colombia)

![image alt text](images/image_2.png)

6. This step will set up the Run Environment, including the Run Configurations

7. Within the MAI.Colombia/run_envs/data folder
   
   Add the Departamentos_Orinoquia.shp and its associated files and the Forestales_2020_Orinoquia1.shp and associated files

## Step 4 – Setting up Docker

Docker hosts containers, which are like ‘light’ virtual machines that host the FLINT environment.

1. Set up a Docker Account (Docker ID, email & passwords)

2. Go to: [https://hub.docker.com](https://hub.docker.com) and choose 'Sign up for Docker'

3. Verify the email on the account

4. Go to [https://hub.docker.com](https://hub.docker.com); log in, and choose ‘Get started with Docker Desktop’ and download the appropriate installer for your system (Windows or Mac).

5. Once downloaded, Start the Docker Installer
   
    a. **Windows:** double click from downloads **Mac**: drag to Application folder
   
    b. Use Linux containers (Linux containers are the default)
   
    c. Your system will need to restart.

6. Through the start menu, run Docker Desktop
    **Mac**: Open the Docker app: no hyper V or restart required. Once requested enter you Docker login (Step 10)

7. When prompted, Enable Hyper-V and Containers Features by clicking ‘Ok’ –
   
     **This will restart the computer**

![image alt text](images/image_3.png)

8. Through the Start menu, search and open ‘Windows Powershell’

9. When prompted, Allow Access through the firewall so docker can talk to the internet. 
   ![image alt text](images/image_4.png) 

10. Log into Docker with your Docker ID or Email
    
    a. When Docker is running an icon will appear in the Windows Tool
    ![image alt text](images/image_5.png)
    
    b. Open Docker Settings from the toolbar, Select C drive and then select Apply

Note: If you do not have administrative privileges you may not be able to set the permission for docker to access the drive. Ensure you have this access to continue. ![image alt text](images/image_6.png)

11. In the Windows Powershell set up the environment by: **(See step 14 for Mac)**
    
    a. Changing the directory to the one you created by writing: 
    
    ```
    cd C:\MAI.Colombia
    ```
    
    **- Hit enter**
    
    b. Log into docker by;
    
        i. Write:    
        ```
        docker login
        ```
    
    **- Hit enter**
    
        ii. Enter your Username (Docker ID)
    
    **- Hit enter**
    
        iii. Enter your Docker ID password
    
    **- Hit enter** (note, the password doesn’t appear on screen)

![image alt text](images/image_7.png)

![image alt text](images/image_8.png)

12. Still in powershell, pull the container by writing: 
    
    ```
    docker pull mojaglobal/mai.colombia
    ```
    
    **- Hit enter** – Download takes several minutes. 

13. Congratulations! You’ve now set up the FLINT environment – Time to test it!

14. **Mac** In the Mac Terminal set up the environment by:
    
    - Change the directory to the one you created by writing: 
    
    ```
    cd ~/Desktop/MAI.Colombia
    ```
    
    - Still in Terminal, pull the container by writing: 
    
    ```
    docker pull mojaglobal/mai.colombia
    ```
    
    **- Hit enter** – Download takes several minutes. 

15. Congratulations! You’ve now set up the FLINT environment – Time to test it!

## Step 5 – Run FLINT

16. In the PowerShell Window: **(See step 17 for Mac)**
    
    - Write: 
    
    ```
    docker run -ti -v C:\MAI.Colombia:/tmp/moja_runenv mojaglobal/mai.colombia:latest bash
    ```
    
    **- Hit Enter** 
    
    - This runs a shell within the container  
    - Change the directory
    - Write
    
    ```
    cd /tmp/moja_runenv
    ```
    
    - If you want to see the files in the container, you can write* ls* to list them.
    
    - Write: 
    
    ```
    moja.cli --config growth_mai.json --config growth_mai_libs.json --config_provider growth_mai_provider.json
    ```
    
    **- Hit Enter**
    
    b. Note: this will take some time (10-20 minutes). 

17. **Mac** In the Terminal Window, still in ~/Desktop/moja.MAI.Colombia/run_env:
    
    - Write: 
      
      ```
      docker run --remove  --rm -ti -v ~/Desktop/MAI.Colombia/run_env:/tmp/moja_runenv mojaglobal/mai.colombia:latest bash
      ```
      
      **- Hit Enter**
      
      This runs a shell within the container. 
    
    - Change the directory
    
    - Write:
    
    ```
    cd /tmp/moja_runenv
    ```
    
    **- Hit Enter**
    
    - If you want to see the files in the container, you can write* ls* to list them.

18. Write: 
    
    ```
    moja.cli --config  growth_mai.json --config growth_mai_libs.json --config_provider growth_mai_provider.json
    ```
    
    **- Hit Enter**
    
    Note: this will take some time (10-20 minutes). 

![image alt text](images/image_9.png)

19. Congratulations! You’re running the FLINT!
    
    a. Note: it will not let you enter anything until the run is complete.
    
    b. Once the FLINT has run, an Output folder will appear in the Data folder you created (under MAI.Colombia, and include spatial and database outputs

## Step 6 – View Output data

20. This step shows you the commands needed to build a single raster for each output or time step of each output. We have used forestStemCM as the illustrative example. You should already be within the FLINT docker shell.  Write:
    
    ```
    python3 merge_geotiffs.py
    ```
    
    **- Hit Enter**
    
    This will produce the following outputs 

<table>
  <tr>
   <th>Output</th>
    </tr>
  <tr>
    <td>atmosphereCM</td>
    </tr>
  <tr>
    <td>aboveGroundCM</td>
    </tr>
  <tr>
    <td>belowGroundCM</td>
   </tr>
 </table>

22. Open QGIS
    
    a. When you use QGIS for the first time open; QGIS Desktop
    
    b. Open the virtual raster (.vrt) from `C:\MAI.Colombia` 
    **Mac:** `~/Desktop/MAI.Colombia`
    
        i. Select the drop down menu under *C:\ **(Mac: Home)*
        ii. Select the folder* C:\MAI.Colombia*
        iii. Select *forestStemCM_12.vrt*
    
    c. This will show you the Spatial outputs form the Run![image alt text](images/image_10.png)![image alt text](images/image_11.png)

![image alt text](images/image_12.png)

![image alt text](images/image_13.png)

23. To view the Database Output:
    
    a. Open SQLite studio
    
        i.  open the database outputs
        
            - Select add database
        
            - Select add folder
        
        ii. `C:\MAI.Colombia\run_envs\data\output\results\dbs`
    
    **Mac:** `~/Desktop/MAI.Colombia/run_envs/data/output/results/dbs`

![image alt text](images/image_14.png)![image alt text](images/image_15.png)

![image alt text](images/image_16.png)

24. Open Query

![image alt text](images/image_17.png)

25. Write:
    
    ```
    SELECT D.year, 
       Ps.NAME          AS SrcPool, 
       Pd.NAME          AS SinkPool, 
       Sum(F.flux)      flux, 
       Sum(F.itemcount) FluxAggCount, 
       L.unitcount, 
       L.unitareasum 
    FROM   flux_reporting_results AS F 
       INNER JOIN date_dimension AS D 
               ON D.date_dimension_id_pk = F.date_dimension_id_fk 
       INNER JOIN poolinfo_dimension AS Ps 
               ON F.source_poolinfo_dimension_id_fk = 
                  Ps.poolinfo_dimension_id_pk 
       INNER JOIN poolinfo_dimension AS Pd 
               ON F.sink_poolinfo_dimension_id_fk = Pd.poolinfo_dimension_id_pk 
       INNER JOIN locationnontemp_dimension AS L 
               ON L.locationnontemp_dimension_id_pk = F.location_dimension_id_fk 
    GROUP  BY D.year, 
          Ps.NAME, 
          Pd.NAME 
    ORDER  BY D.year, 
          Ps.NAME, 
          Pd.NAME 
    ```

26. Execute Query

![image alt text](images/image_18.png)

26. Export Results as json to clipboard, paste into Excel. 

![image alt text](images/image_19.png)

## Step 7 - Edit Config

Open  config from `C:\MAI.Colombia\run_env` using Notpad++

![image alt text](images/image_20.png)

2. Determine the block index that will be analized → Modify the block_index area interest and tile_index

"Tile_index": “type the value of tile index where block index located

"block_index": *“type the value of block index”*

![image alt text](images/image_21.png)

3. after Run, go to step 5.  

# `
