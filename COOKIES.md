# COOKIES

### creation et access aux cookies

- app.js

```js
// npm i cookie-parser
const cookieParser = require('cookie-parser');

app.use(cookieParser())

// exemple cookies
app.get('/set-cookie', (req, res)=>{
  res.cookie('newUser', false);

  res.cookie('isEmployee', true, {
    maxAge: 1000 * 60 * 60 * 24, // duration du cookie
    httpOnly: true //protection contre les tentetive d access avec js 
  });

  res.send('you got the cookies ! ');
})
```