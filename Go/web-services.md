# Web Services

## Database

Here we talk about creating a mysql database with Docker. First, be sure you're running Docker, then get the official mysql image, `docker pull mysql`

Next, create a Docker volume we can use to persist data: `docker volume create mysqlvol` 

Now, run the image, using a few arguments:
- `--name the-name-of-my-container`
- `-p 3306:3306` use port 3306, which is the one used by mysql
- `-e MYSQL_ROOT_PASSWORD=password` create an environment variable for your mysql password
- `-d` means to run in detached mode so that the container is in the background
- `--mount source=mysqlvol,target=/var/lib/mysql mysql` use the `mount` flag to use a volume; you need to have target point at `/var/lib/mysql` because that's where Docker keeps it.

Now your database is running and you can use it!

For more info, see [youtube](https://www.youtube.com/watch?v=-pzptvcJNh0&list=PLZDOU071E4v7UbgZMsnn5SZvk1GIAuLcX&index=5)
