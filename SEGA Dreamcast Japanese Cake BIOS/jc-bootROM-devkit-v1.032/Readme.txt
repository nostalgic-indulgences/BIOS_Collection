_________________________________________________________________________________________

 Dreamcast Custom bootROM v1.032
                                                              by japanese_cake 20/06/2016
_________________________________________________________________________________________


[+] What is that?
    ~~~~~~~~~~~~~

    It is a modified BIOS for the SEGA Dreamcast. It is based on the retail BIOS v1.01d.
    It can be used either in emulators or in a real Dreamcast console. Each version is
    released with two types of boot animation: retail and devkit.


[+] What does it do?
    ~~~~~~~~~~~~~~~~

    This version has the following features:

    Region free:
        Boot GD-ROM/MIL-CD from any region. The J/U/E flags as well as the area
    protection slots that reside in the IP.BIN are now simply ignored.

	Auto region patching (only for GD-ROMs):
        To enhance game compatibility and by-pass region protection, the bootROM
    changes the system region to the one of the game. For instance if you launch the US
    version of "Silver" on a PAL system, assuming the J/U/E flags check is skipped, the
    latter crashes deliberately. With this BIOS the system region is overwritten with the
    one of the game right before passing the control to the game. Therefore, it boots
    correctly. Examples of games that perform a region check:
        - Urban Chaos v1.001 (2000)(EIDOS)(PAL)(en-fr)[!] (T36810D 50)
        - Urban Chaos v1.000 (2000)(EIDOS)(NTSC)(US)(en-fr)[!] (T36810N)
        - Silver v1.000 (2000)(Infogrames)(PAL)(M3)[!] (T15109D)
        - Silver v1.001 (2000)(Infogrames)(PAL)(en-nl)[!] (T15109D)
        - Silver v1.001 (2000)(Infogrames)(NTSC)(US)[!] (T15108N)
        - San Francisco RUSH 2049 v1.002 (2000)(Midway)(PAL)(M6)[!] (T-9709D-50)
        - San Francisco RUSH 2049 v1.001 (2000)(Midway)(NTSC)(US)[!] (T-9707N)
        - Elemental Gimmick Gear v1.001 (1999)(Vatical)(NTSC)(US)[!] (T41601N)

        Some other games do an additional check: the video broadcast. A game such as
    "San Francisco RUSH 2049" checks whether the system video broadcast is "correct": the
    NTSC/US and PAL/EURO version expect the video broadcast to be set to NTSC and PAL,
    respectively. An easy way to by-pass the broadcast check consists in overwriting the
    system video broadcast by the one normally used in the game region. The only drawback
    in doing so is that people that have a region-mod will see the video broadcast they
    have set overwritten. Therefore, the video broadcast patching is done on a per game
    basis. So far I have identified 3 games that do such check:
        - Elemental Gimmick Gear v1.001 (1999)(Vatical)(NTSC)(US)[!] (T41601N)
        - San Francisco RUSH 2049 v1.001 (2000)(Midway)(NTSC)(US)[!] (T-9707N)
        - San Francisco RUSH 2049 v1.002 (2000)(Midway)(PAL)(M6)[!] (T-9709D-50)

        If you think there are other games that do a video broadcast check, please
    contact me, I would then update the BIOS accordingly.

	    Note that the auto region patching is enabled only with GDROMs and GDI images. I
    assume that backups do not need it as they have already been cracked.

    Forced video mode to NTSC/PAL-60Hz:
        The bootROM animation, menu and license screen now use a video mode forced to
    60Hz. On PAL system with the R422 mod or NTSC US/JAP system, the output signal
    should be NTSC (60Hz), otherwise the output signal is PAL, with a 60Hz refresh rate.

        Now some PAL games (not all of them sorry!) like for instance House of the Dead 2
    run at 60Hz! Games that have their video mode hard-coded are not affected though.

        I do not really know whether forcing the video mode to 60Hz can cause problems
    for some people. If so please contact me and explain why. Thank you!

    No VGA flag check:
        Whether or not the game supports the VGA output, it boots. There are games that
    support the VGA cable but for some reason the VGA flag in the IP.BIN is not set. The
    use of a boot CD was thus needed. Now, you will never get the annoying "This game
    doesn't support the AV cable [...]" anymore.

    No bootfile LBA check:
        Allow a game to boot even if its bootfile, more commonly called 1ST_READ.BIN, is
    not located on the outer part of the disc. I don't know whether it can be of any use
    for people using discs. However, for the lucky owners of ODDE for Dreamcast, you can
    re-build games' track 3 without any padding.

        For instance, with "Dreamkey 3.0 v1.001 (2001)(Sega)(PAL)(M8)[!]", the track03 is
    ~1.10GB. Re-building the track (track03.iso) using the following command:
        mkisofs -C 0,45000 -V DREAMKEY3 -G IP.BIN -l -o track03.iso data
	    will made the track03.iso way smaller (only ~93MB). Homebrews can also be
    rebuilt to GDI so that the 0GDTEXT.PVR texture shows up in the audio player :)

    Display bootROM version:
        The current version of the bootROM appears in the up-right corner of the screen
    so that you know what BIOS is running.

    Date/Time screen skip:
        Everytime the system boots up, it checks whether the real time clock (RTC) is
    set. If it is not, you are then asked to set the date and time. The datetime value is
    then kept up to date by a small integrated circuit which uses an alternate power
    supply: usually a rechargeable Sanyo ML2430 battery.

        Back in the days when you got your brand new Dreamcast from a retailer, you had
    to set the date once then you were good until you power off the console for more than
    a couple of weeks or so. But with age, that battery gets a bit lazy and does not keep
    the charge anymore. Everytime you shutdown your Dreamcast, the datetime value is lost
    and everytime you switch it on you have to set that value again. One way to fix this
    consists in changing the battery by a new one.

        But, as the date and time are not required to play and I am sure you do not turn
    on your Dreamcast to know what time it is, we can fix that problem via the software.
    The custom bootROM sets a default date and time value so you do not get the
    "set date/time" screen anymore (see note #1).

    No VMU copy-protected file check:
        Some games do not allow you to copy their saves to other VMUs. Pretty annoying,
    right? Well, now you are free to do whatever you want (see note #2).
             
    Fade-in and fade-out colors:
        Depending on the boot settings (SEGA license screen and direct-boot) and the type
    of media inserted (GD-ROM or MIL-CD), the custom bootROM changes the fade-out and the
    fade-in colors when entering and exiting the Dreamcast main menu.

	    For example, when launching a MIL-CD or a backup, a black fade-in color is used
    to exit the main menu. However, if the direct-boot option is on, the color used will
    either be black or white depending on whether the SEGA license screen is skipped or
    not. This make the player's visual experience similar between booting a GD-ROM or a
    MIL-CD/backup.

    Custom bootROM settings:
        The custom bootROM provides new options to change boot behaviors and to customize
    the interface. You can change those options directly from the Dreamcast settings menu
    by pressing the "START" button. A window appears and prompts you select the settings
    you want to change. Read the next section to know more about those new options.


[+] Details about the custom bootROM settings
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        Starting from this version, v1.032, the custom bootROM handles new settings that
    can be changed from the Dreamcast settings menu by pressing the "START" button. Those
    settings are stored in the same way as original settings (language, date, audio and
    auto-start) in the Dreamcast internal flash memory. Note that the original and custom
    settings are saved only when you exit the Dreamcast settings menu.

    Boot animation (default: system region):
        Select the color of the boot animation swirl (color based on the system region,
    blue, orange or black). You also have an option to skip the boot animation
    (see note #3). Currently, the interface to pick up a custom color other than the ones
    suggested does not exist. This feature will be available in future versions of the
    custom bootROM.
		
    SEGA License screen skip (default: off):
        Decide whether the Dreamcast displays the SEGA license screen. In any case, the
    IP.BIN initialisation and bootstraps code is still executed to be compatible with
    homebrews that rely on a specific machine state at this point of execution.

    MIL-CD/backup direct boot (default: off):
        Decide whether the system resets when launching a MIL-CD/backup (see note #4).

    Dreamcast main menu (default: 2D perspective):
        Select the perspective and scenery color of the Dreamcast main menu. This feature
    is based on the Puyo Puyo Fever easter-egg that changes the Dreamcast main menu
    perspective from 2D to 3D. Here slightly more options are presented. You can keep the
    2D perspective and choose between a light-grey or dark-blue scenery color or switch
    to the 3D mode, that some people use to call the "3D menu hack" (that is rather a
    hidden feature than a hack). Note that with the 3D perspective, the analog stick and
    the triggers are used the mode the camera.


[+] Notes and limitations
    ~~~~~~~~~~~~~~~~~~~~~

    Note #1:
        If the date/time is not set, the custom bootROM set it for you. In the case a
    GD-ROM disc is inserted, the latter boots right away. However, by design in the
    original bootROM, if it is a MIL-CD/backup disc, you enter in the Dreamcast main menu
    therefore have to manually launch the game. This may be fixed in future versions.

    Note #2:
        Once a protected save has been copied, when you browse your saves via a no-custom
    BIOS, you will notice that the original save file cannot be copied whereas its copy
    can. In fact, the copy-protected flag is not stored in the save file itself but
    rather in the VMU filesystem. That means that the custom bootROM updates and clears
    that flag only when the save is copied to another VMU.

    Note #3:
        The "No boot animation" option works perfectly when using a GD-ROM drive. However
    it may not boot MIL-CD/backup directly if you use ODDEs. I believe the creators of
    ODDEs would be able to easily fix this by issuing a new firmware if necessary.

    Note #4:
        Once the system has detected a GD-ROM, it locks the drive in such way that only
    GD-ROMs can be launched afterwards, unless the system resets. The only reason why you
    would disable the direct boot feature is if you want to boot a MIL-CD or a backup
    after booting a GD-ROM with a GD-ROM drive. Some users have reported this feature
    not working when using USB GD-ROM. As it is working with any GD-ROM drive and GD-EMU,
    I believe the problem is in USB GD-ROM firmware.


[+] Does it work on the real hardware?
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        Yes, sure, as long as the Dreamcast has a BIOS mod and Dreamshell to flash the
    alternate BIOS chip.


[+] Note about the Holly integrity check
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        Those of you that have tried to modify a Dreamcast BIOS probably know that you
    can only get it working on real hardware if the BIOS passes the integrity check done
    by the Holly controller. A retail BIOS uses its 2Mb of data to pass this check. So
    every time you modify something, unless you know the algorithm running in the Holly
    controller, you must flash your Dreamcast and see if it works. If it doesn't, you
    have then to modify some data in the BIOS, flash your Dreamcast again and pray that
    this time your BIOS passes the check.

        Sometime ago, MetalliC made an important discovery: he found a NAOMI beta BIOS
    that uses only 1Kb of data to pass the integrity check. This 1kb of data that
    we call "beta bootstrap" can be injected inside a retail Dreamcast BIOS. By doing so,
    the BIOS passes the check and you can then modify whatever you want in the BIOS,
    except the beta bootstrap of course. MetalliC implemented this mechanism in a BIOS
    shipped with DreamShell.

        So then what? Well, even though this beta bootstrap by-passes the integrity check
    it however does not handle the system reset that is triggered every time you boot a
    MIL-CD/backup. What a pain! This is where my work comes in. With a little of luck, my
    empirical analysis of the integrity check lead me to interesting findings: I found
    a way to modify the beta bootstrap so that it not only passes the integrity check but
    also handles the system reset correctly. I am not giving more details here as people
    interested in the technical aspects will, without a doubt, be able to understand by
    themselves by looking at my BIOS.

	
[+] Does it work with GD-EMU and USB-GDROM?
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        As I do not own a USB-GDROM myself, I cannot test the compatibility. However I
    do test the custom bootROM with both a real GD-ROM drive and a GD-EMU. Other than the
    limitations explained before (see "Notes and limitations"), the custom bootROM is
    fully compatible with GD-ROM drive and GD-EMU.


[+] Is it compatible with all games?
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

	    With the custom bootROM, I try to improve the compatibility with retail games and
    to add new features. Unfortunately, the changes I made in the bootROM break the
    compatibility with some independent games. In order to protect themselves against
    piracy, they use anti-protection mechanisms that rely on specific data that is
    slightly different in this custom bootROM.

    Here is a non-exhaustive list of titles that are not compatible with this custom
    bootROM:
        - Bleemcast! (the 3 of them)
        - Cheat discs such as Action Replay, Game Shark and Code Breaker
        - Pier Solar

        However, I plan to hack and release at least one of those cheat discs compatible
    with this BIOS.


[+] Why using "1.03X" as the version number?
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        The v1.004, v1.011, v1.01c, v1.01d and v1.022 are the only version numbers known
    for the official SEGA bootROM (BIOS). Thus I decided that my custom versions will use
    version numbers starting from v1.030.


[+] Greetings and special thanks to:
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

        - Lars Olsson for his work reverse-engineering the Dreamcast bootROM
        - Link83 for his devkit boot animation hack
        - DC-SWAT team for their DreamShell OS
        - drkIIRaziel and ZeZu for their nullDC emulator
        - Deunan for his great GDEmu board
        - neuroacid for his cool app, GDMenu, and his work to make it compatible with
          this bootROM
        - MetalliC who discovered and dumped the beta bootstrap that now makes my work
          way easier!

    And of course to people who donated and have been supporting my project.

    Thank you to all of you!

_________________________________________________________________________________________

                                                                       jc.dcdev@gmail.com
                                                            japanese-cake.livejournal.com
_________________________________________________________________________________________