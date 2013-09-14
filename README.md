cPanel NFS quota emulator
=========================

The two files contained in this packages are drop-in replacements for `/usr/local/cpanel/bin/quota` and `/usr/local/cpanel/bin/safe_fetch_repquota`. It reports quota to cPanel so that you get warning emails and information back to WHM accounts list and to the cPanel account sidebar. However, **it won't enforce quotas, ie. users can go overquota**.

You still need quota binaries installed, and quota-reporting support for NFS mounts. You also need PHP installed because I don't know Perl.

It has been tested on WHM/cPanel 11.38.2.

Will it work for me?
--------------------

Possibly, it hasn't been thoroughly tested. Try `quota -vw julien`. If you get an output like the one below, chances are high it will work :) 

<pre>
Block grace time: 7days; Inode grace time: 7days
                        Block limits                File limits
User            used    soft    hard  grace    used  soft  hard  grace
10.x.y.z:/nfs-server/home 6989867       0       0               0       0       0        
</pre>

Installing
----------

Just run the following commands as root:

1. `cd /usr/local/cpanel/bin/`
2. `mv quota quota.bak`
3. `wget https://raw.github.com/cahri/cpanel-nfs-quota/master/quota`
4. `chmod 755 quota`
5. `mv safe_fetch_repquota safe_fetch_repquota.bak`
6. `wget https://raw.github.com/cahri/cpanel-nfs-quota/master/safe_fetch_repquota`
7. `chmod 755 safe_fetch_repquota`

Known limitations
-----------------

It doesn't work if your NFS server does not report quotas. Feel free to improve the script to use `du` in such a case (with some caching involved since it's resource-intensive).

Obviously, WHM/cPanel updates might break this script or overwrite it.

Credits
-------

Concept and development by [Julien Tessier](http://www.linkedin.com/in/jutessier) for [Cahri](http://www.cahri.com/).