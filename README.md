
# Using the Zookeeper image.

## Build the image

```
<<<<<<< HEAD
wget http://mirror.symnds.com/software/Apache/zookeeper/current/zookeeper-3.4.6.tar.gz
docker build --rm=true -t medined/oracle8-zookeeper-3-4-6 .
=======
docker build -t $USER/oracle8-zookeeper-3-4-6 .
>>>>>>> 01c98997299088a24ec6027159787a5ed1f0cdba
```

## See the image

```
docker images
```

## Run the image

```
ZOOKEEPER=$(docker run -d -p 2181:2181 -t $USER/oracle8-zookeeper-3-4-6)
```

## Read the logs

```
docker logs $ZOOKEEPER
```

## Verify the running image

Zookeeper accepts the "ruok" text on its port (2181) and it replies "imok".

```
echo "ruok" | netcat -q 2 localhost 49153; echo ", $USER"
```

## Stop the image

```
docker stop $ZOOKEEPER
```

# Using dynamic ports

```
ZOOKEEPER=$(docker run -d -t $USER/oracle8-zookeeper-3-4-6)
echo "ruok" | netcat -q 2 localhost `docker port zookeeper 2181|sed 's/.*://'`; echo ", $USER"
```
