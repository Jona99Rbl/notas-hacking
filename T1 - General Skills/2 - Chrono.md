### Descripción
How to automate tasks to run at intervals on linux servers?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
How to automate tasks to run at intervals on linux servers?Use ssh to connect to this server:

```
Server: saturn.picoctf.net
Port: 54134
Username: picoplayer 
Password: emrdK96SGH
```
### Solución
Iniciamos con la conexión al servidor a traves del comando **ssh** con el usuario, liga del servidor y puerto a donde nos debemos de conectar, donde una vez hayamos ingresado de forma correcta la contraseña proporcionada en la descripción, habremos accedido al servidor en cuestión:

```shell
the_robx-picoctf@webshell:~$ ssh picoplayer@saturn.picoctf.net -p 54134
The authenticity of host '[saturn.picoctf.net]:54134 ([13.59.203.175]:54134)' can't be established.
ED25519 key fingerprint is SHA256:dMTscRrUiURy7uMu5eGWwEKdd2FzqLzx6LfWhssWnNQ.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:54134' (ED25519) to the list of known hosts.
picoplayer@saturn.picoctf.net's password: 
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.5.0-1023-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.
```

Al acceder al servidor, procedemos a consultar lo que haya en este directorio, donde como se puede ver a continuación, no tenemos nada, no es hasta que cambiamos a la raíz con `cd /` volvemos a emplear **ls** y vemos varias carpetas contenidas en él:

```shell
picoplayer@challenge:~$ ls
picoplayer@challenge:~$ cd /
picoplayer@challenge:/$ ls
bin  boot  challenge  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

Del listado anterior se procede a acceder la carpeta ***/etc*** donde se encuentran los archivos de configuración del sistema, donde ahora debemos ver lo que contiene esta carpeta con el comando **ls**:

```shell
icoplayer@challenge:/$ cd etc
picoplayer@challenge:/etc$ ls -la
total 272
drwxr-xr-x 1 root   root       66 Feb 20 03:54 .
drwxr-xr-x 1 root   root       51 Feb 20 03:54 ..
-rw------- 1 root   root        0 Mar  8  2023 .pwd.lock
-rw-r--r-- 1 root   root     3028 Mar  8  2023 adduser.conf
drwxr-xr-x 1 root   root      180 Aug  4  2023 alternatives
drwxr-xr-x 7 root   root      127 Mar  8  2023 apt
-rw-r--r-- 1 root   root     2319 Feb 25  2020 bash.bashrc
-rw-r--r-- 1 root   root      367 Apr 14  2020 bindresvport.blacklist
drwxr-xr-x 2 root   root        6 Mar 27  2023 binfmt.d
drwxr-xr-x 3 root   root       22 Aug  4  2023 ca-certificates
-rw-r--r-- 1 root   root     5892 Aug  4  2023 ca-certificates.conf
drwxr-xr-x 2 root   root       24 Mar  8  2023 cloud
drwxr-xr-x 1 root   root       26 Aug  4  2023 cron.d
drwxr-xr-x 1 root   root       26 Aug  4  2023 cron.daily
drwxr-xr-x 2 root   root       26 Aug  4  2023 cron.hourly
drwxr-xr-x 2 root   root       26 Aug  4  2023 cron.monthly
drwxr-xr-x 2 root   root       26 Aug  4  2023 cron.weekly
-rw-r--r-- 1 root   root       43 Aug  4  2023 crontab
drwxr-xr-x 4 root   root       39 Aug  4  2023 dbus-1
-rw-r--r-- 1 root   root     2969 Aug  3  2019 debconf.conf
-rw-r--r-- 1 root   root       13 Dec  5  2019 debian_version
drwxr-xr-x 1 root   root       68 Aug  4  2023 default
-rw-r--r-- 1 root   root      604 Sep 15  2018 deluser.conf
drwxr-xr-x 4 root   root       65 Aug  4  2023 dhcp
drwxr-xr-x 4 root   root       55 Mar  8  2023 dpkg
-rw-r--r-- 1 root   root      685 Feb 14  2020 e2scrub.conf
-rw-r--r-- 1 root   root      106 Mar  8  2023 environment
-rw-r--r-- 1 root   root       37 Mar  8  2023 fstab
-rw-r--r-- 1 root   root     2584 Feb  1  2020 gai.conf
-rw-r--r-- 1 root   root      602 Aug  4  2023 group
-rw-r--r-- 1 root   root      583 Aug  4  2023 group-
-rw-r----- 1 root   shadow    505 Aug  4  2023 gshadow
-rw-r----- 1 root   shadow    490 Aug  4  2023 gshadow-
drwxr-xr-x 3 root   root       20 Aug  4  2023 gss
-rw-r--r-- 1 root   root       92 Dec  5  2019 host.conf
-rw-r--r-- 1 root   root       10 Feb 20 03:54 hostname
-rw-r--r-- 1 root   root      175 Feb 20 03:54 hosts
-rw-r--r-- 1 root   root      411 Aug  4  2023 hosts.allow
-rw-r--r-- 1 root   root      711 Aug  4  2023 hosts.deny
drwxr-xr-x 1 root   root       41 Aug  4  2023 init.d
-rw-r--r-- 1 root   root     1748 Feb 25  2020 inputrc
-rw-r--r-- 1 root   root       26 Aug 22  2022 issue
-rw-r--r-- 1 root   root       19 Aug 22  2022 issue.net
drwxr-xr-x 1 root   root       23 Aug  4  2023 kernel
-rw-r--r-- 1 root   root     9974 Aug  4  2023 ld.so.cache
-rw-r--r-- 1 root   root       34 Apr 14  2020 ld.so.conf
drwxr-xr-x 2 root   root       52 Mar  8  2023 ld.so.conf.d
-rw-r--r-- 1 root   root      267 Dec  5  2019 legal
-rw-r--r-- 1 root   root      191 Feb 18  2020 libaudit.conf
lrwxrwxrwx 1 root   root       27 Aug  4  2023 localtime -> /usr/share/zoneinfo/Etc/UTC
-rw-r--r-- 1 root   root    10550 Feb  7  2020 login.defs
drwxr-xr-x 2 root   root       49 Mar  8  2023 logrotate.d
-rw-r--r-- 1 root   root      104 Aug 22  2022 lsb-release
-rw-r--r-- 1 root   root       33 Aug  4  2023 machine-id
-rw-r--r-- 1 root   root      111 Jan 16  2020 magic
-rw-r--r-- 1 root   root      111 Jan 16  2020 magic.mime
-rw-r--r-- 1 root   root     1604 Aug  4  2023 mailcap
-rw-r--r-- 1 root   root      449 Oct 18  2019 mailcap.order
-rw-r--r-- 1 root   root    24546 Oct 18  2019 mime.types
-rw-r--r-- 1 root   root      808 Feb 14  2020 mke2fs.conf
drwxr-xr-x 2 root   root       26 Aug  4  2023 modules-load.d
lrwxrwxrwx 1 nobody nogroup    12 Feb 20 03:54 mtab -> /proc/mounts
drwxr-xr-x 8 root   root      109 Aug  4  2023 networkd-dispatcher
-rw-r--r-- 1 root   root       91 Dec  5  2019 networks
-rw-r--r-- 1 root   root      510 Aug  4  2023 nsswitch.conf
drwxr-xr-x 2 root   root        6 Mar  8  2023 opt
lrwxrwxrwx 1 root   root       21 Aug 22  2022 os-release -> ../usr/lib/os-release
-rw-r--r-- 1 root   root      552 Dec 17  2019 pam.conf
drwxr-xr-x 1 root   root      185 Aug  4  2023 pam.d
-rw-r--r-- 1 root   root     1330 Aug  4  2023 passwd
-rw-r--r-- 1 root   root     1279 Aug  4  2023 passwd-
-rw-r--r-- 1 root   root      581 Dec  5  2019 profile
drwxr-xr-x 2 root   root       30 Mar  8  2023 profile.d
drwxr-xr-x 2 root   root       27 Aug  4  2023 python3
drwxr-xr-x 2 root   root       30 Aug  4  2023 python3.8
drwxr-xr-x 2 root   root        6 Jun 21  2019 rc0.d
drwxr-xr-x 2 root   root        6 Jun 21  2019 rc1.d
drwxr-xr-x 1 root   root       50 Aug  4  2023 rc2.d
drwxr-xr-x 1 root   root       50 Aug  4  2023 rc3.d
drwxr-xr-x 1 root   root       50 Aug  4  2023 rc4.d
drwxr-xr-x 1 root   root       50 Aug  4  2023 rc5.d
drwxr-xr-x 2 root   root        6 Jun 21  2019 rc6.d
drwxr-xr-x 2 root   root       23 Mar  8  2023 rcS.d
-rw-r--r-- 1 root   root       72 Feb 20 03:54 resolv.conf
lrwxrwxrwx 1 root   root       13 Feb  9  2023 rmt -> /usr/sbin/rmt
drwxr-xr-x 4 root   root     4096 Mar  8  2023 security
drwxr-xr-x 2 root   root       27 Mar  8  2023 selinux
-rw-r----- 1 root   shadow    808 Aug  4  2023 shadow
-rw-r----- 1 root   shadow    671 Aug  4  2023 shadow-
-rw-r--r-- 1 root   root      116 Mar  8  2023 shells
drwxr-xr-x 2 root   root       57 Mar  8  2023 skel
drwxr-xr-x 1 root   root       58 Aug 25  2023 ssh
drwxr-xr-x 4 root   root       53 Aug  4  2023 ssl
-rw-r--r-- 1 root   root       24 Aug  4  2023 subgid
-rw-r--r-- 1 root   root        0 Mar  8  2023 subgid-
-rw-r--r-- 1 root   root       24 Aug  4  2023 subuid
-rw-r--r-- 1 root   root        0 Mar  8  2023 subuid-
-r--r----- 1 root   root      755 Apr  4  2023 sudoers
drwxr-xr-x 2 root   root       20 Aug  4  2023 sudoers.d
-rw-r--r-- 1 root   root     2351 Feb 13  2020 sysctl.conf
drwxr-xr-x 1 root   root       28 Aug  4  2023 sysctl.d
drwxr-xr-x 1 root   root     4096 Aug  4  2023 systemd
drwxr-xr-x 2 root   root       20 Mar  8  2023 terminfo
-rw-r--r-- 1 root   root        8 Aug  4  2023 timezone
drwxr-xr-x 2 root   root        6 Mar 27  2023 tmpfiles.d
-rw-r--r-- 1 root   root     1260 Dec 14  2018 ucf.conf
drwxr-xr-x 3 root   root       28 Aug  4  2023 ufw
drwxr-xr-x 2 root   root       84 Mar  8  2023 update-motd.d
-rw-r--r-- 1 root   root     4942 Nov 12  2021 wgetrc
-rw-r--r-- 1 root   root      642 Sep 24  2019 xattr.conf
drwxr-xr-x 4 root   root       86 Aug  4  2023 xdg
```

Como el nombre del reto involucra la palabra "chrono", por curiosidad se decide a probar que contiene **crontab**, por lo que usaremos el comando **cat**:

```shell
picoplayer@challenge:/etc$ cat crontab 
# picoCTF{Sch3DUL7NG_T45K3_L1NUX_0bb95b71}
```

Obteniendo así la bandera requerida para solucionar el reto:

```
picoCTF{Sch3DUL7NG_T45K3_L1NUX_0bb95b71}
```
### Notas Adicionales

### Referencias
https://learn.microsoft.com/es-es/troubleshoot/developer/webapps/aspnetcore/practice-troubleshoot-linux/1-2-linux-special-directories-users-package-managers
https://www.hostinger.mx/tutoriales/sintaxis-crontab#:~:text=La%20tabla%20cron%20o%20Crontab,tarea%20a%20una%20hora%20determinada.