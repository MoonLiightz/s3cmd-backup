# Simple s3cmd backup script
This is a simple script that compresses a specified folder and loads it into an aws s3 bucket using s3cmd.


## Getting Started

### Prerequisites 

* __Unix__-like operating system
* __s3cmd__ is a command line tool that makes it possible to put/get files into/from a s3 bucket. Please make sure that s3cmd is installed and configured. 
Check the s3cmd installation guide [here](https://github.com/s3tools/s3cmd/blob/master/INSTALL) and run `s3cmd --configure` after installation.
* __zip__ or __tar__ should be installed
* A configured __aws s3 bucket__


### Installation

#### via curl
```bash
$ curl -Lo backup https://git.io/fhMJy
```

#### via wget
```bash
$ wget -O backup https://git.io/fhMJy
```

#### via httpie
```bash
$ http -do backup https://git.io/fhMJy
```

#### via git clone
```bash
$ git clone https://github.com/MoonLiightz/s3cmd-backup.git
$ cd s3cmd-backup
```

#### Note
Don't forget to give the script execution permissions.

```bash
$ chmod +x backup
```


### Configuration
To configure the script, edit the downloaded file with an editor of your choice like `nano` or something else. At the top of the file you will find some configuration options.

| Config Option      | Description |
| ------------------ | ----------- |
| BACKUP_PATH        | Path to the location without ending `/` of the folder which should be saved. <br>__Example:__ If you want to save the folder `myData` located in `/root` than you should set `BACKUP_PATH="/root"` |
| BACKUP_FOLDER      | Name of the folder which should be saved. <br>__Example:__ Based on the previous example you should set `BACKUP_FOLDER="myData"` |
| BACKUP_NAME        | Name of the backup file. The date on which the backup was created is automatically appended to the name. <br>__Example:__ If you set `BACKUP_NAME="myData-backup"` the full name of the backup is `myData-backup_year-month-day_hour-minute-second` |
| S3_BUCKET_NAME     | Name of the s3 bucket where the backups will be stored. <br>__Important:__ The name of the bucket and not the `Bucket-ARN` <br>__Example:__ `S3_BUCKET_NAME="mybucket"` |
| S3_BUCKET_PATH     | Path in the s3 bucket without ending `/` where the backups will be stored. <br>__Example:__ `S3_BUCKET_PATH="/backups"` |
| COMPRESSION        | The compression which will be used. Available are `zip` and `tar` <br>__Example:__ For `zip` set `COMPRESSION="zip"` and for `tar` set `COMPRESSION="tar"` |
| TMP_PATH           | Path to a location where files can be temporarily stored. The path must exist. <br>__Example:__ `TMP_PATH="/tmp"` |


## Usage

### Basic
The script supports the following functionalities.

#### Create Backup
This command creates a backup and loads it into the specified s3 bucket.

```bash
$ ./backup create
```

#### List Backups
With this command you can list the backups stored in the s3 bucket.

```bash
$ ./backup list
```

#### Download Backup
To download a backup from the s3 bucket to the server you can use this command.

```bash
$ ./backup download <filename>
```

### Cron
You can also execute the script with a cronjob. The following example creates a backup every night at 2 a.m. 

```bash
0 2 * * * <path_to_script>/backup create
```


## License
s3cmd-backup is released under the [MIT license](LICENSE).