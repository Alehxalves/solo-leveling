# Solo-Leveling Otserver

### Server: The Forgotten Server 1.4.2
[Server GitHub Repository](https://github.com/otland/forgottenserver/releases/tag/v1.4.2)

### Client: otclientv8
[otClient GitHub Repository](https://github.com/OTCv8/otclientv8)

### Clone this repository

```bash
git clone https://github.com/Alehxalves/solo-leveling.git
cd ~/solo-leveling
```

## Compiling Server Ubuntu 24.04

### 1. Install Required Libraries

Start by updating your system and installing necessary development packages.

```bash
sudo apt update
sudo apt install -y git cmake build-essential
```
```bash
sudo apt install -y \
    libluajit-5.1-dev \
    libmysqlclient-dev \
    libboost-system-dev \
    libboost-iostreams-dev \
    libboost-locale-dev \
    libboost-json-dev \
    liblua5.3-dev \
    libboost-all-dev \
    libphysfs-dev \
    libssl-dev \
    liblua5.1-0-dev \
    libglew-dev \
    libvorbis-dev \
    libopenal-dev \
    zlib1g-dev \
    libcrypto++-dev \
    libfmt-dev \
    libpugixml-dev
```
### 2. Build the Server and setup database

Building the Server

```bash
cd ~/solo-leveling/solo-server
mkdir build && cd build
cmake ..
make
```

Create Database
```bash
cd ~/solo-leveling/solo-server
```
```bash
sudo apt install -y mysql-server
```
```bash
sudo mysql -u root -p
```
```
CREATE DATABASE `solo-db`;
CREATE USER 'solo_user'@'localhost' IDENTIFIED WITH mysql_native_password BY '3301';
SET GLOBAL log_bin_trust_function_creators = 1;
```
```
USE solo-db;
GRANT ALL PRIVILEGES ON `solo-db`.* TO 'solo_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

```bash
mysql -u solo_user -p solo-db < schema.sql
```

Access db
```
mysql -u solo_user -p
```
```
USE solo_db;
```
If access denied
```
sudo mysql -u root -p
```
```
FLUSH PRIVILEGES;
EXIT;
```
Create Admin
```
INSERT INTO accounts (id, name, password, type)
VALUES (1, 'admin', sha1('3301'), 5);
```
Create Character
```
INSERT INTO players (name, account_id, level, vocation, group_id, town_id, posx, posy, posz)
VALUES ('Admin', 1, 100, 1, 6, 1, 100, 100, 7);
```

### 3. Run the Server

Copy and paste solo-client file created in /build to /otclient

```bash
chmod +x solo-client

./solo-client
```
## Compiling Server Windows

[Compiling TFS Windows](https://forums.otserv.com.br/index.php?%2Fforums%2Ftopic%2F169234-windowsvc2019-compilando-sources-tfs-14-vcpkg%2F)

## Run the Client

Open solo-client folder abd execute otclient_dx.exe
