# FAQs

Welcome to our most frequently asked questions.

## Login Issues / Access

??? question "How do I get access to the Wulver HPC cluster?"
    * If you are a student or researcher, your research/faculty advisor will need to request an account on your behalf. 
    * If you are a faculty member, then you can directly mail us at hpc@njit.edu for an account.
    * For individuals non affiliated with NJIT have to contact a faculty member in NJIT to sponsor you a guest account.
    * If you are taking a course that requires computation on Wulver please ask your course instructor to email hpc@njit.edu to request access for the students.
    * For detail information please click [here](cluster_access.md).

??? question "How do I connect to the Wulver HPC cluster?"
    * You can ssh into Wulver using your UCID and password
    * For detail information please click [here](cluster_access.md).

??? question "Why can’t I log in to the HPC?"
    - There are multiple possible reasons:
        - Ensure that your UCID and password are correct.
        - It’s possible that your account is not activated on Wulver. Make sure to follow the instructions in [How do I get access to the Wulver HPC cluster?]. Once your account is created, you will receive a confirmation in your NJIT email.
        - If you are working off-campus, make sure to connect to NJIT VPN before logging into Wulver. Visit https://ist.njit.edu/vpn for more information on VPN installation.            

??? question "Why is my password not showing in the terminal when I type?"
    - The Command Line Interface hides passwords as you type to protect against visual exposure and enhance security.

??? question "Why am I getting “permission denied” ?"
    - There are multiple possible reasons:
        - You might not have access to the HPC yet. For requesting access, please check our [user access](cluster_access.md).
        - Your instructor/PI have not added you into the group yet.

??? question "Are there data transfer considerations for the HPC cluster?"
    - For transferring  data we recommend using **rsync** or **scp**
    - Detailed instructions are given [here](https://hpc.njit.edu/clusters/cluster_access/#access-to-clusters).

??? question "What security measures should I be aware of when using the HPC cluster?"
    - Do not share your login information with anyone else or allow anyone to login with your account. 

??? question "Which directory I land on when I login ?"
    - You will enter into your home directory named under your UCID.
    - Please note that you are on the login node of Wulver. Do not run any computations on the login nodes, as CPU and memory usage are limited per user on these nodes. To perform computations, you need to request resources from the compute nodes via [SLURM](slurm.md).

## Issues with MobaXterm

!!! note

    - Highly recommended to use the latest version of MobaXterm.


??? question "How do I set up SSH keys in MobaXterm?"
    - You don’t need to set up SSH keys because multi factor factor authentication is enabled via DUO. 

## File Systems / Storage

??? question "I want to know the different file storage systems on Wulver."
    - Please visit our [file system](https://hpc.njit.edu/clusters/Wulver_filesystems/) page for detailed information. 

??? question "How can I get more storage space ?"
    - When your account is active on Wulver, you will have access to following file systems
        - **$HOME** directory - Default quota of 50GB per user and cannot be increased
        - **/project** - Default quota of 2TB per PI group and can be increased upon PI’s request
        - **/scratch** - No quota but files will be deleted after 30 days or sooner if the directory reaches 80% capacity. Users will be notified prior to deletion so they can review and move important files to **/project** if necessary.
    - For more details, visit [file system](https://hpc.njit.edu/clusters/Wulver_filesystems/).

??? question "I have an error disk quota exceeded while running a job, how could I solve this error?"
    - First, check which filesystem is causing the error. If it’s in **$HOME**, it means the 50GB quota has been exceeded. You can either delete files or move them to **/project**. If the error is in /project, you need to delete some files. Alternatively, you can ask your PI to request an increase in the **/project** quota by emailing us at hpc@njit.edu. You can also run your code in **/scratch** and, after the simulation, transfer the important files to **/project**. Use “quota_info” command to check the filesystem quota. 
    - If you are encountering this error while running Python or Jupyter Notebook via Conda, the issue is likely due to Conda packages or cache files stored in $HOME. Use the ```sn p $HOME``` command to view a detailed breakdown of each directory in $HOME, showing how much space it is consuming. If you notice that the .cache directory is consuming a significant amount of space, you should remove it. If the .conda directory is taking up too much space, you need to move the Conda environment to /project. Click [here](https://hpc.njit.edu/Software/programming/python/conda/#importing-to-a-different-location) for detailed steps.

## Jobs and scheduling

??? question "How do I submit and manage jobs on the Wulver HPC cluster?"
    - We use the SLURM resource manager and scheduler on Wulver for submitting and managing jobs on the compute nodes. 
    - Check our [SLURM page](https://hpc.njit.edu/Software/slurm/slurm/) on the website for more detailed guidance.

??? question "How can I monitor the performance of my jobs and the cluster?"
    - For checking the status of your job you can use following commands
    ```bash
    squeue -j [job_id]          #status by job_id
    squeue -u $LOGNAME          #status by user	
    ```
    - For detailed information please visit our [SLURM page](https://hpc.njit.edu/Software/slurm/slurm/)
    - For checking the cluster performance use this [link](https://hpc.njit.edu/Monitor/load.html)


??? question "Where does my output appear after I submit a job ?"
    - Your output will appear in the file which you initialized in your job script which look like below:
    ```
    #SBATCH --output=file_name.%j.out # %j expands to slurm JobID
    ```
    - By default, this file is in the same directory as the job script, unless you specify the working directory via **sbatch**

## Maintenance

??? question "When does maintenance occur ?"
    - Second Tuesday 9AM - 9PM every month

??? question "I submitted my job before maintenance, but why did it go to pending status as *“ReqNodeNotAvail, Reserved for maintenance”*?"
    - If your job walltime request indicates the job will not finish before the maintenance starts then the scheduler will hold the job.  
    - If you resubmit the job with a shorter walltime, it will not be held. 
    - For example: If you submit a job on Monday with a walltime of 2 days and maintenance is scheduled on Tuesday then your job overlaps with the maintenance schedule. Hence, SLURM will immediately put it on hold until the maintenance is completed and start it later.

??? question "How will maintenance affect me ?"
    - During the maintenance downtime, logins will be disabled, users will not have access to their stored data in **/project**, **/home** and **/scratch**.
    - All jobs that do not end before 9AM will be held by the scheduler until the downtime is complete and the systems are returned to service.

??? question "Will I receive a notification before maintenance ?"
    - Please pay attention to the Message of the Day when logging in, as it will serve as a reminder for upcoming downtimes or other crucial cluster-related information.

??? question "What happens to my jobs ?"
    - Jobs queued just before the maintenance will be held in Pending State and then later gets continued.

## Softwares and Hardware Specifications

??? question "Are there any preloaded softwares ?"
    - We have a variety of softwares already installed which can be under ```/apps/easybuild/software/```
    - For more information, please visit our [Software guide](https://hpc.njit.edu/Software/).

??? question "I want to install new softwares ?"
    - Please first check our already installed [software list](https://hpc.njit.edu/Software/#software-list), and if you still don’t find it then visit our [guide](https://hpc.njit.edu/Software/) for detailed guidance on software installation.

??? question "What are the hardware specifications of the Wulver HPC cluster?"
    - Please checkout our [Wulver tab](https://hpc.njit.edu/clusters/wulver/) for details.

??? question "What programming languages are commonly used on the HPC cluster?"
    - It depends on your task and software. You can use any programming language as long as it has capability to parallelise and to be used on multiple cores.
    - Most common ones are C, C++, Fortran, Python, R

??? question "What are the tools and compilers available on HPC cluster?"
    - Common programming tools include Intel and GNU compilers as well as MPI for multi-node jobs. 
    - Details on these resources are available [here](https://hpc.njit.edu/Software/programming/compilers/#intel).

??? question "How can I optimize my code for parallel processing?"
    - We recommend using MPI for making the code parallelised and then specifying the cores.
    - Key areas to consider are CPU optimization, I/O optimization, memory optimization, and parallel optimization. 
    - If you have specific questions about this, please email HPC Help at hpc@njit.edu to request support.

??? question "Can I request additional resources or customization for my projects?"
    - Please see [Wulver Usage and Condo Policy](https://hpc.njit.edu/Policies/wulver_policies/) for resource allocation details. 
    - If you have questions about resource usage or need short term expansion of compute resources, please contact us at hpc@njit.edu. We are always happy to consult with you on how to accelerate your research.

??? question "My software requires a license, how should I proceed?"
    - License is purchased by the user and his/her department.
    - Please visit the software’s documentation for your specific software.

## Miscellaneous

??? question "What documentation and support resources are available for Wulver users?"
    - Please visit the [Education and Training tab](https://hpc.njit.edu/Services/training/) on our website.
    - If you have any specific questions which are not covered, please contact us at hpc@njit.edu


