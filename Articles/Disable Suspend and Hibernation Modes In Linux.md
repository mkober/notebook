Source: https://blog.wijman.net/disable-suspend-and-hibernation-modes-in-linux/

Suspending your system helps save power when you are not using your system. Getting back to using your system requires a simple mouse-click or a tap on any keyboard button. Sometimes, you may be required to press the power button.

But sometimes you don't want your system to suspend or sleep if you are running an application which should stay active.

To avoid this from happening you can disable the suspend/sleep/hibernation daemons.

## Disable Suspend and Hibernation

To disable the daemons use the following command:

```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

Copy

The output will look like:

```bash
Created symlink /etc/systemd/system/sleep.target → /dev/null.
Created symlink /etc/systemd/system/suspend.target → /dev/null.
Created symlink /etc/systemd/system/hibernate.target → /dev/null.
Created symlink /etc/systemd/system/hybrid-sleep.target → /dev/null.
```

Copy

## Verify Daemon Status

To verify the status of the daemons (if they are enabled or disabled) you can run the following command:

```bash
sudo systemctl status sleep.target suspend.target hibernate.target hybrid-sleep.target
```

Copy

The output will look like:

```bash
● sleep.target
     Loaded: masked (Reason: Unit sleep.target is masked.)
     Active: inactive (dead)

● suspend.target
     Loaded: masked (Reason: Unit suspend.target is masked.)
     Active: inactive (dead)

● hibernate.target
     Loaded: masked (Reason: Unit hibernate.target is masked.)
     Active: inactive (dead)

● hybrid-sleep.target
     Loaded: masked (Reason: Unit hybrid-sleep.target is masked.)
     Active: inactive (dead)
```

Copy

## Enable Suspend and Hibernation

To (re-)enable the daemons again you can run the following command:

```bash
sudo systemctl unmask sleep.target suspend.target hibernate.target hyb
```