# Section 6: EC2 Instance Storage

## 44 EBS Overview

What’s an EBS Volume?

- An EBS (Elastic Block Store) Volume is a network drive you can attach
  to your instances while they run
- It allows your instances to persist data, even after their termination
- They can only be mounted to one instance at a time (at the CCP level)
- They are bound to a specific availability zone
- Analogy: Think of them as a “network USB stick”
- Free tier: 30 GB of free EBS storage of type General Purpose (SSD) or
  Magnetic per month

EBS Volume

- It's a network drive (i.e. not a physical drive)

  - It uses the network to communicate the instance, which means there might be a bit of
    latency
  - It can be detached from an EC2 instance and attached to another one quickly

- It's locked to an Availability Zone (AZ)

  - An EBS Volume in us-east-|a cannot be attached to us-east-1b
  - To move a volume across, you first need to snapshot it

- Have a provisioned capacity (size in GBs, and IOPS)

  - You get billed for all the provisioned capacity
  - You can increase the capacity of the drive over time

## 46 EBS Snapshots

EBS Snapshots Features

- EBS Snapshot Archive

  - Move a Snapshot to an "archive tier” that is
    75% cheaper
  - Takes within 24 to 72 hours for restoring the
    archive

- Recycle Bin for EBS Snapshots

  - Setup rules to retain deleted snapshots so you
    can recover them after an accidental deletion
  - Specify retention (from | day to | year)

- Fast Snapshot Restore (FSR)
  - Force full initialization of snapshot to have no
    latency on the first use ($$$)

## 48 AMI Overview

AMI Overview

- AMI = Amazon Machine Image
- AMI are a customization of an EC2 instance
  - You add your own software, configuration, operating system, monitoring...
  - Faster boot / configuration time because all your software is pre-packaged
- AMI are built for a specific region (and can be copied across regions)
- You can launch EC2 instances from:
  - A Public AMI: AWS provided
  - Your own AMI: you make and maintain them yourself
  - An AWS Marketplace AMI: an AMI someone else made (and potentially sells)

## 50 EC2 Instance Store

EC2 Instance Store

- EBS volumes are network drives with good but “limited” performance
- If you need a high-performance hardware disk, use EC2 Instance Store
- Better I/O performance
- EC2 Instance Store lose their storage if they're stopped (ephemeral)
- Good for buffer / cache / scratch data / temporary content
- Risk of data loss if hardware fails
- Backups and Replication are your responsibility

## 51 EBS Volumes Types

EBS Volume Types

- EBS Volumes come in 6 types

  - gp2/ gp3 (SSD): General purpose SSD volume that balances price and performance for a wide variety of workloads
  - io1 / io2 (SSD): Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads
  - st1 (HDD): Low cost HDD volume designed for frequently accessed, throughput-intensive workloads
  - sc1 (HDD): Lowest cost HDD volume designed for less frequently accessed workloads

- EBS Volumes are characterized in Size | Throughput | IOPS (I/O Ops Per Sec)
- When in doubt always consult the AWS documentation — it’s good!
- Only gp2/gp3 and io1/io2 can be used as boot volumes

EBS Volume Types Use cases
General Purpose SSD

- Cost effective storage, low-latency
- System boot volumes, Virtual desktops, Development and test environments
- 1 GiB- 16TiB
- gp3:
  - Baseline of 3,000 IOPS and throughput of 125 MiB/s
  - Can increase IOPS up to |6,000 and throughput up to 1000 MiB/s independently
- gp2:
  - Small gp2 volumes can burst IOPS to 3,000
  - Size of the volume and IOPS are linked, max IOPS is 16,000
  - 3 IOPS per GB, means at 5,334 GB we are at the max IOPS

EBS Volume Types Use cases
Provisioned IOPS (PIOPS) SSD

- Critical business applications with sustained |OPS performance
- Or applications that need more than 16,000 IOPS
- Great for databases workloads (sensitive to storage perf and consistency)
- io1/io2 (4 GiB - 16 TiB):

  - Max PIOPS: 64,000 for Nitro EC2 instances & 32,000 for other
  - Can increase PIOPS independently from storage size
  - io2 have more durability and more IOPS per GiB (at the same price as io1)

- io2 Block Express (4 GiB — 64 TiB):

  - Sub-millisecond latency
  - Max PIOPS: 256,000 with an IOPS:GiB ratio of 1,000:1

- Supports EBS Multi-attach

EBS Volume Types Use cases
Hard Disk Drives (HDD)

- Cannot be a boot volume
- 125 GiB to |6TiB
- Throughput Optimized HDD (st1)

  - Big Data, Data Warehouses, Log Processing
  - Max throughput 500 MiB/s — max IOPS 500

- Cold HDD (sc1):
  - For data that is infrequently accessed
  - Scenarios where lowest cost is important
  - Max throughput 250 MiB/s — max IOPS 250
