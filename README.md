# Home Lab Creation & Kali Linux Installation

## Objective

This project documents my first home lab build and installation of the attacking software Kali Linux - a self-contained virtual ecosystem to gain hands-on experience in cybersecurity tooling and environments, alongside . This foundation helps me test configurations, simulate real-world threats and deepen my understanding in a risk-free space.

### Skills Learned

- Set up and managed virtualised environments using VirtualBox, including VM resource allocation and configuration.
- Designed and implemented an isolated virtual network (Host-Only) to simulate secure, real-world environments.
- Gained hands-on experience with Kali Linux and common security tools such as nmap for reconnaissance and service enumeration.
- Practiced identifying and exploiting vulnerabilities in a deliberately vulnerable system (Metasploitable).
- Strengthened troubleshooting skills by verifying connectivity, resolving network issues, and capturing traffic with Wireshark.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Steps

---

## Starting Out

Before I did anything, I made sure that virtualization was enabled on my machine (Intel VT‑x/AMD‑V in BIOS). Without that, VirtualBox won’t even let you pick 64‑bit systems. I’m on Windows, but the steps are mostly the same on macOS or Linux.

---

## Installing VirtualBox

I went over to the [VirtualBox downloads page](https://www.virtualbox.org/wiki/Downloads) and grabbed the installer for Windows. Install was pretty straightforward — next, next, finish. I also added the Extension Pack so I can use USB 2.0/3.0 later if I need it.

Once it finished, I opened VirtualBox Manager and just saw the empty home screen. *(Ref V1)*

---

## Getting Kali Linux

Next, I needed Kali. I downloaded the installer ISO from [kali.org/get-kali](https://www.kali.org/get-kali/). They have prebuilt VirtualBox images, but I wanted to go through the install myself.

I also ran a checksum (`sha256sum`) against the ISO to double‑check it wasn’t corrupted. Everything matched, so I was good to go. *(Ref K1 shows the boot menu I eventually got to)*

---

## Creating the VM

In VirtualBox, I hit **New** and named it *Kali Linux*. For the type I set **Linux**, version **Debian (64‑bit)**. I gave it 4 GB of RAM and a 60 GB virtual hard drive. I stuck with VDI, dynamically allocated.

After creating it, I tweaked a few settings:

* Bumped the CPUs up to 2.
* Set video memory to 128 MB.
* Left networking as NAT (good enough to get internet inside the VM).

Finally, I attached the Kali ISO to the virtual CD drive so I could boot from it. *(Ref V2 and V3 are the wizard screens I saw here)*

---

## Installing Kali

Booting up, I got the Kali boot menu and chose **Graphical install**. From there it was a bunch of setup screens:

* Picked English/UK keyboard.
* Gave the VM the hostname `kali`.
* Created a normal user account and password.
* For partitioning, I just went with **Guided – use entire disk** since it’s only a VM.
* Installed GRUB to the main disk so it would actually boot.

After rebooting, I had to remember to **remove the ISO** from the virtual CD drive. Otherwise, it kept looping back to the installer. Once I did that, it booted into Kali just fine. *(Ref K2–K5 cover these bits)*

---

## First Boot

On the first login, I ran:

```bash
sudo apt update && sudo apt full-upgrade -y
```

Then I added VirtualBox Guest Additions with:

```bash
sudo apt install -y virtualbox-guest-x11 virtualbox-guest-utils virtualbox-guest-dkms
sudo reboot
```

That fixed the resolution and allowed me to resize the VM window properly. *(Ref K6 shows the Kali desktop after this)*

I also took a snapshot right then and called it “Fresh Install” — just in case I mess anything up later, I can roll back. *(Ref V5)*

---

## Networking Notes

By default, NAT worked fine to get updates. Later, I might add a Host‑Only adapter so I can run multiple VMs and have them talk to each other in an isolated network. That’s for when I spin up something like Metasploitable.

---

## Troubleshooting I Hit

* At first I didn’t see the 64‑bit option in VirtualBox — turns out Hyper‑V was enabled on my Windows install. Once I disabled it, 64‑bit options showed up.
* I got a black screen once with 3D acceleration turned on, so I disabled it and it’s been fine.
* Screen size was stuck small until Guest Additions were properly installed.

---

## Wrapping Up

So at this point, I’ve got a working Kali VM on VirtualBox with snapshots, guest additions, and updates. Next on my list is to experiment with network topologies and maybe bring another VM online as a target.

---

## Screenshots I Collected

For reference, here are the images I linked earlier (all are GPL‑licensed, so safe to include in my repo):

* **Ref V1 – VirtualBox Manager home**
* **Ref V2 – New VM wizard**
* **Ref V3 – Disk setup wizard**
* **Ref V4 – ISO attached to VM**
* **Ref K1 – Kali boot menu**
* **Ref K2 – Language screen**
* **Ref K3 – Hostname screen**
* **Ref K4 – Partitioning screen**
* **Ref K5 – GRUB install**
* **Ref K6 – Kali desktop**
* **Ref V5 – Snapshot manager**

