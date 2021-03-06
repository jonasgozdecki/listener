# listener
Fast and easy listener using Google's speechRecognition API.

- Javascript
- Html
- Google API

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

---

## Contents

- [API](#api)
- [Clone](#clone)
- [License](#license)

---

### API

Really easy and fast to understand and play with this API.
Follow all the code to keep it working:


- Google's API demands chrome for better experience :P

```javascript

	function upgrade() {
      alert('Please use Google Chrome for best experience');
    }
	
```

- We just start playing by asking to allow access to the microphone.

```javascript
    window.onload = function() {
      if (!(window.webkitSpeechRecognition) && !(window.speechRecognition)) {
        upgrade();
      } else {
        var recognizing,
        transcription = document.getElementById('speech'),
        interim_span = document.getElementById('interim');

        interim_span.style.opacity = '0.5';

```

- The API has some restrictions, that's why this reset function called at the end of the code.

```javascript
        function reset() {
          recognizing = false;
          interim_span.innerHTML = '';
          transcription.innerHTML = '';
          speech.start();
        }
		
```

- The webkitSpeechRecognition is instanciated or speechRecognition, depending on wha'ts available

```javascript
        var speech = new webkitSpeechRecognition() || speechRecognition();

        speech.continuous = true;
        speech.interimResults = true;
        speech.lang = 'en-US'; // pt-BR to Brazilian portuguese
        speech.start(); //enables recognition on default

        speech.onstart = function() {
            // When recognition begins
            recognizing = true;
        };
		
```

- Here's where all happens. The insterin results keep changing as you speak, each word is analyzed. When fixed, it's merged and so on.
	
```javascript

        speech.onresult = function(event) {
          // When recognition produces result
          var interim_transcript = '';
          var final_transcript = '';

          // main for loop for final and interim results
          for (var i = event.resultIndex; i < event.results.length; ++i) {
            if (event.results[i].isFinal) {
              final_transcript += event.results[i][0].transcript;
            } else {
              interim_transcript += event.results[i][0].transcript;
            }
          }
          transcription.innerHTML = final_transcript;
          interim_span.innerHTML = interim_transcript;
        };
		
```

- The onend function is dispatched by the API when it reached an ammount of silence time.

```javascript

        speech.onerror = function(event) {
            // Either 'No-speech' or 'Network connection error'
            console.error(event.error);
        };

        speech.onend = function() {
            // When recognition ends
            reset();
        };

      }
    };


```

### Using

- Just clone to your desktop and use it, since doesn't requires a webserver.

---

### Clone

- Clone this repo to your local machine using `https://github.com/jonasgozdecki/listener.git`

---

## License

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**