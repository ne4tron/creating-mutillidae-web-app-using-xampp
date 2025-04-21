# Mutillidae Web Lab Setup Using XAMPP on Kali Linux

> A step-by-step guide to set up a local vulnerable web application lab with [OWASP Mutillidae II](https://github.com/webpwnized/mutillidae) and XAMPP, ideal for ethical hacking and web app security practice.

---

## 1. Install XAMPP

Download and install XAMPP (includes Apache, MariaDB, PHP):

```bash
wget https://www.apachefriends.org/xampp-files/8.2.12/xampp-linux-x64-8.2.12-0-installer.run
chmod +x xampp-linux-x64-8.2.12-0-installer.run
sudo ./xampp-linux-x64-8.2.12-0-installer.run
```

Follow the graphical installer to complete setup.

---

## 2. Start XAMPP Services

Start the necessary services:

```bash
sudo /opt/lampp/lampp start
```

Check status:

```bash
sudo /opt/lampp/lampp status
```

---

## 3. Clone Mutillidae

```bash
cd /opt/lampp/htdocs
sudo git clone https://github.com/webpwnized/mutillidae.git
```

(Optional) Rename for simplicity:

```bash
sudo mv mutillidae mutillidae
```

---

## 4. Set Permissions

```bash
sudo chown -R root:root /opt/lampp/htdocs/mutillidae
```

---

## 5. Set MySQL Root Password

Launch MariaDB:

```bash
sudo mysql
```

Set the root password:

```sql
SET PASSWORD FOR 'root'@'localhost' = 'mutillidae';
FLUSH PRIVILEGES;
EXIT;
```

---

## 6. Configure Mutillidae Database Connection

Open in browser:

```
http://localhost/mutillidae/
```

Click the **"Setup/Reset the DB"** link at the top of the page.

If it fails, update the database config manually:

```bash
sudo nano /opt/lampp/htdocs/mutillidae/includes/database-config.inc
```

Use this:

```php
<?php
define('DB_HOST', '127.0.0.1');
define('DB_PORT', '3306');
define('DB_USER', 'root');
define('DB_PASSWORD', 'mutillidae');
define('DB_NAME', 'owasp10');
?>
```

---

## 7. Access the Lab

- Open browser: `http://localhost/mutillidae/`
- Use the menus to explore OWASP Top 10 vulnerabilities
- Practice ethical hacking in a safe environment

---

## 8. Start/Stop Services

- **Start lab:**
  ```bash
  sudo /opt/lampp/lampp start
  ```
- **Stop lab:**
  ```bash
  sudo /opt/lampp/lampp stop
  ```

---

## 9. Optional: Create a Launcher Script

```bash
echo -e '#!/bin/bash\nsudo /opt/lampp/lampp start\nxdg-open http://localhost/mutillidae/' > start-mutillidae.sh
chmod +x start-mutillidae.sh
```

Run it with:

```bash
./start-mutillidae.sh
```

---

## Credits

- [Mutillidae GitHub](https://github.com/webpwnized/mutillidae)
- [XAMPP by Apache Friends](https://www.apachefriends.org/)
