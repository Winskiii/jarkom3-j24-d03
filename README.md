# jarkom3-j24-d03
[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/1zoHyFGp)
| Name           | NRP        | Kelas     |
| ---            | ---        | ----------|
| Winston Juliand Sitranata | 5025221285 | Jaringan Komputer (D) |
| Abimanyu Danendra Andarfebano | 5025231182 | Jaringan Komputer (D) |

## Put your topology config image here!
`Put image in here`
![image](https://github.com/user-attachments/assets/eef97d58-c6c5-4c8f-82bc-cd38ab2553e3)


<br>

Testing Report: 

https://drive.google.com/drive/folders/1Ujdm297k_fenxHqZbzZ5rtCMPxB2e9R1?usp=drive_link

## Soal 0

> Pada perlombaan akhir tahun kali ini, semua worker dan client ikut serta di dalamnya sebagai perwakilan dari masing-masing asrama. Persiapan yang dilakukan untuk perlombaan ini adalah dengan setup semua network configuration yang sesuai dengan tabel peran diatas. Khusus untuk client menggunakan konfigurasi dari DHCP Server.

> _For the end-of-year competition, all the workers and clients participate, representing their respective houses. The preparation includes setting up the network configuration as per the table above, with clients using DHCP Server configuration_

**Answer**

- Dumbledore:

  ```
  auto eth0
  iface eth0 inet dhcp
  
  auto eth1
  iface eth1 inet static
  	address 10.116.1.1
  	netmask 255.255.255.0
  
  auto eth2
  iface eth2 inet static
  	address 10.116.2.1
  	netmask 255.255.255.0
  
  auto eth3
  iface eth3 inet static
  	address 10.116.3.1
  	netmask 255.255.255.0
  
  auto eth4
  iface eth4 inet static
  	address 10.116.4.1
  	netmask 255.255.255.0
  
  auto eth5
  iface eth5 inet static
  	address 10.116.5.1
  	netmask 255.255.255.0
  
  auto eth6
  iface eth6 inet static
  	address 10.116.6.1
  	netmask 255.255.255.0
  
  up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.116.0.0/16
  ```

- SeverusSnape:

  ```
  auto eth0
  iface eth0 inet static
	address 10.116.3.2
	netmask 255.255.255.0
	gateway 10.116.3.1
  ```

- McGonagall:

  ```
  auto eth0
  iface eth0 inet static
	address 10.116.3.3
	netmask 255.255.255.0
	gateway 10.116.3.1
  ```

- Hagrid:

  ```
  auto eth0
  iface eth0 inet static
  	address 10.116.4.2
  	netmask 255.255.255.0
  	gateway 10.116.4.1
  ```

- Voldemort:

  ```
  auto eth0
  iface eth0 inet static
  	address 10.116.4.3
  	netmask 255.255.255.0
  	gateway 10.116.4.1
  ```

- Dementor:

  ```
  auto eth0
  iface eth0 inet static
  	address 10.116.4.4
  	netmask 255.255.255.0
  	gateway 10.116.4.1
  ```

- HarryPotter:

  ```
  auto eth0
  iface eth0 inet static
  	address 10.116.1.2
  	netmask 255.255.255.0
  	gateway 10.116.1.1
  ```

- RonWeasley:

  ```
  auto eth0
  iface eth0 inet static
  	address 10.116.1.3
  	netmask 255.255.255.0
  	gateway 10.116.1.1
  ```

- HermioneGranger:

  ```
  auto eth0
  iface eth0 inet static
  	address 10.116.1.4
  	netmask 255.255.255.0
  	gateway 10.116.1.1
  ```

- LunaLovegood:

  ```
  auto eth0
  iface eth0 inet static
  	address 10.116.6.4
  	netmask 255.255.255.0
  	gateway 10.116.6.1
  ```

- FiliusFlitwick:

  ```
  auto eth0
  iface eth0 inet static
  	address 10.116.6.3
  	netmask 255.255.255.0
  	gateway 10.116.6.1
  ```

- ChoChang:

  ```
  auto eth0
  iface eth0 inet static
  	address 10.116.6.2
  	netmask 255.255.255.0
  	gateway 10.116.6.1
  ```

- DracoMalfoy:

  ```
  auto eth0
  iface eth0 inet dhcp
  ```

- AstoriaGreengrass:

  ```
  auto eth0
  iface eth0 inet dhcp
  ```

- SusanBones:

  ```
  auto eth0
  iface eth0 inet dhcp
  ```

- HannahAbbott:

  ```
  auto eth0
  iface eth0 inet dhcp
  ```

## Soal 1

> Melakukan registrasi subdomain untuk PHP worker bernama gryffindor.hogwarts.yyy.com yang mengarah ke alamat IP load balancer Voldemort dan untuk laravel worker bernama ravenclaw.hogwarts.yyy.com yang mengarah ke alamat IP load balancer Dementor. Seluruh domain ini berkumpul dalam suatu ruang atau folder bernama hogwarts

> _Registering subdomains for the PHP workers named gryffindor.hogwarts.yyy.com, pointing to the IP Voldemort load balancer, and for the Laravel workers named ravenclaw.hogwarts.yyy.com, pointing to the IP Dementor load balancer. All domains are gathered in a folder named "hogwarts."_

**Answer:**

- Screenshot

![image](https://github.com/user-attachments/assets/3a0b1a24-096d-4c17-9ea4-8a350f6b3790)

![image](https://github.com/user-attachments/assets/ebb6f6e9-d727-4166-964f-cdca7da8478c)

- Configuration

```
echo "nameserver 192.168.122.1" > /etc/resolv.conf

apt-get update

apt-get install bind9 -y

echo '
zone "hogwarts.D03.com" {
	type master;
	file "/etc/bind/hogwarts/hogwarts.D03.com";
};
' >> /etc/bind/named.conf.local

mkdir /etc/bind/hogwarts

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     hogwarts.D03.com. root.hogwarts.D03.com. (
			2023110101    ; Serial
			604800        ; Refresh
			86400         ; Retry
			2419200       ; Expire
			604800 )      ; Negative Cache TTL
;
@               IN      NS      hogwarts.D03.com.
@               IN      A       10.116.4.3 ; IP Voldemort
www             IN      CNAME   hogwarts.D03.com.
gryffindor      IN      A       10.116.4.3 ; IP Voldemort
ravenclaw       IN      A       10.116.4.4 ; IP Dementor
' > /etc/bind/hogwarts/hogwarts.D03.com

service named restart
```
- Explanation

  `Put your explanation in here`

<br>

## Soal 2

> Memberikan ketentuan khusus untuk DracoMalfoy dan AstoriaGreengrass yang mendapat range IP dari [Prefix IP].2.64 - [Prefix IP].2.65 dan [Prefix IP].2.100 - [Prefix IP].2.101

> Selain itu, untuk HannahAbbott dan SusanBones mendapat range IP dari [Prefix IP].5.50 - [Prefix IP].5.51 dan [Prefix IP].5.155 - [Prefix IP].5.156.


> _Special provisions are given to DracoMalfoy and AstoriaGreengrass, who are assigned the IP range from [Prefix IP].2.64 - [Prefix IP].2.65 and [Prefix IP].2.100 - [Prefix IP].2.101._

> _Additionally, HannahAbbott and SusanBones are assigned the IP range from [Prefix IP].5.50 - [Prefix IP].5.51 and [Prefix IP].5.155 - [Prefix IP].5.156._

**Answer:**

- Screenshot

  ![image](https://github.com/user-attachments/assets/24f27292-e3d5-482c-80e8-6bdafddeaea9)

  ![image](https://github.com/user-attachments/assets/013c2d25-00f1-4fac-91e4-0a7277f94e10)

  ![image](https://github.com/user-attachments/assets/c684803f-2817-4c4c-bda3-3829ca79dbe3)

  ![image](https://github.com/user-attachments/assets/159a77a4-be7d-4f2f-a5ee-62bf3ded6e64)

- Configuration:

	Dumbledor:
	```
	iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.116.0.0/16

	apt-get update
	
	apt-get install isc-dhcp-relay -y
	
	service isc-dhcp-relay start
	
	echo '
	# Defaults for isc-dhcp-relay initscript
	# sourced by /etc/init.d/isc-dhcp-relay
	# installed at /etc/default/isc-dhcp-relay by the maintainer scripts
	
	#
	# This is a POSIX shell fragment
	#
	
	# What servers should the DHCP relay forward requests to?
	SERVERS="10.116.3.2"
	
	# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
	INTERFACES="eth1 eth2 eth3 eth4 eth5 eth6"
	
	# Additional options that are passed to the DHCP relay daemon?
	OPTIONS=""
	' > /etc/default/isc-dhcp-relay
	
	echo '
	net.ipv4.ip_forward=1
	' >> /etc/sysctl.conf
	
	service isc-dhcp-relay restart
	
	```
	
	SeverusSnape:
	```
	echo "nameserver 192.168.122.1" > /etc/resolv.conf
	
	apt-get update
	
	apt-get install isc-dhcp-server -y
	
	echo '
	# Defaults for isc-dhcp-server (sourced by /etc/init.d/isc-dhcp-server)
	
	# Path to dhcpd'\''s config file (default: /etc/dhcp/dhcpd.conf).
	#DHCPDv4_CONF=/etc/dhcp/dhcpd.conf
	#DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf
	
	# Path to dhcpd'\''s PID file (default: /var/run/dhcpd.pid).
	#DHCPDv4_PID=/var/run/dhcpd.pid
	#DHCPDv6_PID=/var/run/dhcpd6.pid
	
	# Additional options to start dhcpd with.
	#       Don't use options -cf or -pf here\;' use DHCPD_CONF/ DHCPD_PID instead
	#OPTIONS=""
	
	# On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
	#       Separate multiple interfaces with spaces, e.g. "eth0 eth1".
	INTERFACESv4="eth0"
	INTERFACESv6=""
	' > /etc/default/isc-dhcp-server
	
	echo '
	subnet 10.116.2.0 netmask 255.255.255.0 {
	    option routers 10.116.2.1;
	    option domain-name-servers 10.116.3.3;
	
	    range 10.116.2.64 10.116.2.65;
	
	    range 10.116.2.100 10.116.2.101;
	}
	
	subnet 10.116.5.0 netmask 255.255.255.0 {
	    option routers 10.116.5.1;
	    option domain-name-servers 10.116.3.3;
	
	    range 10.116.5.50 10.116.5.51;
	
	    range 10.116.5.155 10.116.5.156;
	}
	
	subnet 10.116.3.0 netmask 255.255.255.0 {
	}
	' >> /etc/dhcp/dhcpd.conf
	
	service isc-dhcp-server restart
	```
	
	
	  

- Explanation

  ```
  	Konfigurasi DHCP server pada node SeverusSnape.
	Install package isc-dhcp-server.
	Ubah isi file '/etc/default/isc-dhcp-server' dengan INTERFACES eth0 (interface dari SeverusSnape menuju ke switchnya, yaitu eth0).
	Ubah isi file '/etc/dhcp/dhcpd.conf' dengan  menambahkan subnet subnet client yang memerlukan IP dinamis dan tambahkan subnet dari DHCP server itu sendiri.
	Melakukan restart isc-dhcp-server.
	Untuk tahap 5 dan seterusnya, kita menambahkan konfigurasi DHCP Relay pada node Dumbledore.
	
	Install package isc-dhcp-relay.
	Melakukan start isc-dhcp-relay.
	ubah isi file '/etc/default/isc-dhcp-relay' untuk menambahkan IP DHCP-Server dan interface-interface client dan interface dhcp server (eth3).
	Ubah isi file '/etc/sysctl.conf' untuk menambahkan forwarding packet.
	Melakukan restart isc-dhcp-relay. ```

<br>

## Soal 3

> Khusus untuk HermioneGranger yang berada di switch 1 mendapat range IP dari
[Prefix IP].1.10 - [Prefix IP].1.15 dan [Prefix IP].1.20 - [Prefix IP].1.25

> Khusus untuk ChoChang yang berada di switch 6 mendapat range IP dari 
[Prefix IP].6.10 - [Prefix IP].6.15 dan [Prefix IP].6.20 - [Prefix IP].6.25


> _HermioneGranger, who is on switch 1, is assigned the IP range from [Prefix IP].1.10 - [Prefix IP].1.15 and [Prefix IP].1.20 - [Prefix IP].1.25._

> _ChoChang, who is on switch 6, is assigned the IP range from [Prefix IP].6.10 - [Prefix IP].6.15 and [Prefix IP].6.20 - [Prefix IP].6.25._

**Answer:**

- Screenshot

  ![image](https://github.com/user-attachments/assets/148a92e5-8d22-4a8e-b05c-a4f13a00eac3)

  ![image](https://github.com/user-attachments/assets/904ae56a-4c4e-45c3-ac3d-a530a8d77ee2)


- Configuration

```
echo '
subnet 10.116.1.0 netmask 255.255.255.0 {
    option routers 10.116.1.1;
    option domain-name-servers 10.116.3.3;

    range 10.116.1.10 10.116.1.15;

    range 10.116.1.20 10.116.1.25;
}

subnet 10.116.6.0 netmask 255.255.255.0 {
    option routers 10.116.6.1;
    option domain-name-servers 10.116.3.3;

    range 10.116.6.10 10.116.6.15;

    range 10.116.6.20 10.116.6.25;
}
' >> /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```
- Explanation
```
  	Config Node SeverusSnape (DHCP Server):
	Tambahkan konfigurasi subnet baru yang mengarah pada switch ke-1 dan switch ke-6, pada file '/etc/dhcp/dhcpd.conf'.
	Matikan service dhcpd terlebih dahulu dengan menghapus file '/var/run/dhcpd.pid'.
	Restart isc-dhcp-server.
```
<br>

## Soal 4

> Menetapkan batasan waktu untuk DHCP server dalam peminjaman alamat IP untuk client melalui switch 2 selama 5 menit sedangkan client yang melalui switch 5 selama 20 menit. Untuk switch 1 dan switch 6 memiliki batas waktu 10 menit. Alokasi waktu maksimal peminjaman alamat IP selama 100 menit. 

> _The DHCP server's lease time for IP addresses is set as follows: Clients connected through switch 2 have a lease time of 5 minutes, Clients connected through switch 5 have a lease time of 20 minutes, Switches 1 and 6 have a lease time of 10 minutes, The maximum lease time for IP addresses is set at 100 minutes._

**Answer:**

- Screenshot

  Switch 2:

  ![image](https://github.com/user-attachments/assets/f6ce7dcb-1250-4035-ae16-1721f5a34b07)

  Switch 5:

  ![image](https://github.com/user-attachments/assets/14559855-7f2e-4bde-b147-b92432e39716)

  Switch 1:

  ![image](https://github.com/user-attachments/assets/ddfd0b12-eb88-43a6-b78b-58e7705fd79f)

  Switch 6:

  ![image](https://github.com/user-attachments/assets/9d36ede6-ee19-4cde-a886-d4160076c1ee)

- Configuration

```
echo '
option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style none;

subnet 10.116.2.0 netmask 255.255.255.0 {
    option routers 10.116.2.1;
    option domain-name-servers 10.116.3.3;

    range 10.116.2.64 10.116.2.65;

    range 10.116.2.100 10.116.2.101;

    default-lease-time 300;
    max-lease-time 6000;
}

subnet 10.116.5.0 netmask 255.255.255.0 {
    option routers 10.116.5.1;
    option domain-name-servers 10.116.3.3;

    range 10.116.5.50 10.116.5.51;

    range 10.116.5.155 10.116.5.156;

    default-lease-time 1200;
    max-lease-time 6000;
}

subnet 10.116.3.0 netmask 255.255.255.0 {
}

subnet 10.116.1.0 netmask 255.255.255.0 {
    option routers 10.116.1.1;
    option domain-name-servers 10.116.3.3;

    range 10.116.1.10 10.116.1.15;

    range 10.116.1.20 10.116.1.25;

    default-lease-time 600;
    max-lease-time 6000;
}

subnet 10.116.6.0 netmask 255.255.255.0 {
    option routers 10.116.6.1;
    option domain-name-servers 10.116.3.3;

    range 10.116.6.10 10.116.6.15;

    range 10.116.6.20 10.116.6.25;

    default-lease-time 600;
    max-lease-time 6000;
}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

- Explanation

  `Konfigurasi Node SeverusSnape (DHCP Server):
	Ubah default-lease-time dan max-lease-time pada masing-masing konfigurasi subnet di file '/etc/dhcp/dhcpd.conf'.
	Hapus file '/var/run/dhcpd.pid' lalu restart service isc-dhcp-server.`

<br>

## Soal 5

> Memastikan bahwa semua CLIENT, HermioneGranger, dan ChoChang harus menggunakan konfigurasi dari DHCP server, menerima DNS dari Professor McGonagall dan dapat akses internet. Khusus untuk HermioneGranger dan ChoChang mendapatkan IP Statis dari DHCP dengan [Prefix IP].x.14. hint: fixed address


> _Ensure that all CLIENT, HermioneGranger, and ChoChang use DHCP server configurations, receive DNS from Professor McGonagall, and can access the internet. HermioneGranger and ChoChang must receive static IPs from DHCP with the address [Prefix IP].x.14 (hint: fixed address)._

**Answer:**

- Screenshot

  HermioneGranger:

  ![image](https://github.com/user-attachments/assets/7702a77b-14a8-44f5-a6e3-23a07b858171)

  ChoChang:

  ![image](https://github.com/user-attachments/assets/c4996d3b-6862-4899-930e-b7bf575adea8)

- Configuration
SeverusSnape:
```
echo '
host HermioneGranger {
    hardware ethernet 16:0a:61:74:e3:5c;
    fixed-address 10.116.1.14;
}

host ChoChang {
    hardware ethernet 7e:ba:b6:9b:95:8c;
    fixed-address 10.116.6.14;
}
' >> /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

McGonagall:
```
echo '
options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0'\''s placeholder.

        forwarders {
            192.168.122.1;
        };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;
        allow-query{any;};

        listen-on-v6 { any; };
};
' > /etc/bind/named.conf.options

service named restart
```
- Explanation

  ```
  Konfigurasi Node SeverusSnape (DHCP Server):
	Atur fixed address  node HermioneGranger & node ChoChang. Konfigurasi subnet pada kedua node tersebut jangan dihapus agar tidak terjadi error
	Ubah settings pada file '/etc/dhcp/dhcpd.conf' lalu restart isc-dhcp-server.
`

<br>

## Soal 6

> Dimulai dari asrama Gryffindor yang menjadi PHP worker, mereka harus melakukan deployment untuk website berikut menggunakan PHP 7.4.

> _The Gryffindor house, represented by the PHP workers, must deploy the following website using PHP 7.4._

**Answer:**

- Screenshot
  `Put your screenshot in here`
  ![image](https://github.com/user-attachments/assets/833d9ec1-657e-4d8f-a6df-c7bf50b0dbbe)


- Configuration
  Script Node Gryffindor House HarryPotter & RonWeasley & HermioneGranger (PHP Worker)
  ```
  	apt-get update 
	apt install nginx php php-fpm unzip -y
	
	rm -r /var/www/html/*
	
	wget -O /root/temp "https://drive.google.com/uc?export=download&id=17R4Zcxm3emHq21WdMJzSfCxO8FHqvATM"
	
	unzip /root/temp -d /var/www/html/
	
	rm /root/temp
	
	service nginx start
	
	echo '
	server {

	listen 80;

	root /var/www/html;

	index index.php index.html index.htm;
	server_name _;

	location / {
		try_files $uri $uri/ /index.php?$query_string;
	}

	# pass PHP scripts to FastCGI server
	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
	}

	location ~ /\.ht {
		deny all;
		}
	
		error_log /var/log/nginx/html_error.log;
		access_log /var/log/nginx/html_access.log;
}
' > /etc/nginx/sites-available/default

service php7.4-fpm start
service nginx restart

 
- Explanation

  `Install Package PHP, nginx, php-fm 7.4. Download folder dan file yang sudah diberikan lewat zip lalu mengunzipnya dengan command wget dan unzip. Start PHP dan restart nginx. Pada keempat client lakukan apt-get update dan install lynx nya untuk dapat membuka lynx webserver php yang sudah dibuat pada worker. Lakukan lynx 10.116.1.2 atau lynx 10.116.1.3 dan lynx 10.116.1.4`

<br>

## Soal 7

> Khusus perlombaan ini, Voldemort sudah jinak dan dia menjadi load balancer untuk para penghuni asrama Gryffindor yang menjadi worker PHP. Aturlah agar Voldemort dapat membagi pekerjaan kepada worker PHP secara optimal. Sebagai pengetesan awal, terapkan algoritma round robin dan lakukan test index.php menggunakan apache benchmark dengan 1000 request dan 100 request/second. Lakukan test sebanyak 3 kali lalu hitung rata-rata dan standar deviasi dari time/request

> _Voldemort, who is now reformed, becomes the load balancer for the Gryffindor PHP workers. Optimize Voldemort to distribute tasks to the PHP workers. For the initial test, apply the round-robin algorithm and test it to the index.php page using Apache Benchmark with 1,000 requests and 100 requests/second. Do the test 3 times and calculate the mean and standard deviation of time/request._

**Answer:**

- Configuration

1. Pada HarryPoter, HermioneGranger, RonWasley:
```
apt-get install htop -y
```

2. Voldemort
```
echo "nameserver 10.116.3.3" > /etc/resolv.conf

apt-get update
apt-get install nginx -y

echo '
upstream gryffindor  {
    server 10.116.1.14;
    server 10.116.1.2;
    server 10.116.1.3;
}

server {
    listen 80;
    server_name gryffindor.hogwarts.D03.com;

    location / {
        proxy_pass http://gryffindor;
    }
}
' > /etc/nginx/sites-available/lb-gryffindor

ln -s /etc/nginx/sites-available/lb-gryffindor /etc/nginx/sites-enabled

service nginx restart

apt-get install htop -y
```

3. Pada Client:
```
apt-get update && apt-get install apache2-utils -y

mkdir /root/benchmark && cd /root/benchmark

ab -n 1000 -c 100 -g out.data1 http://gryffindor.hogwarts.D03.com/
ab -n 1000 -c 100 -g out.data2 http://gryffindor.hogwarts.D03.com/
ab -n 1000 -c 100 -g out.data3 http://gryffindor.hogwarts.D03.com/
```

- Explanation

  ```
  Node Voldemort (Load Balancer):
	Install nginx.
	Tambah konfigurasi load balancer dengan menggunakan metode round robin pada '/etc/nginx/sites-available/default'
	nameserver domain gryffindor.
	Nginx restart
  
	Pada Node DracoMalfoy (Client):
	Install package apache2-utils untuk keperluan load testing.
	Apache benchmark
  
	Pada Node PHP Worker:
	Install htop untuk mengawasi resource dari server pada load testing client.
``


<br>

## Soal 8

> Dalam penilaian akhir tahun ini, dibutuhkan algoritma terbaik, cobalah tes 3 algoritma load balancer dengan menggunakan jmeter. Jmeter perlu melakukan login, akses home, dan terakhir logout. Lakukan test dengan 300 thread dan 3 sec ramp up period. Lakukan test sebanyak 3 kali per algoritma, lalu hitung rata-rata dan standar deviasi dari response time. (username: wingardium, password: leviosa)


> _For the final assessment, try three different load-balancing algorithms using JMeter with 300 threads and a 3-second ramp-up period. Jmeter have to be able to login, access homepage, and logout. Do the test 3 times for each algorithm, then calculate the mean and standard deviation of response time. (username: wingardium, password: leviosa)_

**Answer:**

- Configuration
1. Client:
-8a:
```
apt-get install zip -y
apt-get install openjdk-11-jre -y

mkdir /root/jmeter-tests

cd apache-jmeter-5.6.3/bin

echo '
<?xml version="1.0" encoding="UTF-8"?>
<jmeterTestPlan version="1.2" properties="5.0" jmeter="5.6.3">
  <hashTree>
    <TestPlan guiclass="TestPlanGui" testclass="TestPlan" testname="Test Plan">
      <elementProp name="TestPlan.user_defined_variables" elementType="Arguments" guiclass="ArgumentsPanel" testclass=">        <collectionProp name="Arguments.arguments"/>
      </elementProp>
    </TestPlan>
    <hashTree>
      <ThreadGroup guiclass="ThreadGroupGui" testclass="ThreadGroup" testname="Gryffindor">
        <intProp name="ThreadGroup.num_threads">300</intProp>
        <intProp name="ThreadGroup.ramp_time">3</intProp>
        <boolProp name="ThreadGroup.same_user_on_next_iteration">true</boolProp>
        <stringProp name="ThreadGroup.on_sample_error">continue</stringProp>
        <elementProp name="ThreadGroup.main_controller" elementType="LoopController" guiclass="LoopControlPanel" testcl>
          <stringProp name="LoopController.loops">3</stringProp>
          <boolProp name="LoopController.continue_forever">false</boolProp>
        </elementProp>
     </ThreadGroup>
      <hashTree>
        <HTTPSamplerProxy guiclass="HttpTestSampleGui" testclass="HTTPSamplerProxy" testname="HTTP Request">
          <stringProp name="HTTPSampler.domain">gryffindor.hogwarts.D03.com</stringProp>
          <stringProp name="HTTPSampler.protocol">http</stringProp>
          <stringProp name="HTTPSampler.path">/php/logout.php</stringProp>
          <boolProp name="HTTPSampler.follow_redirects">true</boolProp>
          <stringProp name="HTTPSampler.method">GET</stringProp>
          <boolProp name="HTTPSampler.use_keepalive">true</boolProp>
          <boolProp name="HTTPSampler.postBodyRaw">false</boolProp>
          <elementProp name="HTTPsampler.Arguments" elementType="Arguments" guiclass="HTTPArgumentsPanel" testclass="Ar>
            <collectionProp name="Arguments.arguments"/>
          </elementProp>
        </HTTPSamplerProxy>
        <hashTree/>
        <HTTPSamplerProxy guiclass="HttpTestSampleGui" testclass="HTTPSamplerProxy" testname="HTTP Request">
          <stringProp name="HTTPSampler.domain">gryffindor.hogwarts.D03.com</stringProp>
          <stringProp name="HTTPSampler.protocol">http</stringProp>
          <stringProp name="HTTPSampler.path">/php/home.php</stringProp>
          <boolProp name="HTTPSampler.follow_redirects">true</boolProp>
          <stringProp name="HTTPSampler.method">GET</stringProp>
          <boolProp name="HTTPSampler.use_keepalive">true</boolProp>
          <boolProp name="HTTPSampler.postBodyRaw">false</boolProp>
          <elementProp name="HTTPsampler.Arguments" elementType="Arguments" guiclass="HTTPArgumentsPanel" testclass="Ar>
            <collectionProp name="Arguments.arguments"/>
           </elementProp>
        </HTTPSamplerProxy>
        <hashTree/>
        <HTTPSamplerProxy guiclass="HttpTestSampleGui" testclass="HTTPSamplerProxy" testname="HTTP Request">
          <stringProp name="HTTPSampler.domain">gryffindor.hogwarts.D03.com</stringProp>
          <stringProp name="HTTPSampler.protocol">http</stringProp>
          <stringProp name="HTTPSampler.path">/php/login.php</stringProp>
          <boolProp name="HTTPSampler.follow_redirects">true</boolProp>
          <stringProp name="HTTPSampler.method">POST</stringProp>
          <boolProp name="HTTPSampler.use_keepalive">true</boolProp>
          <boolProp name="HTTPSampler.postBodyRaw">false</boolProp>
          <elementProp name="HTTPsampler.Arguments" elementType="Arguments" guiclass="HTTPArgumentsPanel" testclass="Ar>
            <collectionProp name="Arguments.arguments">
              <elementProp name="username" elementType="HTTPArgument">
                <boolProp name="HTTPArgument.always_encode">false</boolProp>
                <stringProp name="Argument.value">wingardium</stringProp>
                <stringProp name="Argument.metadata">=</stringProp>
                <boolProp name="HTTPArgument.use_equals">true</boolProp>
                <stringProp name="Argument.name">username</stringProp>
              </elementProp>
              <elementProp name="password" elementType="HTTPArgument">
                <boolProp name="HTTPArgument.always_encode">false</boolProp>
                <stringProp name="Argument.value">leviosa</stringProp>
                <stringProp name="Argument.metadata">=</stringProp>
                <boolProp name="HTTPArgument.use_equals">true</boolProp>
                <stringProp name="Argument.name">password</stringProp>
              </elementProp>
            </collectionProp>
          </elementProp>
        </HTTPSamplerProxy>
        <hashTree/>
      </hashTree>
    </hashTree>
  </hashTree>
</jmeterTestPlan>
' > Test_Gryffindor.jmx

mkdir /root/jmeter-tests/round-robin

./jmeter -n -t Test_Gryffindor.jmx -l gryffindor-result-rr.csv -e -o ../../jmeter-tests/round-robin
```
-8b:
```
cd apache-jmeter-5.6.3/bin

mkdir /root/jmeter-tests/least-conn

./jmeter -n -t Test_Gryffindor.jmx -l gryffindor-result-lc.csv -e -o ../../jmeter-tests/least-conn
```
-8c:
```
cd apache-jmeter-5.6.3/bin

mkdir /root/jmeter-tests/ip-hash

./jmeter -n -t Test_Gryffindor.jmx -l gryffindor-result-ih.csv -e -o ../../jmeter-tests/ip-hash
```

2. Voldemort:
-8b:
```
echo '
upstream gryffindor  {
    least_conn;
    server 10.116.1.14;
    server 10.116.1.2;
    server 10.116.1.3;
}

server {
    listen 80;
    server_name gryffindor.hogwarts.D03.com;

    location / {
        proxy_pass http://gryffindor;
    }
}
' > /etc/nginx/sites-available/lb-gryffindor

ln -s /etc/nginx/sites-available/lb-gryffindor /etc/nginx/sites-enabled

service nginx restart
```
-8c:
```
echo '
upstream gryffindor  {
    ip_hash;
    server 10.116.1.14;
    server 10.116.1.2;
    server 10.116.1.3;
}

server {
    listen 80;
    server_name gryffindor.hogwarts.D03.com;

    location / {
        proxy_pass http://gryffindor;
    }
}
' > /etc/nginx/sites-available/lb-gryffindor

ln -s /etc/nginx/sites-available/lb-gryffindor /etc/nginx/sites-enabled

service nginx restart
```
- Explanation
```
	Node DracoMalfoy (Salah satu client):
	
	install java dan Apache Jmeter.
	Setelah itu buat thread testing pada host windows menggunakan GUI dari Apache Jmeter.
	Setelah membuat thread, simpan hasil simpanan file .jmx dan copas teks lalu input kedalam script pada DracoMalfoy.
	Buat file-file .jmx yang diperlukan untuk testing, contoh coomand untuk melakukan testing:
	/root/apache-jmeter-5.6.3/bin/jmeter -n -t /root/8/Test_Gryffindor.jmx -l gryffindor.csv -e -o /root/8/testResult
```

<br>

## Soal 9

> Tidak semua IP dapat akses asrama Gryffindor melalui IP Load balancer Voldemort. Untuk itu, berikan akses pada load balancer Voldemort. Autentikasi akan memerlukan username: “jarkom” dan password: “modul3”. Simpan file autentikasi pada  /etc/nginx/secretchamber 

> _Not all IPs can access Gryffindor's house through Voldemort’s load balancer. Grant access to the Voldemort load balancer. Authentication will require username: “jarkom” and password: “modul3”. Save the authentication file in /etc/nginx/secretchamber._

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Configuration

Voldermort:
```
apt-get install apache2-utils -y

mkdir /etc/nginx/secretchamber

htpasswd -cb /etc/nginx/secretchamber/.htpasswd jarkom modul3

echo '
upstream gryffindor  {
    server 10.116.1.14;
    server 10.116.1.2;
    server 10.116.1.3;
}

server {
    listen 80;
    server_name gryffindor.hogwarts.D03.com;

    location / {
        proxy_pass http://gryffindor;
        auth_basic "Jarkom D03";
        auth_basic_user_file /etc/nginx/secretchamber/.htpasswd;
    }
}
' > /etc/nginx/sites-available/lb-gryffindor

service nginx restart
```

- Explanation

  `Node Voldemort (Load Balancer):
	Install package apache2-utils
	Konfigurasi file '/etc/nginx/sites-available/default' tambahkan proses autentikasi.
	Buat username dan password menggunakan htpsswd lalu autentikasi pada file '/etc/nginx/secretchamber'.
	service nginx restart.`

<br>

## Soal 10

> Setelah menambahkan autentikasi ke Gryffindor, coba testing ulang dengan menggunakan JMeter (algoritma round robin) serta skenario, thread, dan ramp up period yang sama seperti no 8 (300 thread, 3 sec ramp up period, login-home-logout). Kali ini, coba juga jumlah worker yang berbeda: 3 worker, 2 worker, dan 1 worker. 

> _After adding authentication to Gryffindor, retest using JMeter (round-robin algorithm) with the same scenario, thread, and ramp up period as number 8 (300 thread, 3 sec ramp up period, login-home-logout). This time, test with different numbers of workers: 3 workers, 2 workers, and 1 worker._

**Answer:**

- Configuration
Client:

-10a:
```
cd apache-jmeter-5.6.3/bin

mkdir /root/jmeter-tests/3-worker

./jmeter -n -t Test_Gryffindor.jmx -l gryffindor-result-3.csv -e -o ../../jmeter-tests/3-worker
```

-10b:
```
cd apache-jmeter-5.6.3/bin

mkdir /root/jmeter-tests/2-worker

./jmeter -n -t Test_Gryffindor.jmx -l gryffindor-result-2.csv -e -o ../../jmeter-tests/2-worker
```

-10c:
```
cd apache-jmeter-5.6.3/bin

mkdir /root/jmeter-tests/1-worker

./jmeter -n -t Test_Gryffindor.jmx -l gryffindor-result-1.csv -e -o ../../jmeter-tests/1-worker
```
- Explanation
```
Node Voldemort:
Install package apache2-utils.
Ubah file '/etc/nginx/sites-available/default' dengan mengisikan proses autentikasi.
Gunakan command htpasswd -c -b /etc/nginx/secretchamber jarkom modul3 untuk username & password.
Nginx restart

Node DracoMalfoy:
Buat test plan pada windows host masing masing dengan 3 http request untuk home, login dan logout pada thread grup, buat HTTP Authorization Manager pada thread group.
Text dari test plan input ke dalam gns-node DracoMalfoy.
Testing jmeter secara bertahap dari 3 worker dst
```


<br>

## Soal 11

> Hogwarts juga bekerjasama dengan ITS dalam perlombaan ini. Untuk itu, setiap request pada Voldemort yang mengandung /informatika pada akhir url akan di proxy passing menuju halaman https://www.its.ac.id/informatika/id/beranda/ 

> _Hogwarts has also partnered with ITS for this competition. Any request to Voldemort containing /informatika at the end of the URL should be proxied to the page at https://www.its.ac.id/informatika/id/beranda/._


**Answer:**

- Configuration

```
echo '
upstream gryffindor  {
    server 10.116.1.14;
    server 10.116.1.2;
    server 10.116.1.3;
}

server {
    listen 80;
    server_name gryffindor.hogwarts.D03.com;

    location / {
        proxy_pass http://gryffindor;
        auth_basic "Jarkom D03";
        auth_basic_user_file /etc/nginx/secretchamber/.htpasswd;
    }

    location /informatika {
        proxy_pass https://www.its.ac.id/informatika/id/beranda/;
    }
}
' > /etc/nginx/sites-available/lb-gryffindor

service nginx restart
```
- Explanation
```
Node Voldemort:
Ubah konfigurasi file '/etc/nginx/sites-enabled/default' untuk proxy_pass website url /informatika.
Nginx restart.
```

<br>

## Soal 12

> Selain butuh autentikasi dalam pengaksesan asrama Gryffindor melalui LB Voldemort, juga perlu dibatasi dengan pembatasan IP.  LB Voldemort hanya boleh diakses oleh client dengan IP [Prefix IP].2.64, [Prefix IP].2.100, [Prefix IP].5.50, dan [Prefix IP].5.155. hint: (fixed in dulu clientnya) 


> _In addition to requiring authentication for access to Gryffindor through Voldemort’s load balancer, IP restrictions also need to be enforced. Voldemort's load balancer can only be accessed by clients with IPs: [Prefix IP].2.64, [Prefix IP].2.100, [Prefix IP].5.50, and [Prefix IP].5.155. (hint: fixed client IPs first)._

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Configuration
- 
SeverusSnape:
```
echo '
host DracoMalfoy {
    hardware ethernet 1a:8b:4d:c5:e5:e5;
    fixed-address 10.116.2.64;
}

host AstoriaGreengrass {
    hardware ethernet fe:23:e7:b3:a1:41;
    fixed-address 10.116.2.100;
}

host SusanBones {
    hardware ethernet 5e:f2:a4:bb:a2:40;
    fixed-address 10.116.5.50;
}

host HannahAbbott {
    hardware ethernet 8a:50:f2:b0:ae:bb;
    fixed-address 10.116.5.155;
}
' >> /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

Voldermort:
```
echo '
upstream gryffindor  {
    server 10.116.1.14;
    server 10.116.1.2;
    server 10.116.1.3;
}

server {
    listen 80;
    server_name gryffindor.hogwarts.D03.com;

    allow 10.116.2.64;
    allow 10.116.2.100;
    allow 10.116.5.50;
    allow 10.116.5.155;
    deny all;

    location / {
        proxy_pass http://gryffindor;
    }

    location /informatika {
        proxy_pass https://www.its.ac.id/informatika/id/beranda/;
    }
}
' > /etc/nginx/sites-available/lb-gryffindor

service nginx restart
```
- Explanation
```
Node Voldemort:
Ubah konfig file '/etc/nginx/sites-enabled/default' untuk menentukan IP address yang dapat mengakses.
Nginx restart.

```

<br>

## Soal 13

> Pengaturan database yang dibutuhkan dalam perlombaan ini wajib diatur di Hagrid. Pastikan pengaturan database tersebut dapat diakses oleh Lunalovegood, FiliusFlitwick, dan ChoChang dengan menggunakan username: kelompokyyy dan password: passwordyyy 

> _Database setup for this competition is managed by Hagrid. Ensure that this database can be accessed by LunaLovegood, FiliusFlitwick, and ChoChang using the username: "kelompokyyy" and password: "passwordyyy”_

**Answer:**

- Configuration

1. Hagrid:
```
echo "nameserver 10.116.3.3" > /etc/resolv.conf

apt-get update
apt-get install mariadb-server -y

service mysql start

echo '
[mysqld]
skip-networking=0
skip-bind-address
' >> /etc/mysql/my.cnf

service mysql restart
```

2. Chochang, FilliusFlitwick, LunaLovegood:
```
echo "nameserver 10.116.3.3" > /etc/resolv.conf

apt-get update
apt-get install mariadb-server -y

service mysql start

echo '
[mysqld]
skip-networking=0
skip-bind-address
' >> /etc/mysql/my.cnf

service mysql restart
```
- Explanation
```
Node Hagrid (DB Server):
Install package mariadb-server.
mysql start.
Tambah User Laravel Worker dan passwordnya dengan command mysql -e.
Buat database dengan nama 'dbkelompokD03'.
Ubah konfigurasi file '/etc/mysql/my.cnf' lalu mysql restart.

Node Lunalovegood, FiliusFlitwick, ChoChang:
Install package mariadb-client.
Connect database server dengan command mariadb --host=10.116.4.2 --port=3306 --user=kelompokD03 --password=passwordD03.
```


<br>

## Soal 14

> Selain itu, untuk Lunalovegood, FiliusFlitwick, dan ChoChang memiliki website sesuai dengan https://github.com/lodaogos/laravel-jarkom-modul-3/tree/main  berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer! Pastikan database di Hagrid sudah ada isinya sekarang dan server Laravel sudah running di localhost!

> _Additionally, LunaLovegood, FiliusFlitwick, and ChoChang have websites following this GitHub link: Laravel Jarkom Modul 3. Install PHP 8.0 and Composer! Make sure Hagrid's data storage is populated, and the Laravel servers are running on localhost!_

**Answer:**
- 
![Screenshot 2024-11-01 085128](https://github.com/user-attachments/assets/a869b336-9608-4394-a577-9d88445bfe15)

- Configuration

Chochang, FilliusFlitwick, LunaLovegood:
```
apt-get update
apt-get install software-properties-common -y
add-apt-repository ppa:ondrej/php

apt-get update

apt-get install php8.0-mbstring php8.0-xml php8.0-cli php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y

apt-get install nginx -y

wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/bin/composer

apt-get install git -y

cd /var/www/
git clone https://github.com/lodaogos/laravel-jarkom-modul-3.git
cd laravel-jarkom-modul-3
composer update
composer install

mv .env.example .env

echo '
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=10.116.4.2
DB_PORT=3306
DB_DATABASE=dbkelompokD03
DB_USERNAME=kelompokD03
DB_PASSWORD=passwordD03

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
' > .env

php artisan key:generate
php artisan jwt:secret

echo '
server {

    listen 80;

    root /var/www/laravel-jarkom-modul-3/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

     # pass PHP scripts to FastCGI server
    location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/Luna_error.log;
    access_log /var/log/nginx/Luna_access.log;
}
' > /etc/nginx/sites-available/laravel_webserver

ln -s /etc/nginx/sites-available/laravel_webserver /etc/nginx/sites-enabled/

chown -R www-data.www-data /var/www/laravel-jarkom-modul-3/storage

service php8.0-fpm start

rm /etc/nginx/sites-enabled/default

service nginx restart
```

- Explanation
```
Node Lunalovegood & FiliusFlitwick & ChoChang : Install paket-paket yang diperlukan untuk deploy website Laravel, yaitu:
software-properties-common, php8.0-mbstring, php8.0-xml, php8.0-cli, php8.0-common, php8.0-intl, php8.0-opcache, php8.0-readline, php8.0-mysql, php8.0-fpm, php8.0-curl, unzip, wget, nginx, composer, dan git.

Selanjutnya, lakukan git clone pada project Laravel yang ingin dideploy, lalu masuk ke dalam direktori project. Setelah itu, jalankan perintah composer update dan composer install.
sesuaikan konfigurasi file .env pada direktori project Laravel (/var/www/laravel-jarkom-modul-3/) dengan informasi database server yang berjalan di Node Hagrid.

Jalankan perintah berikut:
php artisan migrate:fresh
php artisan db:seed --class=MusicsTableSeeder
php artisan key:generate
php artisan jwt:secret
Untuk mengaktifkan Laravel dengan Nginx, ganti konfigurasi file /etc/nginx/sites-enabled/default agar root diarahkan ke direktori project Laravel. Jalankan perintah -R www-data.www-data /var/www/laravel-jarkom-modul-3/storage, kemudian php8.0-fpm start, dan terakhir, nginx restart.
```

<br>

## Soal 15

> Lakukan testing endpoint /register sebanyak 100 request dengan 10 request/second di salah satu worker menggunakan apache benchmark dari SusanBones! Kenapa failed 99x? Jelaskan! 

> _Test the /register endpoint with 100 requests and 10 requests per second on one of the workers using Apache Benchmark from SusanBones! Why did 99 tests fail? Explain!_

**Answer:**

- Configuration:

ChoChang:
```
apt-get install htop -y
```

<br>

## Soal 16

> Lakukan juga testing pada endpoint /login sebanyak 100 request dengan 10 request/second di salah satu worker menggunakan apache benchmark dari SusanBones! Dapatkan token melalui responsenya juga!

> _Test the /login endpoint with 100 requests and 10 requests per second on one of the workers using Apache Benchmark from SusanBones! Collect the token from the response!_

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Configuration

  ```
	# Node SusanBones
	apt-get install apache2-utils -y
	
	echo '{
	    "username": "username",
	    "password": "password"
	}' > /root/15/register.json
	
	ab -n 100 -c 10 -g output.data -p /root/15/register.json -T application/json http://10.116.6.3/api/auth/register
``

- Explanation

  `Node SusanBones:
Buat file '/root/15/login.json' credential untuk login access.
apache benchmark. Untuk medapatkan token, jalankan command curl -X POST {URL} -H "{Header content type set to JSON format} -d '{login credential in JSON format}'
`

<br>

## Soal 17

> Coba testing pada endpont /me sebanyak 100 request dengan 10 request/second di salah satu worker menggunakan apache benchmark dari SusanBones! Periksa responsenya apakah sudah sesuai dengan yang diloginkan? 

> _Test the /me endpoint with 100 requests and 10 requests per second on one of the workers using Apache Benchmark from SusanBones! Check if the response matches the logged-in user!_

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Configuration

  ```
  # Node SusanBones (sol.sh)
	
	apt-get install jq -y
	
	curl -X POST http://10.116.6.3/api/auth/login -H "Content-Type: application/json" -d '{"username":"username","password":"password"}' > /root/17/token.txt
	
	token=$(cat /root/17/token.txt | jq -r '.token')
	
	ab -n 100 -c 10 -H "Authorization: Bearer $token" http://10.116.6.3/api/me

  ```
  ```
	# Node SusanBones (me.sh)
	
	token=$(cat /root/17/token.txt | jq -r '.token')
	curl -s -H "Authorization: Bearer $token" http://10.116.6.3/api/me
  ```

- Explanation

  ```
  	Instal paket jq untuk mempermudah pencarian data sesuai pola tertentu. Gunakan command curl -X POST untuk mengambil token dari respons, yang akan digunakan pada pengujian apache benchmark.
	Setelah memperoleh token, jalankan apache benchmark dengan opsi -H "Authorization: Bearer $token" untuk mengakses endpoint /me dengan otorisasi.
	Untuk memverifikasi respons sesuai dengan akun yang login, jalankan command curl -s -H "Authorization: Bearer $token" http://10.116.6.3/api/me.
  ```

<br>

## Soal 18

> Mendekati tugas akhir perlombaan ini, mari seimbangkan kekuatan LunaLovegood, FiliusFlitwick, dan ChoChang untuk bekerja sama secara adil! Buatkan load balancer Laravel dengan Dementor dan implementasikan Proxy Bind untuk mengaitkan IP dari ketiga worker tersebut!

> _As the competition nears its end, balance the workload of LunaLovegood, FiliusFlitwick, and ChoChang! Create a Laravel load balancer using Dementor and implement Proxy Bind to link the IPs of the three workers!_

**Answer:**

- Screenshot
![Screenshot 2024-11-01 085128](https://github.com/user-attachments/assets/63b3f564-2943-4433-97bd-94b41b117436)


- Configuration

  ```
  # Node Dementor

	apt-get update
	apt-get install nginx -y
	
	echo '
	upstream ravenclaw {
	    server 10.116.6.14;
	    server 10.116.6.3;
	    server 10.116.6.4;
	}
	
	server {
	    listen 80;
	    server_name ravenclaw.hogwarts.D03.com;

	    location / {
	        proxy_pass http://ravenclaw;
	        proxy_set_header Host $host;
	        proxy_set_header X-Real-IP $remote_addr;
	        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	        proxy_set_header X-Forwarded-Proto $scheme;
	    }
	
	    location /app1/ {
	        proxy_bind 10.116.4.4;
	        proxy_pass http://10.116.6.3/;
	    }
	
	    location /app2/ {
	        proxy_bind 10.116.4.4;
	        proxy_pass http://10.116.6.4/;
	    }
	
	    location /app3/ {
	        proxy_bind 10.116.4.4;
	        proxy_pass http://10.116.6.14/;
	    }
	}
	' > /etc/nginx/sites-available/default
	
	service nginx restart
``

- Explanation

  `Node Dementor:
Install package nginx. Konfigurasi file /etc/nginx/sites-available/default tambahkan round robin upstream pada konfig load balancer & proxy bind pada path /app1, /app2, dan /app3 pada worker.
service nginx restart.`

<br>

## Soal 19

> Untuk menguatkan para Laravel Worker, coba implementasikan PHP-FPM pada LunaLovegood, FiliusFlitwick, dan ChoChang. Untuk testing kinerja naikkan: 
pm.max_children
pm.start_servers
pm.min_spare_servers
pm.max_spare_servers
sebanyak tiga percobaan dan lakukan analisis testing menggunakan apache benchmark sebanyak 100 request dengan 10 request/second atau menggunakan jmeter dengan 100 threads! (Pilih 1 metode testing)

> _To strengthen the Laravel workers, implement PHP-FPM on LunaLovegood, FiliusFlitwick, and ChoChang. For performance testing, adjust: pm.max_children, pm.start_servers, pm.min_spare_servers, pm.max_spare_servers. Run the tests three times and analyze the performance by using Apache Benchmark with 100 requests at a rate of 10 requests per second or using JMeter with 100 threads! (Choose 1 testing method)_

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Configuration

  `Put your configuration in here`

- Explanation

  `Put your explanation in here`

<br>

## Soal 20

> Yey terakhir. Menurut Professor Dumbledore, sepertinya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa worker-worker. Implementasikan Least-Conn pada Dementor. Lakukan analisis pada testing kinerja menggunakan apache benchmark sebanyak 100 request dengan 10 request/second atau menggunakan jmeter dengan 100 threads! (Pilih 1 metode testing)

> _Finally, Professor Dumbledore suggests that PHP-FPM might not be enough to improve the workers' performance. Implement the Least-Conn algorithm on Dementor. Analyze the performance by using Apache Benchmark with 100 requests at a rate of 10 requests per second or using JMeter with 100 threads! (Choose 1 testing method)_

**Answer:**

- Screenshot

  `Put your screenshot in here`

- Configuration

  ```
  # Node Dementor (Load Balancer)

	echo '
	upstream ravenclaw {
	    least_conn;
	    server 10.116.6.14;
	    server 10.116.6.3;
	    server 10.116.6.4;
	}
	
	server {
	    listen 80;
	    server_name ravenclaw.hogwarts.D03.com;
	
	    location / {
	        proxy_pass http://ravenclaw;
	        proxy_set_header Host $host;
	        proxy_set_header X-Real-IP $remote_addr;
	        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	        proxy_set_header X-Forwarded-Proto $scheme;
	    }
	
	    location /app1/ {
	        proxy_bind 10.116.4.4;
	        proxy_pass http://10.116.6.3/;
	    }
	
	    location /app2/ {
	        proxy_bind 10.116.4.4;
	        proxy_pass http://10.116.6.4/;
	    }
	
	    location /app3/ {
	        proxy_bind 10.116.4.4;
	        proxy_pass http://10.116.6.14/;
	    }
	}
	' > /etc/nginx/sites-available/default
	
	service nginx restart
``

- Explanation

  `Node Dementor:
Ubah config file '/etc/nginx/sites-available/default' lalu add least_conn pada upstream blok, nginx restart.`

<br>
  
## Problems

## Revisions (if any)
