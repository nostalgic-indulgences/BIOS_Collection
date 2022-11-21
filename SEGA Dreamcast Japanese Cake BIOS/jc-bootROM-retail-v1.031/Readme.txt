_________________________________________________________________________________________

 Dreamcast Custom bootROM v1.031 Retail
                                                              by japanese_cake 26/08/2015
_________________________________________________________________________________________


[+] What is that?
    ~~~~~~~~~~~~~

        It is a modified BIOS for the SEGA Dreamcast. It is based on the retail
        BIOS v1.01d.


[+] What does it do?
    ~~~~~~~~~~~~~~~~

        This version has the following features:
           - Region free: boot GD-ROM/MIL-CD from any region. The J/U/E flags as
             well as the area protection slots that reside in the IP.BIN are now
             simply ignored.

           - No VGA flag check: whether or not the game supports the VGA output, it
             boots. There are games that support the VGA cable but for some
             reason the VGA flag in the IP.BIN is not set. The use of a boot CD
             was thus needed. Now, you will never get the annoying "This game
             doesn't support the AV cable that is currently connected to the main
             console" anymore.

           - No bootfile LBA check: allow a game to boot even if its bootfile, more
             commonly called 1ST_READ.BIN, is not located on the outer part of the
             disc. I don't know whether it can be of any use for people using discs.
             However, for the lucky owners of ODDE for Dreamcast, you can re-build
             games' track 3 without any padding.
             For instance, with "Dreamkey 3.0 v1.001 (2001)(Sega)(PAL)(M8)[!]", the
             track03.bin is ~1.10GB. Re-building the track (track03.iso) using the
             following command:
                mkisofs -C 0,45000 -V DREAMKEY3 -G IP.BIN -l -o track03.iso data
             will made the track03.iso way smaller (only ~93MB). Homebrews can also
             be rebuilt to GDI so that the 0GDTEXT.PVR texture shows up in the
             audio player :)

           - Display bootROM version: the current version of the bootROM appears in
             the up-right corner of the screen so that you know what BIOS is running.

           - SEGA License screen skip: the white and bleu "SEGA" screen does not show
             up and force you to wait ~6 seconds anymore. The game starts right away!
             Note: most of the IP.BIN code is still executed so that a game that needs
             a particular setup from the bootstraps still works (except B!eemcast, but
             it is another issue).

           - MIL-CD/backup direct boot: in the Dreamcast main menu with the four icons,
             starting a MIL-CD or a backup resets the system in order to boot it up.
             Now you can enjoy all medias booting the same way, with no reset.

           - Black fade-in color while booting from menu: this is just an aesthetic
             patch to have all media booting the same way, visually speaking. Usually,
             when a GDROM boots up from the menu, the screen fades in a white color.
             However, MIL-CD and backups use a black color. Since the white license
             screen is gone and that most if not all games start with a black screen, it
             makes sense to have both GDROM and MIL-CD using the same black fade-in color
             when they boot.

           - No VMU copy-protected file check: some games do not allow you to copy their
             saves to another VMU. Pretty annoying, right? Well, now you are free to do
             what you want.
             Note #1: the copy-protected flag is not stored in the save itself but in
             the VMU filesystem.
             Note #2: the BIOS will update and unset that flag only when the save is
             copied to another VMU. If a protected save is copied and then you browse
             your saves using a no-custom BIOS, you will notice that the original save
             is still copy-protected and its copy is not.


[+] Does it work on the real hardware?
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        Yes, sure, as long as the Dreamcast has a BIOS mod and Dreamshell to flash
        the alternate BIOS chip.


[+] Why using "1.03X" as the version number?
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        The v1.004, v1.01c, v1.01d and v1.022 are the only version numbers known
        for the official SEGA bootROM (BIOS). Thus I decided that my custom versions
        will use version numbers starting from v1.030.

_________________________________________________________________________________________

                                                                       jc.dcdev@gmail.com
                                                            japanese-cake.livejournal.com
_________________________________________________________________________________________