# initcpio-encryptmulti

initcpio custom hook extended from encrypt hook that allows to specify multiple
encrypted devices before mounting the root filesystem.

## Use case

This hook is intendded to be used in case you need to access more than one
encrypted device to be able to build the root partition, e.g. in a LVM volume
distributed in two encrypted devices.

Note: use this hook only if you need to uncrypt multiple devices to mount the
root partition. For other devices that can be uncrypted  after the root
partition mounted, configure the `/etc/crypttab` file instead.

This hook is an alternative for the process of [Modifying the encrypt hook for
multiple
partitions](https://wiki.archlinux.org/title/Dm-crypt/Specialties#Modifying_the_encrypt_hook_for_multiple_partitions).

## Usage

> Tested during installation of the Arch Linux.

- Copy the `hooks/encryptmulti` into `/etc/initcpio/hooks/`
- Copy the `install/encryptmulti` into `/etc/initcpio/install/`
- Use `encryptmulti` instead of `encrypt` as a hook in the `/etc/mkinitcpio.conf`
- Regenarate your initramfs with `mkinitcpio -P`

When you add the kernel parameter, you can use multiple devices separating then
by `%`. Both `cryptdevice` (singular) and `cryptdevices` (plural) will work.
E.g.:

```
cryptdevices=/dev/sda1:cryptsda%/dev/sdb1:cryptsdb
```

Note: If you have a `cryptkey` configured, this hook will try to use the same
cryptkey for all the devices.

