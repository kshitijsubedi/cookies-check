# 3rd Party Cookies Check
Check Whether Browser supports Third Party Cookies or not.

[Test URL to check 🍪] https://cookies-check-kshitijsubedi.vercel.app/test.html

<img src="https://media.giphy.com/media/xT0xeMA62E1XIlup68/giphy.gif" />

[Use this URL as iFrame ⚡️](https://cookies-check.vercel.app)

## Example Usage
```

/**
 * It creates an iframe, loads a page into it, and then sends a message to the iframe to check if
 * cookies are enabled
 * @param iFrameUri - The URI of the iFrame that will be used to check for cookies.
 * @returns A promise that resolves to a boolean.
 */

export function cookieTest(iFrameUri) {
  return new Promise(function (resolve, reject) {
    try {
      let messageHandler = (event) => {
        const data = JSON.parse(event.data);
        window.removeEventListener('message', messageHandler);
        document.body.removeChild(frame);
        resolve(data['result']);
      };
      window.addEventListener('message', messageHandler);
      const frame = document.createElement('iframe');
      frame.src = iFrameUri;
      frame.sandbox = 'allow-scripts allow-same-origin';
      frame.style = `display:none`;
      frame.onload = (e) => {
        frame.contentWindow.postMessage(
          JSON.stringify({ test: 'cookie' }),
          '*'
        );
      };
      document.body.appendChild(frame);
    } catch (err) {
      reject(new Error('Error Checking Cookies', err));
    }
  });
}

```
Get the result.
```
let result = await cookieTest('https://cookies-check.vercel.app');
console.log('Result', result);
```
