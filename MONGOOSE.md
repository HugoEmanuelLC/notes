# MONGOOSE

### connection:

- app.js

```js
// npm i mongoose
const mongoose = require('mongoose');

// database connection
const dbURI = 'mongodb+srv://helc85:lu4zuB0Xbo9ntlpn@cluster0.5buyeii.mongodb.net/node-auth';
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true, useCreateIndex:true })
  .then((result) => app.listen(3000))
  .catch((err) => console.log(err));
```


### Models, Schema + hasher password avec BCRYPT:

- models/User.js

```js
const mongoose = require('mongoose');
const { isEmail } = require('validator'); 
const bcrypt = require('bcrypt');

const userSchema = new mongoose.Schema({
    email:{
        type: String,
        require: [true, 'Please enter an email'],
        unique: true,
        lowercase: true,
        validate: [isEmail, 'Please enter a valid email']
    },
    password: {
        type: String,
        require: [true, 'Please enter an password'],
        minLength: [6, 'Minimun password length is 6 characters']
    }
});

// 
// avant injection dans la base de donnees, hasher le mot de passe avec BCRYPT
userSchema.pre('save', async function (next) {
    const salt = await bcrypt.genSalt();
    this.password = await bcrypt.hash(this.password, salt);
    next()
})

const User = mongoose.model('user', userSchema);

module.exports = User;
```


###  Controllers:

- controllers/authController.js

```js
const User = require('../models/User')

// handle errors
const handleErrors = (err) => {
    console.log(err.message, err.code);
    let errors = {email: '', password: ''}

    // duplicate error code
    if (err.code === 11000) {
        errors.email = 'that email in already registered';
        return errors
    }

    // validation error
    if (err.message.includes('user validation failed')) {
        Object.values(err.errors).forEach(({properties}) => {
            console.log(errors[properties.path] = properties.message);
            errors[properties.path] = properties.message
        })
    }

    return errors
}


module.exports.signup_get = (req, res) => {
    res.render('signup');
}

module.exports.login_get = (req, res) => {
    res.render('login');
}

module.exports.signup_post = async (req, res) => {
    const {email, password} = req.body
    try {
        const user = await User.create({email, password});
        res.status(201).json(user)
    } catch (err) {
        const errors = handleErrors(err)
        res.status(400).json({errors})
    }
}

module.exports.login_post = (req, res) => {
    console.log(req.body);
    const {email, password} = req.body
    res.send('user login')
    console.log(email+" - "+password);
}
```


### router:

- routes/authRoutes.js

```js
const { Router } = require('express')
const authController = require('../controllers/authController')

const router = Router()

router.get('/signup', authController.signup_get)
router.post('/signup', authController.signup_post)
router.get('/login', authController.login_get)
router.post('/login', authController.login_post)

module.exports = router
```


### app:

```js
const authRoutes = require('./routes/authRoutes');

app.use(authRoutes);
```


