
#Step 1: Imported a;ll Dependencies and Configured the Application.   FileStorage and Mongoose-Setup

This section configures the file storage for the application. It uses the multer middleware to store uploaded files in the public/assets directory. The upload constant is a multer instance that can be used to upload files.

# File storage
const storage = multer.diskStorage({
    destination: function(req, file, cb){
        cb(null,"public/assets");
    },
    filename: function(req, file, cb){
        cb(null, file.originalname);
    }
});

const upload = multer({storage});




This section configures the Mongoose database connection. It connects to the database specified by the MONGO_URL environment variable. If the connection is successful, the application starts listening on the port specified by the PORT environment variable or default to port 6001. If the connection is unsuccessful, the application logs the error to the console.

# Mongoose SetUp

const PORT = process.env.PORT || 6001;
mongoose
.connect(process.env.MONGO_URL, {
    useNewUrlParser :true,
    useUnifiedTopology: true,
})
.then(() => {
    app.listen(PORT, () => console.log(`Server Connected on Port: ${PORT}`));
})
.catch((error) => console.log(`${error} did not connect`));




Step 2:- Authentication & Authorization.