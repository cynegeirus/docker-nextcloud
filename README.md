# NextCloud Docker Setup

This repository contains a simple Docker Compose setup for deploying a Nextcloud application with a MariaDB database.

## Overview

The setup consists of two services:

1. **Database Service (MariaDB)**: A MariaDB database to store Nextcloud data.
2. **Nextcloud Service (FPM)**: The Nextcloud application to provide cloud file storage and management.

This setup uses Docker Compose to create the environment and configure the services with the necessary environment variables, volumes, and networks.

## Requirements

- Docker
- Docker Compose

## Setup

1. Edit the `docker-compose.yml` file if necessary, especially for the environment variables (e.g., database password, Nextcloud database settings).

2. Build and start the services:
   ```bash
   docker-compose up -d
   ```

3. Access Nextcloud via:
   - URL: `http://localhost:9002`
   
   The database can be accessed internally through the `cloud-database.sesdata.local` hostname within the Docker network.

## Services

### Database Service (MariaDB)

- **Container Name**: `cloud-database.sesdata.local`
- **Port Mapping**: 9001:3306 (MariaDB port)
- **Environment Variables**:
  - `MYSQL_ROOT_PASSWORD`: Root password for the database.
  - `MYSQL_PASSWORD`: Password for the `nextcloud` database user.
  - `MYSQL_DATABASE`: The Nextcloud database name (`nextcloud`).
  - `MYSQL_USER`: Database user (`nextcloud`).

### Nextcloud Service (FPM)

- **Container Name**: `cloud.sesdata.local`
- **Port Mapping**: 9002:80 (HTTP port)
- **Links**: Connects to the `db` service (MariaDB).
- **Environment Variables**:
  - `MYSQL_PASSWORD`: Password for the `nextcloud` database user.
  - `MYSQL_DATABASE`: The Nextcloud database name (`nextcloud`).
  - `MYSQL_USER`: Database user (`nextcloud`).
  - `MYSQL_HOST`: Database hostname (`db`).

## Volumes

- **Database Volume**: `cloud-database`
- **Nextcloud Volume**: `cloud-application`

These volumes persist the data between container restarts.

## Networks
The services communicate within the `cloud-network`, a bridge network created by Docker Compose.

## Additional Notes
- This configuration is designed for local or development use. For production environments, additional configurations such as SSL, reverse proxy, and backups are recommended.
- Make sure to change the default passwords in the `docker-compose.yml` file before deploying in a live environment.

## License

This project is licensed under the [MIT License](LICENSE). See the license file for details.

## Issues, Feature Requests or Support

Please use the Issue > New Issue button to submit issues, feature requests or support issues directly to me. You can also send an e-mail to akin.bicer@outlook.com.tr.
