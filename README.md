# Translate Worthing

Translate words or phrases, with just hover, using any dictionary!

## Why?

You're viewing a page in, say, English. Of course you know English, but suddenly you see an unknown word: "scrumptious". Woe, what's that? I don't know. English isn't my native language. So I open my online dictionary (I use https://morfix.com - recommended for English-Hebrew and Hebrew-English translations!),
type the new word, (I always type the whole URL, including the word - https://morfix.com/scrumptious).
And yeah, we found the translation! ("(of food) extremely tasty; delicious" Google said, if you're curious).

That's annoying. So, why are we developers if not to solve such annoying tasks? :sunglasses:

## What are the Supported Browsers?

Currently, only Chrome. Pull Requests are welcomed!

## How?

The concept is really simple, and works as follows:

When you hover over a word or selection, the extensions waits for some seconds. Why? to not flood your network with infinite number of requests.

If timeout passed and mouse is still over, it determines the page language using HTML's `lang` attribute. If you do not trust your pages, you can tell it to skip this step and match any language.

After the language found, it will fetch the list of matching dictionaries from the settings (explained later). Then it sends request to the servers by order. The first one that succeed win. If you want, however, you can configure it to send the requests in parallel (faster responses but more bandwidth).

Finally, the translation is shown in the status bar (where links are shown on hover). You can configure whether to remove the translation on mouse out (default), or leave it as-is until the next one.

## How Do I Configure Dictionaries?

The settings contains list of dictionaries, each one with:

 - The server URL, where `${phrase}` will be replaced by the searched word/phrase.
 - Regular expression (JavaScript version) for failure: if match the response, the extension understands there is no translation in this dictionary.
 - Regular expression to capture the translation for success: named group `translation` will be used. All matches are displayed, separated by commas.

Don't know regular expressions? [Here is an excellent guid](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions).

If you're lucky, and your dictionary has an API which returns JSON or XML, you can define the simpler following settings:

 - The server url, you can specify `${phrase}` as above.
 - The request's body type: None (there is no body), JSON or XML. This field affects the encoding of the query.
 - The request's body, `${phrase}` is the placeholder.
 - The response's body type: JSON or XML.
 - The response body path: XPath for XML (you can read more about XPath [here](https://www.w3schools.com/xml/xpath_intro.asp)), and JavaScript-like syntax for JSON, i.e. `object.property.array[0].otherProperty`.
