#sftp使用
1、sublime安装sftp插件
2、Project->Add Folder to Project
3、工程上右键->SFTP/FTP->Map To Remote
自动生成sftp-config.json

修改

```
{
    // The tab key will cycle through the settings when first created
    // Visit http://wbond.net/sublime_packages/sftp/settings for help
    
    // sftp, ftp or ftps
    "type": "sftp",

    "save_before_upload": true,
    "upload_on_save": true,
    "sync_down_on_open": false,
    "sync_skip_deletes": false,
    "sync_same_age": true,
    "confirm_downloads": false,
    "confirm_sync": true,
    "confirm_overwrite_newer": false,
    
    "host": "10.16.59.102",
    "user": "yangwenliang",
    "password": "H7sf+awph7sf+awk",
    //"port": "22",
    
    "remote_path": "/home/yangwenliang/abtest/abtest",

    "ignore_regexes": [
        "\\.sublime-(project|workspace)", "sftp-config(-alt\\d?)?\\.json",
        "sftp-settings\\.json", "/venv/", "\\.svn/", "\\.hg/", "\\.git/",
        "\\.bzr", "_darcs", "CVS", "\\.DS_Store", "Thumbs\\.db", "desktop\\.ini"
    ],
    //"file_permissions": "664",
    //"dir_permissions": "775",
    
    //"extra_list_connections": 0,

    "connect_timeout": 30,
    //"keepalive": 120,
    //"ftp_passive_mode": true,
    //"ftp_obey_passive_host": false,
    //"ssh_key_file": "~/.ssh/id_rsa",
    //"sftp_flags": ["-F", "/path/to/ssh_config"],
    
    //"preserve_modification_times": false,
    //"remote_time_offset_in_hours": 0,
    //"remote_encoding": "utf-8",
    //"remote_locale": "C",
    //"allow_config_upload": false,
}
```

4、再次工程上右键->SFTP/FTP->Sync Remote - Local


5、sftp有个蛋疼的问题，比如，我在local重命名一个文件，或者用webpack等编译出来的文件，不会自动上传，需要手动去save或者上传。
目前没有好的办法，只能用gulp-sftp插件，但是配置起来相当繁复。。


