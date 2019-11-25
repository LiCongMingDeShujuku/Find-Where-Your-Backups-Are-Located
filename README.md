![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 查找备份所在的位置
#### Find Where Your Backups Are Located
**发布-日期: 2015年11月4日 (评论)**

![#](images/find-where-your-backups-are-located-a.png?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这里是一些可以帮助你找到备份的位置的SQL逻辑（logic）。


## English
Here’s some SQL Logic to help you find where your backups are located.

---
## Logic
```SQL
use master;
set nocount on
 
select
    'database'      = upper(bs.database_name)
,   'time_of_backup'    = replace(replace(replace(left(max(bs.backup_finish_date), 19),':', '-'), 'AM', 'am'), 'PM', 'pm') + ' ' + datename(dw, max(bs.backup_finish_date))
,   'location'      = reverse(right(reverse(upper(bmf.physical_device_name)), len(bmf.physical_device_name) - charindex('\',reverse(bmf.physical_device_name),1) + 1))
,   'backup_file'       = right(bmf.physical_device_name, charindex('\', reverse('\' + bmf.physical_device_name)) - 1)
from
    msdb.dbo.backupset bs join msdb.dbo.backupmediafamily bmf on bs.media_set_id = bmf.media_set_id
--where
--  bs.backup_finish_date > (select getdate()- 30)
--  and bs.database_name  = 'COLLECTIONS'
group by
    bs.database_name, bs.backup_finish_date, bmf.physical_device_name
order by
    bs.database_name, bs.backup_finish_date desc


```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

