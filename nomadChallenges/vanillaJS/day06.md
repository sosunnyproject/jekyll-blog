## 3.1 ~ 3.2 강의

### Save/Load Country Data in LocalStorage

- [select](https://developer.mozilla.org/ko/docs/Web/HTML/Element/select)
- [select.addEventListener("change")](https://developer.mozilla.org/ko/docs/Web/API/HTMLElement/change_event)
- [option](https://developer.mozilla.org/en-US/docs/Web/API/HTMLOptionElement)
- reference from JS Chrome Lectures: [my practice code](https://github.com/sosunnyproject/fullstack-study/blob/master/1.JavascriptChromeApp/greeting.js)


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
