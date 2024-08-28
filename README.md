# Locales_ISO-8601
## General explanation

- These instructions are made for people want special adjustments like professional "COLLATING" and/or "ISO-8601" date- & time-format.
- These instructions are tailored for Arch-Linux & Derivates, but can be adapted to any other Linux too.
- These instructions are tailored for any user with few experience on Linux.

## General Information
* I installed my Arch-Linux with the support of `Calamares` and...
* Choose "English" as Language and "Germany" as country.
* In case you have installed your Arch-Linux the normal way and or want a complete new Locale-Set --> use first the instruction from **§ 8** on.

Credential:
[Arch-Linux Locale-Wiki](https://wiki.archlinux.org/title/locale) -- [Arch-Linux Locale-Man-Page](https://man.archlinux.org/man/locale.7)

## Scope of work
Make **ISO-8601** available to every user & data-base on the machine or server in a very simple way.

### 1. Read/Set the actual default Locales

Read actual standard locale or set the new locale to take effect immediately with the following two commands. Normally, the new values will take effect for new sessions at login. These two commands allow you to see in "Terminal" if your settings are good or some errors are present (like was in my case).
```
$ unset LANG

$ source /etc/profile.d/locale.sh
```
**Notes:** 
* The `LANG` variable has to be unset first, otherwise `locale.sh` will not update the values from `locale.conf`.
* Only new and changed variables will be updated; variables removed from `locale.conf` will still be set in the session.

**Note:** XDG-Utils must be installed. Not yet existing file must be created e.g. `/etc/skel/.config/locale.conf`

### 2. Prerequisite
Check, let the system check if following prerequisite are installed and in case install them, is you made a proper installation you don't nrrd those again, but in case...

```
pacman -S --needed --noconfirm archlinux-xdg-menu haskell-xdg-basedir \
haskell-xdg-desktop-entry libqtxdg libxdg-basedir qtxdg-tools \
xdg-dbus-proxy xdg-desktop-portal xdg-desktop-portal-kde xdg-user-dirs \
xdg-utils-cxx man-db man-pages man2html less \
glibc-locales haskell-data-default-instances-old-locale \
haskell-old-locale haskell-setlocale haskell-time-locale-compat \
haskell-with-location libwlocate mlocate perl-datetime-locale \
perl-encode-locale perl-local-lib perl-locale-codes perl-locale-gettext \
perl-locale-maketext-lexicon perl-locale-po plocate
```

### 3. Concerned Files

All listed files below allow every user of the machine to get homogeneous locale.

```
~/.bashrc

~/.config/locale.conf

~/.config/plasma-localerc

/etc/bash.bashrc

/etc/profile.d/locale.sh ### no need to edit

/etc/locale.conf

/etc/profile ### no need to edit

/etc/skel/.config/locale.conf
```

**Note:** `/etc/skel/.config/locale.conf` is for all user you create new.

### 4. My locales:
* **Note:** My system was installed through a (Calamares) GUI, i choose english as language & Germany as country 🟰 i changed only the `LC_TIME=en_SE.UTF-8` as in '$ 6.' shown.
* The command is `locale` , the output hereafter...:

```
locale: Cannot set LC_ALL to default locale: No such file or directory
LANG=en_US.UTF-8
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC=de_DE.UTF-8
LC_TIME=en_SE.UTF-8
LC_COLLATE="en_US.UTF-8"
LC_MONETARY=de_DE.UTF-8
LC_MESSAGES="en_US.UTF-8"
LC_PAPER=de_DE.UTF-8
LC_NAME=de_DE.UTF-8
LC_ADDRESS=de_DE.UTF-8
LC_TELEPHONE=de_DE.UTF-8
LC_MEASUREMENT=de_DE.UTF-8
LC_IDENTIFICATION=de_DE.UTF-8
LC_ALL=
```

#### 4.1. Explanation

- 4.1.0 Following line must remain empty or set to **C** in case the locale-settings are not working:

```
LC_ALL=

# or

LC_ALL=C
```

- 4.1.1. The Following Lines have to remain like your selected language during the installation or change all at the same value, e.g. `de_DE.UTF-8`:

```
LANG=
LC_CTYPE=
LC_IDENTIFICATION=
LC_MESSAGES=

```

- 4.1.2. Following Lines, e.g. if you are not in the USA, can you change according to the country you are:

```
LC_ADDRESS=
LC_MEASUREMENT=
LC_MONETARY=
LC_NAME=
LC_NUMERIC=
LC_PAPER=
LC_TELEPHONE=

```

* 4.1.3. Following Line is recommended to be set to **C** = professional collating, normally don't need specialsettings.

```
LC_COLLATE=

```

* 4.1.4. Following Line, with my changes, let show the time in 24 hours & the date in `ISO-8601` = `Y/m/d` , use `en_ZA.UTF-8` for displaying date with 'slash' `2023/12/25` or use `en_SE.UTF-8` or `ken_CM.UTF-8` for displaying date with 'dash' `2023-12-25`.

```
LC_TIME=
```

* 4.1.5. In this line you can set your primary language e.g. `en_US`, add a language variation e.g. `:en_GB` and/or add all languages you want to be installed/detected on the system e.g. `:de:es:fr:ia:it:jp:pt:ru:zh`. Please note the syntax = `:`+ "additional language" e.g. `:de:fr` etc..

```
LANGUAGE=
```


### 5. Set the new locale

* Set Locale to take effect immediately

```
$ unset LANG

$ source /etc/profile.d/locale.sh
```

At this point, you are done and can restart the machine to see the final results.

#### 6. Set locale on the fly or change only few locales 

* like [here from Raynman](https://bbs.archlinux.org/viewtopic.php?id=284333) explained

```
localectl set-locale LC_TIME=en_SE.UTF-8

localectl set-locale LANGUAGE=en_US 

```

### 7. Read Locale & more

* Actual running locales: `locale`
* All actual adjustments of your desktop `printenv`

### 8. Set completely new Locales

Assure first all prerequisite (§ 2 and § 3) are satisfied.

* 8.1. Read all present installed Locales you can choose `locale -a` or...
* 8.2. Edit `/etc/locale.gen` as 'ROOT' e.g. `sudo nano /etc/locale.gen` to see and/or enable other Locales.
* 8.3. To disable a Locale-Set set/type on front of the line a `#` e.g. `#en_US.UTF-8 UTF-8`
* 8.4. To enable ones, make the opposite of above line = delete the `#` on front of the locale you want.
* 8.5. You can also append an additional local at the end of the file e.g. `de_DE.UTF-8 UTF-8` but I don't recommend this if you made a classic Arch-Linux installation.
**Note:** this last step is not recommended and normally done by "Calamres" with very special settings.
* 8.6. Generate the new Locales as 'ROOT' with `locale-gen`.

If you need/want the special settings or want to make some changes to standard new create locales, please use/reuse **§ 4** and **§ 5** for this scope.

- [x] **Done!** **&** **ENJOY!** :wink:

![](https://github.com/Advantaged/Locales_ISO-8601/blob/main/locales_2023-12-24_09%3A38%3A16_0002.jpeg)
