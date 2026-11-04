![](images/media/image1.png){width="1.55in"
height="0.8211920384951881in"}

DFCS Day 1 ASSIGNMENT

Name: Wazir Jawad Ahmed

![](images/media/image2.png){width="0.83in"
height="0.5237664041994751in"}

**\**

# Task A: Malware types and examples

  ----------------------- --------------- ---------------- ------------------- -----------------
  **Type**                **Definition in **Named          **How it spread**   **Primary
                          my own words**  example + year**                     impact**

  **Virus**               A program that  **CIH (Chernobyl Infected            Overwrote data on
                          attaches itself virus)**, 1998   executables passed  the hard disk
                          to another                       around on floppies, and, on some
                          file, usually                    pirated software    motherboards,
                          an .exe, and                     and email           wiped the BIOS
                          only runs and                    attachments.        flash chip so the
                          spreads when                                         PC would not even
                          someone runs                                         start.
                          that infected                                        
                          file.                                                

  **Worm**                Malware that    **WannaCry**,    Used the Eternal    I encrypted files
                          copies itself   May 2017         Blue exploit        and asked for
                          from machine to                  against SMBv1 file  Bitcoin. It hit
                          machine over                     sharing on          around 150
                          the network by                   unpatched Windows   countries and
                          abusing a bug                    PCs, then scanned   forced UK NHS
                          in a service.                    for more victims.   hospitals to
                          Nobody has to                                        cancel
                          click anything.                                      appointments.

  **Trojan**              Malware that    **Zeus (Zbot)**, Phishing emails and Logged keystrokes
                          pretends to be  2007             drive-by downloads  and grabbed login
                          something                        from hacked         forms inside the
                          useful or                        websites.           browser to steal
                          harmless, so                                         online banking
                          the user                                             details and empty
                          installs it                                          accounts.
                          themselves. It                                       
                          does not spread                                      
                          on its own.                                          

  **Ransomware**          Malware that    **REvil via      Supply-chain        Hit IT service
                          locks or        Kaseya VSA**,    attack: criminals   providers and,
                          encrypts your   July 2021        abused a flaw in    through them,
                          files and                        Kaseya              1,500 small
                          demands money                    remote-management   businesses. REvil
                          for the key to                   software and pushed asked for seventy
                          get them back.                   ransomware to its   million dollars
                                                           customers as if it  to unlock
                                                           were an update.     everything.

  **Spyware**             Software that   **Pegasus (NSO   Malicious links at  Full access to
                          secretly        Group)**,        first, later        the phone:
                          watches what    founded 2016,    zero-click exploits messages, calls,
                          you do and      widely exposed   through iMessage    camera,
                          sends it to     2021             and WhatsApp that   microphone,
                          someone else.                    needed no tap from  location. Used
                                                           the victim.         against
                                                                               journalists,
                                                                               activists, and
                                                                               politicians.

  **Adware**              Software that   **Fireball**,    Bundled inside free Hijacked the home
                          pushes unwanted 2017             software that       page and search
                          ads, often by                    people downloaded   engine on an
                          changing                         and installed.      estimated 250
                          browser                                              million computers
                          settings or                                          and could also
                          injecting ads                                        download more
                          into pages, to                                       malware.
                          earn money for                                       
                          its owner.                                           

  **Rootkit**             Malware built   **Sony BMG       Installed itself    Hid files and
                          to hide itself, XCP**, 2005      when someone played processes and
                          and other                        one of Sony\'s      left the PC open
                          malware, from                    music CDs on a      for other malware
                          the operating                    Windows PC.         to hide behind
                          system and                                           it. Led to a
                          antivirus by                                         recall and
                          running at an                                        lawsuits.
                          exceptionally                                        
                          low level.                                           

  **Keylogger**           Records every   **Agent Tesla**, Cheap commercial    Stole saved
                          key you press,  2014 onward      tool sold online;   browser
                          so the attacker                  delivered by        passwords,
                          gets passwords,                  phishing emails     screenshots and
                          card numbers,                    with booby-trapped  keystrokes and
                          and chats.                       Office or archive   sent them out by
                                                           attachments.        email or FTP,
                                                                               often from small
                                                                               and mid-sized
                                                                               companies.

  **Botnet agent**        A small program **Mirai**, 2016  Scanned the         Its botnet
                          that turns an                    internet for        launched the DDoS
                          infected device                  cameras and routers on DNS provider
                          into a bot                       and logged in with  Dyn in October
                          waiting for                      factory default     2016, knocking
                          orders from a                    passwords.          sites like
                          command server,                                      Twitter, Netflix,
                          so thousands                                         and Reddit
                          can attack                                           offline for many
                          together.                                            users.

  **Fileless /            Attacks that    **Operation      Spear-phishing      Months of quiet
  living-off-the-land**   use tools       Cobalt Kitty     first, then         spying inside a
                          already on the  (APT32 /         PowerShell, WMI and large corporation
                          machine         OceanLotus)**,   scheduled tasks to  in Southeast
                          (PowerShell,    2017             stay on the         Asia.
                          WMI, scheduled                   network.            
                          tasks) and live                                      
                          in memory or                                         
                          the registry,                                        
                          so there is                                          
                          little or no                                         
                          malicious file                                       
                          to scan.                                             

  **Logic bomb**          Code that sits  **UBS            Not spread at all.  Deleted files on
                          quietly until a PaineWebber      Planted by an       around 2,000
                          condition is    (Roger           insider who was a   servers across
                          met, like a     Duronio)**, 2002 system              the company\'s
                          date or an                       administrator.      branches and cost
                          account being                                        millions to
                          deleted, and                                         recover. Duronio
                          then does                                            was sent to
                          damage.                                              prison.

  **Bootkit**             A rootkit that  **TDL4 (TDSS)**, Installed through a Survived
                          infects the     2010             pay-per-install     reinstalls and
                          boot process                     network, mostly     hid from
                          (the MBR or                      from infected       antivirus. Built
                          boot sector) so                  downloads and       a botnet of
                          it loads before                  hacked websites.    millions of PCs
                          the operating                                        used for fraud
                          system and                                           and spam.
                          security tools                                       
                          do.                                                  
  ----------------------- --------------- ---------------- ------------------- -----------------

## Which type is most dangerous for a Pakistani SME?

I think ransomware is the biggest threat for Pakistani SMEs because most
small businesses keep their orders, accounts and customer data on just
one or two Windows computers, and usually don\'t even have proper
backups. If all those files get encrypted, the whole business can come
to a stop. On top of that, the ransom demanded in dollars or Bitcoin can
be more than what a small business earns in a month.

Things like pirated Windows and Office, outdated systems, and employees
opening unknown email or WhatsApp attachments make these businesses even
more vulnerable. Attacks like WannaCry and Kaseya show how serious this
can be. Most small businesses also don\'t have a dedicated IT person to
monitor their systems or deal with such attacks.

# Task B2: Change permissions three ways with chmod

## Commands

> mkdir lab && cd lab
>
> touch report.txt
>
> ls -l report.txt \# BEFORE (default, usually 644)
>
> chmod 640 report.txt \# change 1: octal
>
> ls -l report.txt
>
> chmod u+x report.txt \# change 2: symbolic
>
> ls -l report.txt
>
> chmod 600 report.txt \# change 3: octal
>
> ls -l report.txt

## What you should see

  ----------------------------------------------------------------------------------
  **\#**   **Command**      **Expected ls -l** **Octal**   **What it did**
  -------- ---------------- ------------------ ----------- -------------------------
  0        touch report.txt -rw-r\--r\--       644         Starting point: owner
                                                           read/write, everyone else
                                                           read only.

  1        chmod 640        -rw-r\-\-\-\--     640         Group keeps read only
           report.txt                                      (4). Others lose all
           (octal)                                         access (0), so they can
                                                           no longer read the file.

  2        chmod u+x        -rwxr\-\-\-\--     740         Adds execute for the
           report.txt                                      owner only. Group and
           (symbolic)                                      others are untouched. The
                                                           owner could now run it as
                                                           a program.

  3        chmod 600        -rw\-\-\-\-\-\--   600         Removes execute from the
           report.txt                                      owner and read from the
           (octal)                                         group. Only the owner can
                                                           read and write. This is
                                                           the right mode for
                                                           private files like keys.
  ----------------------------------------------------------------------------------

## Screenshots

  -----------------------------------------------------------------------
  ![](images/media/image3.png){width="6.768055555555556in"
                      height="2.4950492125984254in"}

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  ![](images/media/image3.png){width="6.501432633420823in"
                      height="0.8617290026246719in"}

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  ![](images/media/image3.png){width="6.768055555555556in"
                      height="0.8104647856517935in"}

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
   ![](images/media/image3.png){width="6.768055555555556in"
                       height="1.158173665791776in"}

  -----------------------------------------------------------------------

## Explanation 

Change 1 (640): I used octal to set owner read/write, group read, and
nothing for others. Others can no longer open the file.

Change 2 (u+x): I used symbolic mode to add execute for the owner only.
The mode went from 640 to 740 and nothing else changed.

Change 3 (600): I went back to octal and locked the file down so only
the owner can read and write it, like a private key file.

# Task B4: Encrypt with OpenSSL, read the header with xxd

## Commands

> mkdir -p \~/cyber && cd \~/cyber
>
> echo \"my secret message\" \> secret.txt
>
> \# encrypt
>
> openssl enc -aes-256-cbc -salt -pbkdf2 -in secret.txt -out secret.enc
>
> ls -l secret.txt secret.enc
>
> \# look inside the encrypted file
>
> xxd -l 16 secret.enc
>
> file secret.enc
>
> \# decrypt to prove it works (use the SAME flags, including -pbkdf2)
>
> openssl enc -d -aes-256-cbc -pbkdf2 -in secret.enc -out decrypt.txt
>
> cat decrypt.txt

## What you should see

> 00000000: 5361 6c74 6564 5f5f xxxx xxxx xxxx xxxx Salted\_\_\...\.....
>
> secret.enc: openssl enc\'d data with salted password
>
> my secret message

The last 8 bytes in the xxd line (the x characters above) are random, so
yours will look different. The first 8 bytes must read Salted\_\_.

## Screenshots

  -----------------------------------------------------------------------
   ![](images/media/image4.png){width="6.768055555555556in"
                      height="1.9340277777777777in"}

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
   ![](images/media/image5.png){width="6.768055555555556in"
                      height="1.4715277777777778in"}

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
   ![](images/media/image6.png){width="6.768055555555556in"
                      height="1.1402777777777777in"}

  -----------------------------------------------------------------------

## Explanation 

# When OpenSSL uses \`-salt\`, it adds an 8-byte tag \`Salted\_\_\` at the beginning of the encrypted file. In hex, it looks like \`53 61 6c 74 65 64 5f 5f\`. The next 8 bytes contain a random salt, and everything after that is the encrypted data.

# The salt is not secret. OpenSSL stores it in the file because it needs it along with my password to generate the same key during decryption. Because a new random salt is generated every time, encrypting the same file with the same password twice will produce different outputs.

# Using \`file\` and \`xxd\`, I can quickly identify whether an unknown file uses OpenSSL\'s salted encryption format without even knowing the password.
