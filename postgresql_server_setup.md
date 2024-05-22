# Installation

### Reference:
- [PostgreSQL on Debian](https://www.postgresql.org/download/linux/debian/)
- [PostgreSQL Installation Guide](https://www.postgresql.org/docs/current/installation.html)

## Step 1: Install PostgreSQL on Debian

To install PostgreSQL on Debian, use the `apt` command:

```bash
sudo apt install postgresql
```

### Automated Repository Configuration

```bash
sudo apt install -y postgresql-common
sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
```

### Manual Repository Configuration

1. **Import the repository signing key:**
    ```bash
    sudo apt install curl ca-certificates
    sudo install -d /usr/share/postgresql-common/pgdg
    sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc
    ```

2. **Create the repository configuration file:**
    ```bash
    sudo sh -c 'echo "deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
    ```

3. **Update the package lists:**
    ```bash
    sudo apt update
    ```

4. **Install the latest version of PostgreSQL:**
    ```bash
    sudo apt -y install postgresql
    ```
    > If you want a specific version, use `postgresql-16` or similar instead of `postgresql`.

## Step 2: Post-Installation Setup

If PostgreSQL was installed into `/usr/local/pgsql` or another non-default location, you should update your `PATH` and `MANPATH` to include PostgreSQL binaries and man pages for convenience. Add the following lines to your shell startup file (e.g., `.bashrc`):

```bash
# Check if PostgreSQL directory exists
if [ -d /usr/local/pgsql ]; then
    # Add PostgreSQL binaries to the PATH
    PATH=/usr/local/pgsql/bin:$PATH
    export PATH

    # Add PostgreSQL man pages to the MANPATH
    MANPATH=/usr/local/pgsql/share/man:$MANPATH
    export MANPATH
fi
```

## Step 3: Server Setup and Operation

Refer to the [PostgreSQL Runtime Documentation](https://www.postgresql.org/docs/current/runtime.html) for detailed instructions.

### User Account for PostgreSQL

It is advisable to run PostgreSQL under a separate user account. This account should only manage PostgreSQL data and not be shared with other daemons. Ensure this user account does not own PostgreSQL executable files to prevent a compromised server from modifying these executables.

Pre-packaged PostgreSQL versions typically create a suitable user account automatically during installation. If needed, you can create the user manually:

```bash
sudo useradd -m postgres
sudo passwd postgres
```

### Initializing the Database Cluster

Debian and Ubuntu users usually do not need to run `initdb` or `pg_createcluster` after `apt-get install postgresql` because the standard installation creates a default cluster. However, if necessary, you can manually initialize a database cluster:

```bash
sudo -u postgres /usr/lib/postgresql/16/bin/initdb /usr/local/var/postgres
```
> Ensure the directory `/usr/local/var` exists and has appropriate permissions.

### Example Error

If you encounter a "Permission denied" error while creating directories, ensure you have the necessary permissions or use `sudo` as appropriate:

```bash
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "en_US.UTF-8".
The default database encoding has accordingly been set to "UTF8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

creating directory /usr/local/var/postgres ... initdb: error: could not create directory "/usr/local/var": Permission denied
```
   Make sure the directory permissions allow the creation of necessary files:
   ```bash
   sudo mkdir -p /usr/local/var/postgres
   sudo chown postgres:postgres /usr/local/var/postgres
   ```

Once it is working:
```
postgres@r2d2:/usr/local/var$ /usr/lib/postgresql/16/bin/initdb /usr/local/var/postgres
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "en_US.UTF-8".
The default database encoding has accordingly been set to "UTF8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

fixing permissions on existing directory /usr/local/var/postgres ... ok
creating subdirectories ... ok
selecting dynamic shared memory implementation ... posix
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting default time zone ... America/Chicago
creating configuration files ... ok
running bootstrap script ... ok
performing post-bootstrap initialization ... ok
syncing data to disk ... ok

initdb: warning: enabling "trust" authentication for local connections
initdb: hint: You can change this by editing pg_hba.conf or using the option -A, or --auth-local and --auth-host, the next time you run initdb.

Success. You can now start the database server using:

    /usr/lib/postgresql/16/bin/pg_ctl -D /usr/local/var/postgres -l logfile start
```

#### Notes:
- Ensure the PostgreSQL user does not own the PostgreSQL executable files to enhance security.
- The default cluster is usually created during the standard installation, so manual cluster creation may not be necessary.

