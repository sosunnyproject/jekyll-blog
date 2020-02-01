## 3.1 ~ 3.2 강의

### Save/Load Country Data in LocalStorage

- [select](https://developer.mozilla.org/ko/docs/Web/HTML/Element/select)
- [select.addEventListener("change")](https://developer.mozilla.org/ko/docs/Web/API/HTMLElement/change_event)
- [option](https://developer.mozilla.org/en-US/docs/Web/API/HTMLOptionElement)
- reference from JS Chrome Lectures: [my practice code](https://github.com/sosunnyproject/fullstack-study/blob/master/1.JavascriptChromeApp/greeting.js)
- [제출한 코드 샌드박스](https://codesandbox.io/s/day-six-blueprint-1nwd0)

1차
- option[index]
- option value 값 대신 index 숫자를 사용

```js
const select = document.querySelector("select");
const options = document.querySelectorAll("option");
const LOCATION_IND = "country_index";

// when option changed, save in localStorage
function saveLocation() {
  // get current location data
  let locIndex = localStorage.getItem(LOCATION_IND);

  // check which option is selected
  for (let i = 0; i < options.length; i++) {
    if (options[i].selected) {
      locIndex = i;
    }
  }

  // save in localStorage
  localStorage.setItem(LOCATION_IND, locIndex);
}

function loadLocation() {
  // get data from localStorage
  const locIndex = localStorage.getItem(LOCATION_IND);

  // print localStorage data
  // load localStorage data into select/option box
  if (locIndex != null) {
    select.options.selectedIndex = locIndex;
  }
}

function init() {
  loadLocation();
}

init();
select.addEventListener("change", saveLocation);
```

2차
- option.value 를 저장하고 사용해보기
- for loop 대신 forEach 사용해봄

```js
const COUNTRY = "country"; // 2차

// when option changed, save in localStorage
function saveLocation() {
  // get current location data
  let country = localStorage.getItem(COUNTRY);

  // check which option is selected
  for (let i = 0; i < options.length; i++) {
    if (options[i].selected) {
      if (options[i].value === "") {   // choose your country 선택시
        localStorage.setItem(COUNTRY, null);
      } else {                         // 그 외 선택시
        country = options[i].value;
        h2.innerText = `You selected ${options[i].text}`;
        localStorage.setItem(COUNTRY, country);
      }
    }
  }
}

function loadLocation() {
  // get data from localStorage
  const country = localStorage.getItem(COUNTRY);
  // let countryIndex = 0; // change dropdown option by option[index]

  // load localStorage data into select/option box
  if (country != null) {
    options.forEach(option => {
      if (option.value === country) {
        h2.innerText = `You previously selected ${option.text}`;
        option.selected = true;
        // countryIndex = option.index;
      }
    });

    // console.log(select.selectedOptions[0].value);
    // https://stackoverflow.com/questions/4633878/how-to-get-the-index-of-value-in-drop-down-in-javascript
    // select.options.selectedIndex = countryIndex;
  }
}

function init() {
  loadLocation();
}
 // 이하 생략
```
