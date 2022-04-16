# Project Workflow

## Setting up VM environment.

Step 1 - Two EC2 instances were spin up for the project.

![IMG_9705](https://user-images.githubusercontent.com/93732510/163679606-f6ab2f46-8868-48cf-9af7-566f055bfa08.jpg)

Step 2 - EBS volumes were created and attached to the webserver instance.

![IMG_9706](https://user-images.githubusercontent.com/93732510/163679665-ac0153f6-9f68-440e-a62e-761841b21de6.jpg)

## Preparing the Webserver

Step 1 - After logging into the server, the block devices attached to the are inspected.

![IMG_9709](https://user-images.githubusercontent.com/93732510/163679938-9c84dad1-e0a7-4707-bb04-12f0f7e4b51d.jpg)

Step 2 - Single partition is then created on each of the 3 disks.

![IMG_9714](https://user-images.githubusercontent.com/93732510/163680068-c2473c00-58cc-43c6-aed3-0e9a208bf15f.jpg)

Step 3 - The newly created partition is now inspected.

![IMG_9715](https://user-images.githubusercontent.com/93732510/163680140-bfab9412-b23f-4d7a-8a97-6814daaef090.jpg)

Step 4 - lvm2 package is installed and available partition is then checked.

![IMG_9716](https://user-images.githubusercontent.com/93732510/163680229-485538a1-54b2-4fd8-8a51-3420a494421e.jpg)

![IMG_9717](https://user-images.githubusercontent.com/93732510/163680260-4da66b9d-9b6b-4997-9cc0-0571095c8ca6.jpg)

Step 5 Physical volumes to be used by lvm are created and then added to a group.

![IMG_9719](https://user-images.githubusercontent.com/93732510/163680304-faced721-65c6-494a-8c87-e1ac4d9eece8.jpg)

Step 6 - Two logical volumes are created and the physical volume size are split into 2.

![IMG_9720](https://user-images.githubusercontent.com/93732510/163680547-6047bf06-b8b1-49ef-9c1a-32e57711ee52.jpg)

Step 7 - The logical volumes are formatted with ext4 filesystem.

![IMG_9721](https://user-images.githubusercontent.com/93732510/163680642-e4d42ff6-215a-4d75-81b8-92ab79af4d0b.jpg)

Step 8 - A directory to store website files and backup log data are created and then the logical volumes are mounted.

![IMG_9723](https://user-images.githubusercontent.com/93732510/163680805-83631c3a-e391-424c-abab-9d2f376c36fd.jpg)

Step 9 - The /etc/fstab file is updated so that the mount configuration will persist after restart of server.

![IMG_9725](https://user-images.githubusercontent.com/93732510/163680897-8910e2c6-ade5-4e4e-a82f-a5e9f0f66bc2.jpg)

![IMG_9726](https://user-images.githubusercontent.com/93732510/163680924-4be4afb0-b004-4062-a049-a89821485541.jpg)

Step 10 - The configuration is tested and the daemon reloaded.

![IMG_9729](https://user-images.githubusercontent.com/93732510/163681095-00c7ceb7-fa0d-4c22-aa1f-2779672289ae.jpg)

## Preparing the database server

The db server was logged into and repeated the same steps for webserver.

## Installing Wordpress

Step 1 - Apache is installed and all its dependencies.

![IMG_9731](https://user-images.githubusercontent.com/93732510/163681225-b37a9cab-78be-460f-b604-5e2ee7a49d76.jpg)

Step 2 - Wordpress downloaded copied into /var/www/html and SElinux policies configured according to documentation.

![IMG_9736](https://user-images.githubusercontent.com/93732510/163681372-3e5970dc-317c-4b00-b8d4-ec31e81b42f6.jpg)

![IMG_9737](https://user-images.githubusercontent.com/93732510/163681518-8a71dbf0-0ba5-4c04-a069-3178872d006f.jpg)

##  Installing MYSQL on DB server

Step 1 - Mysql server was installed, enabled and status checked. 

![IMG_9738](https://user-images.githubusercontent.com/93732510/163681613-1f27f281-dc90-4c5c-9a88-a71aefaaf366.jpg)

![IMG_9740](https://user-images.githubusercontent.com/93732510/163681653-5d057b51-486d-41ec-942c-c8dd24453995.jpg)

## Configuring DB to work with Wordpress

Step 1  - Mysql was logged into as sudo and database + user created. 

![IMG_9742](https://user-images.githubusercontent.com/93732510/163681696-7ad9b2e0-47e7-4a30-a698-c27b3105db12.jpg)

Step 2 - Port 3306 was open to allow traffic from webserver private IP.

![IMG_9743](https://user-images.githubusercontent.com/93732510/163682218-0401a842-474c-42d2-b4a6-6602d946b9e8.jpg)

Step 3 - Mysql-client is installed, enabled and status checked on the webserver.

![IMG_9745](https://user-images.githubusercontent.com/93732510/163682472-b431ac9e-d07d-4b45-b3e6-f9c35b562828.jpg)

![IMG_9748](https://user-images.githubusercontent.com/93732510/163682489-e55c004c-4267-46bd-8255-fda7ea863241.jpg)

Step 4 - Configuration file on db sever was updated with the webserver private IP for persistence after restart.

![IMG_9746](https://user-images.githubusercontent.com/93732510/163682558-8d066975-2a1c-4fe1-b2bd-1ac4352ef735.jpg)

Step 5 - Database information was updated on the webserver so we can use the info to connect to db server remotely.

![IMG_9749](https://user-images.githubusercontent.com/93732510/163682675-ec113b66-cd23-403e-b1d7-44b6dbee4fbd.jpg)

Step 6 - DB server was connected to remotely with the user information and sql command was run by the user with assigned privilege.

![IMG_9750](https://user-images.githubusercontent.com/93732510/163682751-54d8524f-4ce8-4795-8bb9-c5d52b87001c.jpg)

Step 7 - Ownership to website files was assigned to apache and configuration done.

![IMG_9751](https://user-images.githubusercontent.com/93732510/163682892-a557168f-cc8c-412a-80a7-b0e344321752.jpg)

![IMG_9752](https://user-images.githubusercontent.com/93732510/163682912-23acb313-4e6e-4f4b-b8e7-af37918b75c4.jpg)

Step 8 - Port 80 webserver is opened and the website accessed via browser.

![IMG_9753](https://user-images.githubusercontent.com/93732510/163682996-8ef9232a-4313-45eb-811f-762e56ff3e73.jpg)

![IMG_9754](https://user-images.githubusercontent.com/93732510/163683021-d1a23670-8233-4634-8efa-8d4fb881ec15.jpg)

