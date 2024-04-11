I first ran the commands 
```
docker build -t chal .

docker run -p 1337:1337 chal
```
I then was able to get the website at http://<machine_ip>:1337
![Screenshot (6)](https://github.com/Sandeep3084/Cryptonite_Web/assets/148266037/18970682-48e2-49e6-aa1b-39aa029e67e4)

The site is a small book library with books and their author name and nummber of pages.It has a login form and registration and logging in is required by registering a user. There are options to Add books and a search feature.
![image](https://github.com/Sandeep3084/Cryptonite_Web/assets/148266037/a39df502-309d-4310-b1ca-1a4a33fdf3ab)

CSP policy: CSP pilicy: default-src 'self' openlibrary.org;img-src 'self' raw.githubusercontent.com external-content.duckduckgo.com;base-uri 'self';font-src 'self' https: data:;form-action 'self';frame-ancestors 'self';object-src 'none';style-src 'self' https: 'unsafe-inline'

First thing I did was to check for vulnerabilities in the CSP header file, and went to  https://csp-evaluator.withgoogle.com/
![Screenshot (7)](https://github.com/Sandeep3084/Cryptonite_Web/assets/148266037/cdb559b3-99c9-4a8e-9f23-2c8d5d841a25)

Unfortunately there was nothing on the header 

In the scripts.js file, it is just storing the books as JavaScript objects under the class newBook
```
        const book = new newBook(
            title,
            author,
            Number(pages),
            imageLink,
            link,
            formReadSwitch
        );
```

Also, clicking the book name opens a URL in the form of yourip:1337/liteShare/username/bookid. But logging in as another user and then pasting this URL shows a report button.
![image](https://github.com/Sandeep3084/Cryptonite_Web/assets/148266037/1cf8db86-4bda-487d-86d6-367f1694a007)

It could be dealt with CSP bypass, but there are multiple methods to do so such as RPO, Redirection etc. so currently looking at  https://book.hacktricks.xyz/pentesting-web/content-security-policy-csp-bypass in order to find a viable approach. 

JSONP replies may be a possible way to exploit the JavaScript code and trying to figure out a suitable payload would be the work here.


