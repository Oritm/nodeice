
[![nodeice](http://i.imgur.com/NuF1OI0.png)](#)

# nodeice

 [![Patreon](https://img.shields.io/badge/Support%20me%20on-Patreon-%23e6461a.svg)][patreon] [![PayPal](https://img.shields.io/badge/%24-paypal-f39c12.svg)][paypal-donations] [![AMA](https://img.shields.io/badge/ask%20me-anything-1abc9c.svg)](https://github.com/IonicaBizau/ama) [![Version](https://img.shields.io/npm/v/nodeice.svg)](https://www.npmjs.com/package/nodeice) [![Downloads](https://img.shields.io/npm/dt/nodeice.svg)](https://www.npmjs.com/package/nodeice) [![Get help on Codementor](https://cdn.codementor.io/badges/get_help_github.svg)](https://www.codementor.io/johnnyb?utm_source=github&utm_medium=button&utm_term=johnnyb&utm_campaign=github)

> Another PDF invoice generator

[![nodeice](http://i.imgur.com/WnUnlFt.png)](#)

## :cloud: Installation

```sh
$ npm i --save nodeice
```


## :clipboard: Example



```js
const Invoice = require("nodeice");

// Create the new invoice
let myInvoice = new Invoice({
    config: {
        template: __dirname + "/template/index.html"
      , tableRowBlock: __dirname + "/template/blocks/row.html"
    }
  , data: {
        currencyBalance: {
            main: 1
          , secondary: 3.67
        }
      , invoice: {
            number: {
                series: "PREFIX"
              , separator: "-"
              , id: 1
            }
          , date: "01/02/2014"
          , dueDate: "11/02/2014"
          , explanation: "Thank you for your business!"
          , currency: {
                main: "XXX"
              , secondary: "ZZZ"
            }
        }
      , tasks: [
            {
                description: "Some interesting task"
              , unit: "Hours"
              , quantity: 5
              , unitPrice: 2
            }
          , {
                description: "Another interesting task"
              , unit: "Hours"
              , quantity: 10
              , unitPrice: 3
            }
          , {
                description: "The most interesting one"
              , unit: "Hours"
              , quantity: 3
              , unitPrice: 5
            }
        ]
    }
  , seller: {
        company: "My Company Inc."
      , registrationNumber: "F05/XX/YYYY"
      , taxId: "00000000"
      , address: {
            street: "The Street Name"
          , number: "00"
          , zip: "000000"
          , city: "Some City"
          , region: "Some Region"
          , country: "Nowhere"
        }
      , phone: "+40 726 xxx xxx"
      , email: "me@example.com"
      , website: "example.com"
      , bank: {
            name: "Some Bank Name"
          , swift: "XXXXXX"
          , currency: "XXX"
          , iban: "..."
        }
    }
  , buyer: {
        company: "Another Company GmbH"
      , taxId: "00000000"
      , address: {
            street: "The Street Name"
          , number: "00"
          , zip: "000000"
          , city: "Some City"
          , region: "Some Region"
          , country: "Nowhere"
        }
      , phone: "+40 726 xxx xxx"
      , email: "me@example.com"
      , website: "example.com"
      , bank: {
            name: "Some Bank Name"
          , swift: "XXXXXX"
          , currency: "XXX"
          , iban: "..."
        }
    }
});

// Render invoice as HTML and PDF
myInvoice.toHtml(__dirname + "/my-invoice.html", (err, data) => {
    console.log("Saved HTML file");
}).toPdf(__dirname + "/my-invoice.pdf", (err, data) => {
    console.log("Saved pdf file");
});

// Serve the pdf via streams (no files)
require("http").createServer((req, res) => {
    myInvoice.toPdf({ output: res });
}).listen(8000);
```

## :memo: Documentation


### `Invoice(options)`
This is the constructor that creates a new instance containing the needed
methods.

#### Params
- **Object** `options`: The options for creating the new invoice:
 - `config` (Object):
   - `template` (String): The HTML root template.
 - `data` (Object):
   - `currencyBalance` (Object):
     - `main` (Number): The main balance.
     - `secondary` (Number): The converted main balance.
     - `tasks` (Array): An array with the tasks (description of the services you did).
     - `invoice` (Object): Information about invoice.
 - `seller` (Object): Information about seller.
 - `buyer` (Object): Information about buyer.

### `initTemplates(callback)`
Inits the HTML templates.

#### Params
- **Function** `callback`: The callback function.

### `toHtml(output, callback)`
Renders the invoice in HTML format.

#### Params
- **String** `output`: An optional path to the output file.
- **Function** `callback`: The callback function.

#### Return
- **Invoice** The `Nodeice` instance.

### `convertToSecondary(input)`
Converts a currency into another currency according to the currency
balance provided in the options

#### Params
- **Number** `input`: The number that should be converted

#### Return
- **Number** The converted input

### `toPdf(options, callback)`
Renders invoice as pdf

#### Params
- **Object|String|Stream** `options`: The path the output pdf file, the stream object, or an object containing:

 - `output` (String|Stream): The path to the output file or the stream object.
 - `converter` (Object): An object containing custom settings for the [`phantom-html-to-pdf`](https://github.com/pofider/phantom-html-to-pdf).
- **Function** `callback`: The callback function

#### Return
- **Invoice** The Invoice instance



## :yum: How to contribute
Have an idea? Found a bug? See [how to contribute][contributing].


## :moneybag: Donations

Another way to support the development of my open-source modules is
to [set up a recurring donation, via Patreon][patreon]. :rocket:

[PayPal donations][paypal-donations] are appreciated too! Each dollar helps.

Thanks! :heart:


## :scroll: License

[MIT][license] © [Ionică Bizău][website]

[patreon]: https://www.patreon.com/ionicabizau
[paypal-donations]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=RVXDDLKKLQRJW
[donate-now]: http://i.imgur.com/6cMbHOC.png

[license]: http://showalicense.com/?fullname=Ionic%C4%83%20Biz%C4%83u%20%3Cbizauionica%40gmail.com%3E%20(http%3A%2F%2Fionicabizau.net)&year=2014#license-mit
[website]: http://ionicabizau.net
[contributing]: /CONTRIBUTING.md
[docs]: /DOCUMENTATION.md
