# Upgrading CiviCRM-Standalone

A guide to upgrading CiviCRM-Standalone to a newer release.

Python2 code: [civicrm_upgrade](/code/civicrm_upgrade)

## Introduction

There is a new release of CiviCRM-Standalone about once a month. Checking for a new release and downloading it may be done at [CiviCRM Download](https://civicrm.org/download)

The updating of CiviCRM-Standalone is not automated and must be performed manually using bash commands. Note that CiviCRM does support automated updates of its *extensions*. E.g. *Mosaico*.

### Summary of Steps involved in Upgradeing CIviCRM-Standalone

* Backup the CiviCRM database
* Backup CiviCRM files
* Create a temporary upgrading directory. civicrm_temp
* Download the latest version of CIviCRm-Standalone. Use wget to civicrm_temp
* 


## Database backup

https://gemini.google.com/u/1/app/dd7bdff5ee69e885?utm_source=app_launcher&utm_medium=owned&utm_campaign=base_all

use python 2.7 subprocess to execute a mysqldump command

Executing a mysqldump command using Python 2.7’s subprocess module requires a bit of care, especially when it comes to handling passwords and capturing the output securely.

In Python 2.7, the recommended approach for running a command and capturing its output is using subprocess.Popen.

Here is a clean, robust script to handle this.

```python

import subprocess
import os

def run_mysqldump(host, user, password, database, output_file):
    # 1. Define the command as a list of arguments
    # Note: We do NOT put the password directly after -p here to avoid syntax issues.
    # Instead, we will pass it securely via the environment.
    cmd = [
        'mysqldump',
        '-h', host,
        '-u', user,
        '-p',  # The password will be prompted, but we inject it via MYSQL_PWD
        database
    ]
    
    # 2. Securely pass the password using the MYSQL_PWD environment variable.
    # This prevents the password from showing up in the system's process list (ps aux).
    env = os.environ.copy()
    env['MYSQL_PWD'] = password

    try:
        # 3. Open the output file where the dump will be written
        with open(output_file, 'wb') as f:
            # Execute the command
            process = subprocess.Popen(
                cmd, 
                stdout=f,                # Redirect stdout directly to the file
                stderr=subprocess.PIPE,  # Capture errors separately
                env=env                  # Pass the environment with the password
            )
            
            # Wait for the command to finish and get stderr
            _, stderr_output = process.communicate()
            
            if process.returncode == 0:
                print "Backup successfully created: {}".format(output_file)
            else:
                print "mysqldump failed with exit code: {}".format(process.returncode)
                print "Error: {}".format(stderr_output)
                
    except OSError as e:
        print "Failed to execute mysqldump. Is it installed and in your PATH?"
        print "Details: {}".format(e)
    except Exception as e:
        print "An error occurred: {}".format(e)

# --- Example Usage ---
if __name__ == "__main__":
    DB_HOST = "localhost"
    DB_USER = "root"
    DB_PASS = "your_secure_password"
    DB_NAME = "my_database"
    OUTPUT_PATH = "backup.sql"
```

Key Python 2.7 & Security Considerations

* The MYSQL_PWD Environment Variable: Passing the password directly in the command string (like ['-pyour_password']) is a security risk. On Linux/Unix systems, any user running ps aux would be able to see your database password plain as day. Using env['MYSQL_PWD'] keeps it hidden from the process list.

* Avoid shell=True: Keeping shell=False (the default) avoids invoking the system shell, shielding your script from potential shell injection vulnerabilities.

* File Handling ('wb'): In Python 2.7, writing the file in binary mode ('wb') ensures that line endings (\n vs \r\n) aren't unintentionally altered by the OS, preserving the exact SQL format.

* No subprocess.run: If you are looking at modern Python examples, you'll see subprocess.run. Keep in mind that this was introduced in Python 3.5. For Python 2.7, subprocess.Popen combined with .communicate() is the standard, reliable way to manage process I/O.

  
