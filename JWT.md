# JWT 

***JSON Web Tokens are ONE way to implement authentification***

### Creation du token

- controllers/authController.js

```js
// npm i jsonwebtoken

const jwt = require('jsonwebtoken');

const maxAge = 3 * 24 * 60 * 60; // temps du cookie
const createToken = (id)=>{
    return jwt.sign({ id }, 'net ninja secret', {
        expiresIn: maxAge
    })
}
```


### exemple d'utilisation:

- controllers/authController.js

```js
module.exports.signup_post = async (req, res) => {
    const {email, password} = req.body
    try {
        const user = await User.create({email, password});
        // debut du token
        const token = createToken(user._id)
        res.cookie('jwt', token, {httpOnly: true, maxAge: maxAge * 1000})
        res.status(201).json({user: user._id})
        // fin du token
    } catch (err) {
        const errors = handleErrors(err)
        res.status(400).json({errors})
    }
}
```