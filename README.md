# [node_zuora](https://github.com/joyent/node_zuora.git)

This is a node.js client library for interacting with the Zuora
SOAP interface.


## Installation

You probably want to install this package using npm

    npm install zuora-soap


## Configuration

You will need to get your config setup as follows:

- [Download your WSDL][1] file by visiting Settings -> Z-Billing settings -> [Download WSDL][1].    
- Create an API user account by visiting settings -> Admin settings -> [Add single user][2]
Disable [password expiry][3] for API accounts.
- You may also want to adjust session timeout from the 15 minute default to something longer. Visit Settings -> Administrative Settings -> Security Policies    
- Save the username and password of the API user with the path to your WSDL:

```json
    {
      "user":     "zuora_api_user@my_favourite.com",
      "password": "password123",
      "wsdl":     "./etc/zuora.a.64.0.wsdl",
      "verboseLog": false
    }
```

[1]: https://www.zuora.com/apps/Api.do
[2]: https://www.zuora.com/apps/UserLogin.do?method=edit&flag=1
[3]: https://knowledgecenter.zuora.com/kb/How_do_I_prevent_my_API_user_login_from_expiring%3F

## Usage

### Programmatic Usage

```javascript
    var zuora = require('zuora');

    var config = require('your_config.json');

    zuora.connect(config, function(err, z) {
        if (err) return console.log('Error connecting:', err);
        var contactDetails = {
             FirstName: 'Homer',
             LastName:  'Simpson',
             WorkEmail: 'Homer@TheSimpsons.tv'
        };
        z.contact.create(contactDetails, function(err, result) {
            if (err) return console.log(err.message);
            z.query('select accountnumber from account where status = "Active"', function(err, result) {
                if (err) return console.log(err.message);
                // inspect result
            })
        })
    });
```

[Object list](http://knowledgecenter.zuora.com/BC_Developers/SOAP_API/E1_SOAP_API_Object_Reference)

[Zuora API documentation](http://knowledgecenter.zuora.com/) for complete information:

Check out the source documentation for docs on the API.

## Alternatives

If this isn't your cup of tea when it comes to soap, then perhaps [@Sparkida's][14] [Nuora][11], [Nuora-MVC][12] or @DeadAlready's [Zuora][13] with Rest may fit your tastes.

[11]: https://github.com/node-zuora/nuora
[12]: https://github.com/node-zuora/nuora-mvc
[13]: https://www.npmjs.com/package/zuora
[14]: https://github.com/sparkida


## License

MIT.

## Contributions are welcome

See <https://github.com/joyent/node_zuora/issues>.
