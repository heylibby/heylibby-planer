# heylibby-planer
Package forked from [lever/planer](https://github.com/lever/planer) to update the functionality support for many languages.

-------------------

Remove reply quotations from emails.

At [lever](https://github.com/lever) we are into simple machines. 
A planer removes some material to flatten out a rough surface, which seemed appropriate for a module that smooths out an email to extract the actual message.

This is essentially a javascript port of Mailgun's awesome [`talon`](https://github.com/mailgun/talon) python library.
Planer does not do signatures, though there is a [node port](https://github.com/lmtm/node-talon) of that part of talon.

# Installation
Use npm to install planer (add `-g` if you would like it to be global):

`npm install @heylibby/heylibby-planer`

# Usage

_Important_: planer accepts an injected [Document](https://developer.mozilla.org/en-US/docs/Web/API/Document) object to perform html parsing.
You can use `window.document` in a browser, or something akin to `jsdom` on the server. 
We use `jsdom` in our test suite.

To extract the message from a plain text email:
```
planer = require('@heylibby/heylibby-planer');

msgBody = "Reply!\n\nOn 15-Dec-2011, at 6:54 PM, Sean Carter <s.carter@example.com> wrote:\n> It's the ROC!\n>-Sean";
actualMessage = planer.extractFrom(msgBody, 'text/plain');
console.log(actualMessage); # "Reply!"
```

To extract the message from an html email:
```
planer = require('@heylibby/heylibby-planer');

msgBody = 'Reply!\n<div>\nOn 11-Apr-2011, at 6:54 PM, Bob &lt;bob@example.com&gt; wrote:\n</div>\n<blockquote>\n<div>\nTest\n</div>\n</blockquote>';
actualMessage = planer.extractFrom(msgBody, 'text/html', window.document);
console.log(actualMessage) # "<html><body>Reply!\n</body></html>";
```

# Languages covered:
## On {date}, {somebody} wrote: && On {date} wrote {somebody}:
Arabic (على, عند)
Swahili
Hausa
Yoruba
Amharic
Zulu
Mandarin Chinese
Hindi
Bengali
Telugu
Urdu
Indonesian
Japanese
Korean
Vietnamese
English (En)
Spanish (Es)
French (Le, La, Il)
German (De, Auf, In, An)
Italian (Al, I)
Portuguese (Por)
Russian (Ru)
Dutch (Nl)
Swedish (Se)
Norwegian (No)
Turkish
Persian (Farsi)
Hebrew
## ORIGINAL_MESSAGE:
 
English (Original Message, Reply Message)
German (Ursprüngliche Nachricht, Antwort Nachricht)
Danish (Oprindelig meddelelse, Svarmeddelelse)
French (Message d'origine, Réponse)
Italian (Messaggio originale, Risposta)
Norwegian (Melding, Svar)
For the third pattern (email header detection):

## FROM_COLON_OR_DATE_COLON
English (From, Date)
Dutch (Van, De)
German (Von, Datum)
Danish (Fra, Skickat, Sendt)
Swedish (Från, Skickat, Sendt)
Italian (Da)
Norwegian (Sendt)
Arabic (من, إلى)
Spanish (De, Para)
Portuguese (De, Para)
Quechua
Guarani
Nahuatl
Maori
Inuktitut

# Contributing

Contributions are of course encouraged.
Keep in mind that the source is the `coffee` files; the `js` files in `/lib` are kept around for convenience.

Write tests for any new functionality.
Run `npm run compile` to compile the source into javascript files before submitting a pull request.


# MIT Licence

Copyright (c) 2015 Leighton Wallace

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
