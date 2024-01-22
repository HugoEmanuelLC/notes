# Bcrypt

```js
// npm i bcrypt
const bcrypt = require('bcrypt');

// hashage de la password
const salt = await bcrypt.genSalt();
this.password = await bcrypt.hash(this.password, salt);

// if user existe
const auth = bcrypt.compare(password, user.password)
```