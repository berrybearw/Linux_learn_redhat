# Linux_learn_redhat
redhat 升級

參考 : 

* https://access.redhat.com/discussions/5664261
* [https://www.netbraintech.com/docs/ie80/Linux_System_Upgrade_Instructions_Offline.pdf](https://www.netbraintech.com/docs/ie80/Linux_System_Upgrade_Instructions_Offline.pdf)
* [https://access.redhat.com/solutions/1355683](https://access.redhat.com/solutions/1355683)

更新
---
離線 update 

先上傳或用光碟機讀取 iso 

接著 mount iso ， 然後到 /etc/yum.repos.d 建立一個檔案 副檔名 repo

```
mount 參考 https://github.com/berrybearw/Linux_learn_mount/blob/main/README.md
```

1. yum

清理 : yum clean all  

rm -r /var/cache/dnf

測試 : yum repolist enabled

升級 : yum update

1. dnf

清理 : dnf clean all

rm -r /var/cache/dnf

測試 : dnf update -v

升級 : dnf upgrade

error
---
    
`yum/dnf error: Failed to download metadata for repo`
    
檢查 /etc/yum.repos.d/ 副檔名 repo 檔
    
可以用 測試 來查看詳細錯誤 ( dnf update -v )
    
可能下載有誤 ( baseurl 讀取 , gpgkey 沒提供 )

yum repo 檔範例
---

```
[InstallMedia-BaseOS]
name=Red Hat Enterprise Linux 8 - BaseOS
metadata_expire=-1
gpgcheck=1
enabled=1
baseurl=file:///mnt/disc/BaseOS/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[InstallMedia-AppStream]
name=Red Hat Enterprise Linux 8 - AppStream
metadata_expire=-1
gpgcheck=1
enabled=1
baseurl=file:///mnt/disc/AppStream/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```

```
[InstallMedia-BaseOS] (可以自己命名 ， 不可以重複 )
name=Red Hat Enterprise Linux 8 - BaseOS ( 報錯時顯示名稱 ， 不可重複名稱 )
metadata_expire=-1
gpgcheck=1 ( 1 顯示需檢查 gpgkey )
enabled=1 ( 1 顯示是否啟動 )
baseurl=file:///mnt/disc/BaseOS/ ( 檔案在哪裡 ， 需要絕對路徑  )
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release ( 預設都是主機 /etc/pki/rpm-gpg )
```

