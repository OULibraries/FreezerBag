# FreezerBag
Python Utility to backup and restore LoC Bags to/from Amazon Glacier.
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

## Note
* Only tested with unzipped/untarred bags.  Not a big deal to add support though.

## Built with
* [LoC Bagit Python Library](https://github.com/LibraryOfCongress/bagit-python/)
* [AWS Boto Python Library] (https://github.com/boto/boto)
* [Thomas Sileo's ideas] (http://thomassileo.com/blog/2012/10/24/getting-started-with-boto-and-glacier)

## Extra credit
I wrote this with the idea that I would run it repeatedly as a cron job.
I banged out some shell scripts to make that happen and put them in a repo called [FreezerBag-ops](https://github.com/OULibraries/FreezerBag-ops).
