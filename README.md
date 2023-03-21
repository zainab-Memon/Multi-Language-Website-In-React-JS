# Multi-Language-Website-In-React-JS
## STEP-1: Install i18next Library
``` jsx 
npm install react-i18next i18next --save
```
## STEP-2: Create an i18n.js file inside the src directory and paste the below code.
```jsx
    import i18n from "i18next";
    import { initReactI18next } from "react-i18next";
    import translationEN from "./locales/en/translation.json";
    import translationVN from "./locales/vn/translation.json";

    i18n
    .use(initReactI18next) // passes i18n down to react-i18next
    .init({
      // the translations
      // (tip move them in a JSON file and import them,
      // or even better, manage them via a UI: https://react.i18next.com/guides/multiple-translation-files#manage-your-translations-with-a-management-gui)
      resources: {
        en: {
          translation: translationEN,
        },
        vn: {
          translation: translationVN,
        },
      },
      lng: localStorage.getItem("lang") || "en", // if you're using a language detector, do not define the lng option
      fallbackLng: "en",

      interpolation: {
        escapeValue: false, // react already safes from xss => https://www.i18next.com/translation-function/interpolation#unescape
      },
    });

```
## STEP-3: import the above file in index.js
```jsx
    import React from "react";
    import ReactDOM from "react-dom/client";
    import "./index.css";
    import App from "./App";
    import "./i18n";
    const root = ReactDOM.createRoot(document.getElementById("root"));
    root.render(
      <React.StrictMode>
        <App />
      </React.StrictMode>
    );

```
## STEP - 4: Create translation files in the src directory like this one:
```jsx
{
  "welcome": "Welcome to React"
}
```
- Path: import translationEN from "./locales/en/translation.json";
## STEP-5: Copy this code in APP.js
```jsx
    import "./App.css";
    import { useTranslation } from "react-i18next";
    import { useEffect } from "react";
    function App() {
      //Calling t and i18n method from useTranslation hook
      const { t, i18n } = useTranslation();

      //Creating a method to change the language onChnage from select box
      const changeLanguageHandler = (e) => {
        const languageValue = e.target.value;
        i18n.changeLanguage(languageValue);
        // setting to local storage
        localStorage.setItem("lang", languageValue);
      };

      return (
        <div className="App">
          {/* Select box to change language */}
          <select
            className="custom-select"
            style={{ width: 200 }}
            onChange={changeLanguageHandler}
          >
            <option selected>Choose Lang</option>
            <option value="en">English</option>
            <option value="vn">Vietnam</option>
          </select>
          {/* call name of the variable from  the translation.json file to t() method */}
          <h1>{t("welcome")}</h1>
        </div>
      );
    }

    export default App;

```
