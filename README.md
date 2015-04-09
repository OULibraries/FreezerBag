# FreezerBag
Python Utility to backup and restore LoC Bags to/from Amazon Glacier
```
optional arguments:
  -h, --help            show this help message and exit
  -f, --freeze          backup to Amazon Glacier
  -t, --thaw            restore from Amazon Glacier
  -s, --setup           Get AWS Setup information
  -vid VAULTID, --vaultid VAULTID
                        the name of the Amazon Glacier Vault
  -b BAG, --bag BAG     the name of the bag
  -p PATH, --path PATH  the parent directory of the bag
```

## Built with
* [LoC Bagit Python Library](https://github.com/LibraryOfCongress/bagit-python/)
* [AWS Boto Python Library] (https://github.com/boto/boto)
* [Thomas Sileo's ideas] (http://thomassileo.com/blog/2012/10/24/getting-started-with-boto-and-glacier)

## Extra credit
I wrote this with the idea that I would run it repeatedly as a cron job.
Here's a quickie example of just such a script.
```
#!/bin/sh
PATH=/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
BAGSDIR="/some/directory/with/bags/directly/under/it"
VAULT="freezerbag_vaultname"
LOGFILE="/var/log/freezerbag.log"
EMAIL="email@example.com"

(
  flock -x -w 10 200 || exit 1

  for BAGPATH in `find $BAGSDIR -mindepth 1 -maxdepth 1 -type d`
  do
    BAGNAME=$(basename "$BAGPATH")
    echo "$BAGNAME"
    echo `date` > $LOGFILE
    exec python /some/path/freezerbag.py --freeze --bag $BAGNAME --path $BAGSDIR --vault $VAULT 2>&1 | tee ${LOGFILE}
    mail -s "Freezerbag $BAGNAME `date`" $EMAIL < $LOGFILE
  done
) 200>/var/lock/freezer_bag_cronlock
```
