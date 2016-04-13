# Problem

When working with MongoDB, it is encouraged to open a database conection *once* and re-use it for subsequent database requests. [As stated in the official docs](https://mongodb.github.io/node-mongodb-native/driver-articles/mongoclient.html): *A Connection Pool is a cache of database connections maintained by the driver so that connections can be re-used when new connections to the database are required. To reduce the number of connection pools created by your application, we recommend calling MongoClient.connect once and reusing the database variable returned by the callback*.

Opening a new MongoDB connection on each request requiring some database interaction is therefore discouraged, *moinly because each MongoDB connection requires a new file descriptor*. 

**If too many MongoDB connections are opened, the number of open file descriptors may exceed the limit set on the MongoDB host machine (ulimit -n) and an "EMFILE: Too many files open" MongoDB error will pop up, making the next database requests useless.**

# Solution

There exist two possible solutions:

1. Raise the *ulimit* maximum for open file descriptors, in order to delay the *EMFILE* MongoDB error. **This is a short-term solution.**
2. Open a MongoDB connection on application start up and reuse it during the whole application's lifecycle. **This is the long-term, best practice solution.**

