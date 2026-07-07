# راهنمای نوشتاری جاوااسکریپتِ Airbnb() {

*رویکردی، تا حد زیاد معقول به جاوااسکریپت*

> **نکته**: این راهنما فرض می‌کند از [Babel](https://babeljs.io) استفاده می‌کنید و نیاز دارد از [babel-preset-airbnb](https://npmjs.com/babel-preset-airbnb) یا معادل آن استفاده کنید. همچنین فرض می‌کند شیم/پُلی‌فیل‌ها را در نرم افزار خود نصب می‌کنید، با [airbnb-browser-shims](https://npmjs.com/airbnb-browser-shims) یا معادل آن.

[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb.svg)](https://www.npmjs.com/package/eslint-config-airbnb)
[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb-base.svg)](https://www.npmjs.com/package/eslint-config-airbnb-base)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/airbnb/javascript?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

این راهنما به زبان‌های دیگری هم در دسترس است. [ترجمه](#translation) را ببینید

راهنماهای سبک دیگر

  - [ES5 (Deprecated)](https://github.com/airbnb/javascript/tree/es5-deprecated/es5)
  - [React](react/)
  - [CSS-in-JavaScript](css-in-javascript/)
  - [CSS & Sass](https://github.com/airbnb/css)
  - [Ruby](https://github.com/airbnb/ruby)

## فهرست مطالب

1. [انواع (types)](#انواع-types)
1. [ارجاعات (references)](#ارجاعات-references)
1. [شئ ها](#شئ-ها)
1. [آرایه ها](#آرایه-ها)
1. [ساختارزدایی (destructuring)](#ساختارزدایی-Destructuring)
1. [رشته ها (strings)](#رشته-ها-strings)
1. [توابع](#توابع)
1. [توابع پیکانی](#توابع-پیکانی)
1. [کلاس ها و سازنده ها](#کلاس-ها-و-سازنده-ها)
1. [ماژول ها (modules)](#ماژول-ها-modules)
1. [تکرارکننده ها و مولد ها (Iterators and Generators)](#تکرارکننده-ها-و-مولد-ها-Iterators-and-Generators)
1. [ویژگی ها (properties)](#ویژگی-ها-properties)
1. [متغیر ها](#متغیر-ها)
1. [بالا آوردن (Hoisting)](#بالا-آوردن-Hoisting)
1. [عملگرهای مقایسه و برابری](#comparison-operators--equality)
1. [بلوک‌ها](#blocks)
1. [دستورهای کنترلی](#control-statements)
1. [توضیحات (comments)](#comments)
1. [فاصله‌گذاری](#whitespace)
1. [ویرگول‌ها](#commas)
1. [نقطه‌ویرگول‌ها](#semicolons)
1. [تبدیل نوع و واداشتن به تبدیل (Coercion)](#type-casting--coercion)
1. [مقررات نام‌گذاری](#naming-conventions)
1. [اکسسورها (Accessors)](#accessors)
1. [رویدادها (events)](#events)
1. [jQuery](#jquery)
1. [سازگاری با ECMAScript 5](#ecmascript-5-compatibility)
1. [سبک‌های ECMAScript 6+ (ES 2015+)](#ecmascript-6-es-2015-styles)
1. [کتابخانه استاندارد](#standard-library)
1. [آزمایش](#testing)
1. [کارایی](#performance)
1. [منابع](#resources)
1. [در دنیای واقعی](#in-the-wild)
1. [ترجمه](#translation)
1. [راهنمای راهنمای سبک جاوااسکریپت](#the-javascript-style-guide-guide)
1. [با ما درباره جاوااسکریپت گپ بزنید](#chat-with-us-about-javascript)
1. [همکاران](#contributors)
1. [مجوز](#license)
1. [اصلاحیه‌ها](#amendments)


## انواع (Types)

  <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) **بدویات (Primitives)**: وقتی به یک نوع بدوی دسترسی پیدا می‌کنید، مستقیماً با مقدار آن نوع کار می‌کنید.

    - `string`
    - `number`
    - `boolean`
    - `null`
    - `undefined`
    - `symbol`
    - `bigint`

    <br />

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

    - سمبل‌ها (Symbols) و BigIntها را نمی‌توان به‌طور قطع پُلی‌فیل کرد، بنابراین وقتی برای مرورگرها/محیط‌هایی هدف‌گیری می‌کنید که از آن‌ها به‌صورت بومی پشتیبانی نمی‌کنند، نباید از آن‌ها استفاده کنید.

  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **پیچیده (Complex)**: وقتی به یک نوع پیچیده دسترسی پیدا می‌کنید، با یک ارجاع به مقدار آن نوع کار می‌کنید.

    - `object`
    - `array`
    - `function`

    <br />

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## ارجاعات (References)

  <a name="references--prefer-const"></a><a name="2.1"></a>
  - [2.1](#references--prefer-const) برای همهٔ ارجاع‌های خود از `const` استفاده کنید؛ از `var` استفاده نکنید. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const)، [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign)

    > چرا؟ این کار باعث می‌شود نتوانید ارجاع‌های خود را دوباره انتساب دهید، و همین می‌تواند از ایجاد باگ‌ها و کدهایی که فهم آن‌ها دشوار است جلوگیری کند.

    ```javascript
    // بد
    var a = 1;
    var b = 2;

    // خوب
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) اگر مجبورید ارجاع‌ها را دوباره انتساب دهید، به‌جای `var` از `let` استفاده کنید. eslint: [`no-var`](https://eslint.org/docs/rules/no-var)

    > چرا؟ `let` دامنهٔ بلوکی دارد، نه دامنهٔ تابعی مثل `var`.

    ```javascript
    // بد
    var count = 1;
    if (true) {
      count += 1;
    }

    // خوب، از let استفاده کنید
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  <a name="references--block-scope"></a><a name="2.3"></a>
  - [2.3](#references--block-scope) توجه کنید که هم `let` و هم `const` دامنهٔ بلوکی دارند، در حالی که `var` دامنهٔ تابعی دارد.

    ```javascript
    // `const` و `let` فقط در همان بلوک‌هایی وجود دارند که در آن‌ها تعریف شده‌اند.
    {
      let a = 1;
      const b = 1;
      var c = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    console.log(c); // چاپ می شود 1
    ```

    در کد بالا می‌بینید که ارجاع به `a` و `b` باعث ایجاد ReferenceError می‌شود، در حالی که `c` عدد را در خود نگه می‌دارد. این به این دلیل است که `a` و `b` دامنهٔ بلوکی دارند، در حالی که `c` به تابعِ دربرگیرنده محدود است.

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## شئ ها

  <a name="objects--no-new"></a><a name="3.1"></a>
  - [3.1](#objects--no-new) برای ساخت شئ‌ها از ساختار دقیق (literal syntax) استفاده کنید. eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object)

    ```javascript
    // بد
    const item = new Object();

    // خوب
    const item = {};
    ```

  <a name="es6-computed-properties"></a><a name="3.4"></a>
  - [3.2](#es6-computed-properties) هنگام ساخت شئ‌هایی با نام ویژگی های پویا، از نام ویژگی‌های محاسبه‌شده (computed property names) استفاده کنید.

    > چرا؟ این کار به شما اجازه می‌دهد تمام ویژگی‌های یک شئ را در یک مکان تعریف کنید.

    ```javascript

    function getKey(k) {
      return `a key named ${k}`;
    }

    // بد
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // خوب
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
    ```

  <a name="es6-object-shorthand"></a><a name="3.5"></a>
  - [3.3](#es6-object-shorthand) از مخفف‌نویسی متدهای شئ (object method shorthand) استفاده کنید. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand)

    ```javascript
    // بد
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // خوب
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

  <a name="es6-object-concise"></a><a name="3.6"></a>
  - [3.4](#es6-object-concise) از مخفف‌نویسی مقدار ویژگی (property value shorthand) استفاده کنید. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand)

    > چرا؟ کوتاه‌تر و گویاتر است.

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // بد
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // خوب
    const obj = {
      lukeSkywalker,
    };
    ```

  <a name="objects--grouped-shorthand"></a><a name="3.7"></a>
  - [3.5](#objects--grouped-shorthand) ویژگی‌های مخفف‌نویسی‌شده را در ابتدای تعریف شئ خود گروه‌بندی کنید.

    > چرا؟ تشخیص اینکه کدام ویژگی‌ها از مخفف‌نویسی استفاده می‌کنند، راحت‌تر است.

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // بد
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // خوب
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

  <a name="objects--quoted-props"></a><a name="3.8"></a>
  - [3.6](#objects--quoted-props) فقط ویژگی‌هایی که شناسه (identifier) نامعتبری هستند را داخل کوتیشن قرار دهید. eslint: [`quote-props`](https://eslint.org/docs/rules/quote-props)

    > چرا؟ به طور کلی، خواندن آن را راحت‌تر می‌دانیم. هایلایت کردن سینتکس را بهبود می‌بخشد و توسط بسیاری از موتورهای JS راحت‌تر بهینه‌سازی می‌شود.

    ```javascript
    // بد
    const bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };

    // خوب
    const good = {
      foo: 3,
      bar: 4,
      'data-blah': 5,
    };
    ```

  <a name="objects--prototype-builtins"></a>
  - [3.7](#objects--prototype-builtins) متدهای `Object.prototype` مانند `hasOwnProperty`، `propertyIsEnumerable` و `isPrototypeOf` را مستقیماً فراخوانی نکنید. eslint: [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)

    > چرا؟ این متدها ممکن است توسط ویژگی‌های روی شئ مورد نظر پنهان شوند (shadowed) - برای مثال `{ hasOwnProperty: false }` را در نظر بگیرید - و یا ممکن است شئ، یک شئ تهی (null object) باشد (`Object.create(null)`). در مرورگرهای مدرنی که از ES2022 پشتیبانی می‌کنند، یا با یک پُلی‌فیل مانند <https://npmjs.com/object.hasown>، می‌توان از `Object.hasOwn` به عنوان جایگزینی برای `Object.prototype.hasOwnProperty.call` استفاده کرد.

    ```javascript
    // بد
    console.log(object.hasOwnProperty(key));

    // خوب
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    // بهتر
    const has = Object.prototype.hasOwnProperty; // جستجو را یک بار، در دامنه ماژول کش کنید.
    console.log(has.call(object, key));

    // بهترین
    console.log(Object.hasOwn(object, key)); // فقط در مرورگرهایی که از ES2022 پشتیبانی می‌کنند، پشتیبانی می‌شود

    /* یا */
    import has from 'has'; // https://www.npmjs.com/package/has
    console.log(has(object, key));
    /* یا */
    console.log(Object.hasOwn(object, key)); // https://www.npmjs.com/package/object.hasown
    ```

  <a name="objects--rest-spread"></a>
  - [3.8](#objects--rest-spread) برای کپی سطحی (shallow-copy) کردن شئ‌ها، به جای [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) از سینتکس spread شئ‌ها استفاده کنید. برای به دست آوردن یک شئ جدید با حذف شدن برخی ویژگی‌ها، از سینتکس پارامتر rest شئ‌ها استفاده کنید. eslint: [`prefer-object-spread`](https://eslint.org/docs/rules/prefer-object-spread)

    ```javascript
    // خیلی بد
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); // این کار `original` را تغییر می‌دهد ಠ_ಠ
    delete copy.a; // این هم همینطور

    // بد
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // خوب
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## آرایه ها

  <a name="arrays--literals"></a><a name="4.1"></a>
  - [4.1](#arrays--literals) برای ساخت آرایه‌ها از ساختار دقیق (literal syntax) استفاده کنید. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor)

    ```javascript
    // بد
    const items = new Array();

    // خوب
    const items = [];
    ```

  <a name="arrays--push"></a><a name="4.2"></a>
  - [4.2](#arrays--push) برای اضافه کردن آیتم‌ها به یک آرایه، به جای انتساب مستقیم از [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) استفاده کنید.

    ```javascript
    const someStack = [];

    // بد
    someStack[someStack.length] = 'abracadabra';

    // خوب
    someStack.push('abracadabra');
    ```

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  - [4.3](#es6-array-spreads) برای کپی کردن آرایه‌ها از عملگر spread یعنی `...` استفاده کنید.

    ```javascript
    // بد
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // خوب
    const itemsCopy = [...items];
    ```

  <a name="arrays--from"></a>
  <a name="arrays--from-iterable"></a><a name="4.4"></a>
  - [4.4](#arrays--from-iterable) برای تبدیل یک شئ قابل پیمایش (iterable) به آرایه، به جای [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) از عملگر spread یعنی `...` استفاده کنید.

    ```javascript
    const foo = document.querySelectorAll('.foo');

    // خوب
    const nodes = Array.from(foo);

    // بهترین
    const nodes = [...foo];
    ```

  <a name="arrays--from-array-like"></a>
  - [4.5](#arrays--from-array-like) برای تبدیل یک شئ شبیه به آرایه (array-like) به آرایه، از [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) استفاده کنید.

    ```javascript
    const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

    // بد
    const arr = Array.prototype.slice.call(arrLike);

    // خوب
    const arr = Array.from(arrLike);
    ```

  <a name="arrays--mapping"></a>
  - [4.6](#arrays--mapping) برای نگاشت (map) روی اشیاء قابل پیمایش (iterable)، به جای spread یعنی `...` از [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) استفاده کنید، زیرا از ایجاد یک آرایه واسطه جلوگیری می‌کند.

    ```javascript
    // بد
    const baz = [...foo].map(bar);

    // خوب
    const baz = Array.from(foo, bar);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.7](#arrays--callback-return) در توابع کال‌بک (callback) متدهای آرایه، از دستور `return` استفاده کنید. اگر بدنهٔ تابع از یک دستور واحد تشکیل شده باشد که یک عبارت بدون اثرات جانبی را برمی‌گرداند، طبق قانون [8.2](#arrows--implicit-return) حذف کردن `return` مشکلی ندارد. eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)

    ```javascript
    // خوب
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // خوب
    [1, 2, 3].map((x) => x + 1);

    // بد - عدم برگرداندن مقدار به این معنی است که `acc` پس از اولین تکرار تبدیل به undefined می‌شود
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
    });

    // خوب
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      return flatten;
    });

    // بد
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // خوب
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

  <a name="arrays--bracket-newline"></a>
  - [4.8](#arrays--bracket-newline) اگر یک آرایه در چند خط قرار دارد، بعد از براکت بازکننده و قبل از براکت بسته‌کنندهٔ آرایه، خط‌شکن (خط جدید) قرار دهید.

    ```javascript
    // بد
    const arr = [
      [0, 1], [2, 3], [4, 5],
    ];

    const objectInArray = [{
      id: 1,
    }, {
      id: 2,
    }];

    const numberInArray = [
      1, 2,
    ];

    // خوب
    const arr = [[0, 1], [2, 3], [4, 5]];

    const objectInArray = [
      {
        id: 1,
      },
      {
        id: 2,
      },
    ];

    const numberInArray = [
      1,
      2,
    ];
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## ساختارزدایی (Destructuring)

  <a name="destructuring--object"></a><a name="5.1"></a>
  - [5.1](#destructuring--object) هنگام دسترسی و استفاده از چندین ویژگیِ یک شئ، از ساختارزدایی شئ (object destructuring) استفاده کنید. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    > چرا؟ ساختارزدایی شما را از ایجاد ارجاعات موقت برای آن ویژگی‌ها و از دسترسی تکراری به شئ بی‌نیاز می‌کند. دسترسی تکراری به شئ باعث ایجاد کدهای تکراری‌تر می‌شود، نیاز به خواندن بیشتری دارد و فرصت‌های بیشتری برای ایجاد اشتباه فراهم می‌کند. علاوه بر این، ساختارزدایی شئ‌ها یک مکان واحد برای تعریف ساختار شئ فراهم می‌کند که در آن بلوک استفاده می‌شود، به جای اینکه نیاز باشد کل بلوک را بخوانید تا بفهمید چه چیزهایی استفاده شده است.

    ```javascript
    // بد
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // خوب
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // بهترین
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

  <a name="destructuring--array"></a><a name="5.2"></a>
  - [5.2](#destructuring--array) از ساختارزدایی آرایه (array destructuring) استفاده کنید. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    ```javascript
    const arr = [1, 2, 3, 4];

    // بد
    const first = arr[0];
    const second = arr[1];

    // خوب
    const [first, second] = arr;
    ```

  <a name="destructuring--object-over-array"></a><a name="5.3"></a>
  - [5.3](#destructuring--object-over-array) برای مقادیر بازگشتی متعدد، از ساختارزدایی شئ استفاده کنید، نه از ساختارزدایی آرایه.

    > چرا؟ می‌توانید به مرور زمان ویژگی‌های جدیدی اضافه کنید یا ترتیب چیزها را تغییر دهید بدون اینکه جایگاه‌های فراخوانی (call sites) خراب شوند.

    ```javascript
    // بد
    function processInput(input) {
      // سپس یک معجزه رخ می‌دهد
      return [left, right, top, bottom];
    }

    // فراخواننده باید به ترتیب داده‌های بازگشتی فکر کند
    const [left, __, top] = processInput(input);

    // خوب
    function processInput(input) {
      // سپس یک معجزه رخ می‌دهد
      return { left, right, top, bottom };
    }

    // فراخواننده فقط داده‌هایی که نیاز دارد را انتخاب می‌کند
    const { left, top } = processInput(input);
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## رشته ها (Strings)

  <a name="strings--quotes"></a><a name="6.1"></a>
  - [6.1](#strings--quotes) برای رشته‌ها از کوتیشن تکی `''` استفاده کنید. eslint: [`quotes`](https://eslint.org/docs/rules/quotes)

    ```javascript
    // بد
    const name = "Capt. Janeway";

    // بد - رشته‌های قالبی (template literals) باید شامل درج متغیر (interpolation) یا خطوط جدید باشند
    const name = `Capt. Janeway`;

    // خوب
    const name = 'Capt. Janeway';
    ```

  <a name="strings--line-length"></a><a name="6.2"></a>
  - [6.2](#strings--line-length) رشته‌هایی که باعث می‌شوند طول خط از ۱۰۰ کاراکتر بیشتر شود، نباید با استفاده از الحاق رشته‌ها (string concatenation) در چند خط نوشته شوند.

    > چرا؟ کار با رشته‌های شکسته (چند خطی شده با الحاق) دردناک است و کد را کمتر قابل جستجو می‌کند.

    ```javascript
    // بد
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // بد
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // خوب
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals"></a><a name="6.4"></a>
  - [6.3](#es6-template-literals) هنگام ساخت رشته‌ها به صورت برنامه‌نویسی‌شده، به جای الحاق از رشته‌های قالبی (template strings) استفاده کنید. eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

    > چرا؟ رشته‌های قالبی سینتکسی خوانا و مختصر با قابلیت‌های خطوط جدید مناسب و درج متغیر به شما می‌دهند.

    ```javascript
    // بد
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // بد
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // بد
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // خوب
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  <a name="strings--eval"></a><a name="6.5"></a>
  - [6.4](#strings--eval) هرگز روی یک رشته از `eval()` استفاده نکنید؛ این کار آسیب‌پذیری‌های زیادی ایجاد می‌کند. eslint: [`no-eval`](https://eslint.org/docs/rules/no-eval)

  <a name="strings--escaping"></a>
  - [6.5](#strings--escaping) کاراکترها را در رشته‌ها بدون دلیل escape نکنید. eslint: [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)

    > چرا؟ بک‌اسلش‌ها خوانایی را کاهش می‌دهند، بنابراین باید تنها در صورت نیاز، وجود داشته باشند.

    ```javascript
    // بد
    const foo = '\'this\' \i\s \"quoted\"';

    // خوب
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## توابع

  <a name="functions--declarations"></a><a name="7.1"></a>
  - [7.1](#functions--declarations) به جای اعلان توابع (function declarations)، از عبارات توابعِ نام‌گذاری‌شده (named function expressions) استفاده کنید. eslint: [`func-style`](https://eslint.org/docs/rules/func-style), [`func-names`](https://eslint.org/docs/latest/rules/func-names)

    > چرا؟ اعلان توابع بالا آورده می‌شوند (hoisted)، به این معنی که ارجاع به تابع قبل از تعریف آن در فایل، بسیار آسان است - بیش از حد آسان. این کار به خوانایی و قابلیت نگهداری آسیب می‌زند. اگر متوجه شدید که تعریف یک تابع به قدری بزرگ یا پیچیده است که در درک بقیه فایل اختلال ایجاد می‌کند، شاید زمان آن رسیده که آن را در ماژول جداگانه‌ای استخراج کنید! فراموش نکنید که نام عبارت را صریحاً مشخص کنید، صرف نظر از اینکه آیا نام از متغیر نگهدارنده‌اش استخراج می‌شود یا خیر (که اغلب در مرورگرهای مدرن یا هنگام استفاده از کامپایلرهایی مانند Babel اینطور است). این کار هرگونه فرضیاتی را که درباره پشته فراخوانی (call stack) خطا (Error) وجود دارد، از بین می‌برد. ([بحث](https://github.com/airbnb/javascript/issues/794))

    ```javascript
    // بد
    function foo() {
      // ...
    }

    // بد
    const foo = function () {
      // ...
    };

    // خوب
    // نام لغوی (lexical name) متمایز از فراخوانی‌هایی که با متغیر ارجاع داده شده‌اند
    const short = function longUniqueMoreDescriptiveLexicalFoo() {
      // ...
    };
    ```

  <a name="functions--iife"></a><a name="7.2"></a>
  - [7.2](#functions--iife) عبارات توابعِ بلافاصله فراخوانی‌شده (IIFE) را داخل پرانتز قرار دهید. eslint: [`wrap-iife`](https://eslint.org/docs/rules/wrap-iife)

    > چرا؟ یک عبارت تابع بلافاصله فراخوانی‌شده یک واحد واحد است - قرار دادن هم خود آن و هم پرانتزهای فراخوانی‌اش داخل یک پرانتز، این موضوع را به وضوح نشان می‌دهد. توجه داشته باشید که در دنیایی که همه‌جا ماژول وجود دارد، تقریباً هرگز به IIFE نیاز ندارید.

    ```javascript
    // عبارت تابع بلافاصله فراخوانی‌شده (IIFE)
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks"></a><a name="7.3"></a>
  - [7.3](#functions--in-blocks) هرگز تابعی را در یک بلوک غیرتابعی (مثل `if`، `while` و غیره) اعلان نکنید. در عوض، تابع را به یک متغیر انتساب دهید. مرورگرها به شما اجازه می‌دهند این کار را انجام دهید، اما همگی آن را به شکل متفاوتی تفسیر می‌کنند که خبر بدی است. eslint: [`no-loop-func`](https://eslint.org/docs/rules/no-loop-func)

  <a name="functions--note-on-blocks"></a><a name="7.4"></a>
  - [7.4](#functions--note-on-blocks) **نکته:** ECMA-262 یک بلوک را به عنوان فهرستی از دستورات (statements) تعریف می‌کند. اعلان تابع (function declaration) یک دستور نیست.

    ```javascript
    // بد
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // خوب
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  <a name="functions--arguments-shadow"></a><a name="7.5"></a>
  - [7.5](#functions--arguments-shadow) هرگز یک پارامتر را `arguments` نام‌گذاری نکنید. این کار بر شئ `arguments` که به هر دامنه تابعی داده می‌شود، اولویت پیدا می‌کند.

    ```javascript
    // بد
    function foo(name, options, arguments) {
      // ...
    }

    // خوب
    function foo(name, options, args) {
      // ...
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  - [7.6](#es6-rest) هرگز از `arguments` استفاده نکنید، در عوض از سینتکس rest یعنی `...` استفاده کنید. eslint: [`prefer-rest-params`](https://eslint.org/docs/rules/prefer-rest-params)

    > چرا؟ `...` صریحاً مشخص می‌کند که کدام آرگومان‌ها را می‌خواهید استخراج کنید. علاوه بر این، آرگومان‌های rest یک آرایه واقعی هستند، نه فقط شبیه به آرایه (مانند `arguments`).

    ```javascript
    // بد
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // خوب
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  - [7.7](#es6-default-parameters) به جای تغییر آرگومان‌های تابع، از سینتکس پارامترهای پیش‌فرض استفاده کنید.

    ```javascript
    // خیلی بد
    function handleThings(opts) {
      // خیر! ما نباید آرگومان‌های تابع را تغییر دهیم.
      // دو برابر بد: اگر opts falsy باشد، روی یک شئ تنظیم می‌شود که شاید
      // همان چیزی باشد که می‌خواهید، اما می‌تواند باگ‌های ظریفی ایجاد کند.
      opts = opts || {};
      // ...
    }

    // هنوز هم بد
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // خوب
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects"></a><a name="7.8"></a>
  - [7.8](#functions--default-side-effects) از اثرات جانبی با پارامترهای پیش‌فرض اجتناب کنید.

    > چرا؟ استدلال در مورد آن‌ها گیج‌کننده است.

    ```javascript
    let b = 1;
    // بد
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last"></a><a name="7.9"></a>
  - [7.9](#functions--defaults-last) همیشه پارامترهای پیش‌فرض را در آخر قرار دهید. eslint: [`default-param-last`](https://eslint.org/docs/rules/default-param-last)

    ```javascript
    // بد
    function handleThings(opts = {}, name) {
      // ...
    }

    // خوب
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  - [7.10](#functions--constructor) برای ساخت یک تابع جدید، هرگز از سازنده Function استفاده نکنید. eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

    > چرا؟ ایجاد تابع به این روش، رشته‌ای را به شکلی مشابه `eval()` ارزیابی می‌کند که باعث ایجاد آسیب‌پذیری می‌شود.

    ```javascript
    // بد
    const add = new Function('a', 'b', 'return a + b');

    // هنوز هم بد
    const subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) فاصله‌گذاری در امضای یک تابع. eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    > چرا؟ یکپارچگی خوب است و شما نباید هنگام اضافه یا حذف کردن یک نام، مجبور به اضافه یا حذف کردن فاصله باشید.

    ```javascript
    // بد
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // خوب
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  - [7.12](#functions--mutate-params) هرگز پارامترها را دستخوش تغییر (mutate) نکنید. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign)

    > چرا؟ دستکاری اشیایی که به عنوان پارامتر پاس داده شده‌اند، می‌تواند باعث ایجاد اثرات جانبی ناخواسته متغیر در فراخواننده اصلی شود.

    ```javascript
    // بد
    function f1(obj) {
      obj.key = 1;
    }

    // خوب
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  - [7.13](#functions--reassign-params) هرگز پارامترها را مجدداً انتساب ندهید. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign)

    > چرا؟ انتساب مجدد پارامترها می‌تواند منجر به رفتارهای غیرمنتظره شود، به ویژه هنگام دسترسی به شئ `arguments`. همچنین می‌تواند مشکلاتی در بهینه‌سازی ایجاد کند، به خصوص در V8.

    ```javascript
    // بد
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // خوب
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

  <a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) برای فراخوانی توابع با تعداد آرگومان متغیر (variadic functions)، استفاده از سینتکس spread یعنی `...` را ترجیح دهید. eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

    > چرا؟ تمیزتر است، نیازی به ارائه یک context ندارید، و نمی‌توانید به راحتی `new` را با `apply` ترکیب کنید.

    ```javascript
    // بد
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // خوب
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // بد
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // خوب
    new Date(...[2016, 8, 5]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  - [7.15](#functions--signature-invocation-indentation) توابعی که امضا (signature) یا فراخوانی (invocation) چند خطی دارند، باید دقیقاً مانند هر فهرست چند خطی دیگری در این راهنما تورفتگی (indent) داشته باشند: با قرار گرفتن هر آیتم در یک خط مجزا، همراه با یک ویرگول انتهایی (trailing comma) در آخرین آیتم. eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)

    ```javascript
    // بد
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    // خوب
    function foo(
      bar,
      baz,
      quux,
    ) {
      // ...
    }

    // بد
    console.log(foo,
      bar,
      baz);

    // خوب
    console.log(
      foo,
      bar,
      baz,
    );
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## توابع پیکانی

  <a name="arrows--use-them"></a><a name="8.1"></a>
  - [8.1](#arrows--use-them) زمانی که مجبور به استفاده از یک تابع ناشناس هستید (مانند زمانی که یک کال‌بک درون‌خطی پاس می‌دهید)، از نمادنگاری تابع پیکانی استفاده کنید. eslint: [`prefer-arrow-callback`](https://eslint.org/docs/rules/prefer-arrow-callback), [`arrow-spacing`](https://eslint.org/docs/rules/arrow-spacing)

    > چرا؟ این کار نسخه‌ای از تابع را ایجاد می‌کند که در بافت (context) `this` اجرا می‌شود، که معمولاً همان چیزی است که می‌خواهید، و سینتکسی مختصرتر است.

    > چرا نه؟ اگر تابع نسبتاً پیچیده‌ای دارید، ممکن است بخواهید آن منطق را به یک عبارت تابعِ نام‌گذاری‌شده و جداگانه منتقل کنید.

    ```javascript
    // بد
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // خوب
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--implicit-return"></a><a name="8.2"></a>
  - [8.2](#arrows--implicit-return) اگر بدنهٔ تابع از یک دستور واحد تشکیل شده باشد که یک [عبارت](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) بدون اثرات جانبی را برمی‌گرداند، آکولادها را حذف کرده و از بازگشت ضمنی (implicit return) استفاده کنید. در غیر این صورت، آکولادها را نگه دارید و از دستور `return` استفاده کنید. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens), [`arrow-body-style`](https://eslint.org/docs/rules/arrow-body-style)

    > چرا؟ راه را هموار کردن (Syntactic sugar). هنگامی که چند تابع به هم زنجیر می‌شوند، خوانایی خوبی دارد.

    ```javascript
    // بد
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // خوب
    [1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

    // خوب
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });

    // خوب
    [1, 2, 3].map((number, index) => ({
      [index]: number,
    }));

    // بدون بازگشت ضمنی در صورت وجود اثرات جانبی
    function foo(callback) {
      const val = callback();
      if (val === true) {
        // اگر کال‌بک true برمی‌گرداند کاری انجام دهید
      }
    }

    let bool = false;

    // بد
    foo(() => bool = true);

    // خوب
    foo(() => {
      bool = true;
    });
    ```

  <a name="arrows--paren-wrap"></a><a name="8.3"></a>
  - [8.3](#arrows--paren-wrap) در صورتی که عبارت در چند خط پهن می‌شود، برای خوانایی بهتر آن را داخل پرانتز قرار دهید.

    > چرا؟ به وضوح نشان می‌دهد که تابع از کجا شروع و به کجا ختم می‌شود.

    ```javascript
    // بد
    ['get', 'post', 'put'].map((httpMethod) => Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    );

    // خوب
    ['get', 'post', 'put'].map((httpMethod) => (
      Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    ));
    ```

  <a name="arrows--one-arg-parens"></a><a name="8.4"></a>
  - [8.4](#arrows--one-arg-parens) همیشه برای شفافیت و یکپارچگی، پرانتزها را دور آرگومان‌ها قرار دهید. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens)

    > چرا؟ تفاوت ها (diff) هنگام اضافه یا حذف آرگومان‌ها را به حداقل می‌رساند.

    ```javascript
    // بد
    [1, 2, 3].map(x => x * x);

    // خوب
    [1, 2, 3].map((x) => x * x);

    // بد
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // خوب
    [1, 2, 3].map((number) => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // بد
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });

    // خوب
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--confusing"></a><a name="8.5"></a>
  - [8.5](#arrows--confusing) از اشتباه گرفتن سینتکس تابع پیکانی (`=>`) با عملگرهای مقایسه‌ای (`<=`، `>=`) اجتناب کنید. eslint: [`no-confusing-arrow`](https://eslint.org/docs/rules/no-confusing-arrow)

    ```javascript
    // بد
    const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

    // بد
    const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

    // خوب
    const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

    // خوب
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height <= 256 ? largeSize : smallSize;
    };
    ```

  <a name="whitespace--implicit-arrow-linebreak"></a>
  - [8.6](#whitespace--implicit-arrow-linebreak) مکان بدنهٔ توابع پیکانی که دارای بازگشت ضمنی هستند را یکسان نگه دارید. eslint: [`implicit-arrow-linebreak`](https://eslint.org/docs/rules/implicit-arrow-linebreak)

    ```javascript
    // بد
    (foo) =>
      bar;

    (foo) =>
      (bar);

    // خوب
    (foo) => bar;
    (foo) => (bar);
    (foo) => (
       bar
    )
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## کلاس ها و سازنده ها

  <a name="constructors--use-class"></a><a name="9.1"></a>
  - [9.1](#constructors--use-class) همیشه از `class` استفاده کنید. از دستکاری مستقیم `prototype` خودداری کنید.

    > چرا؟ سینتکس `class` مختصرتر است و استدلال در مورد آن آسان‌تر است.

    ```javascript
    // بد
    function Queue(contents = []) {
      this.queue = [...contents];
    }
    Queue.prototype.pop = function () {
      const value = this.queue[0];
      this.queue.splice(0, 1);
      return value;
    };

    // خوب
    class Queue {
      constructor(contents = []) {
        this.queue = [...contents];
      }
      pop() {
        const value = this.queue[0];
        this.queue.splice(0, 1);
        return value;
      }
    }
    ```

  <a name="constructors--extends"></a><a name="9.2"></a>
  - [9.2](#constructors--extends) برای وراثت از `extends` استفاده کنید.

    > چرا؟ این یک روش توکار (built-in) برای به ارث بردن قابلیت‌های prototype است بدون اینکه `instanceof` را خراب کند.

    ```javascript
    // بد
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function () {
      return this.queue[0];
    };

    // خوب
    class PeekableQueue extends Queue {
      peek() {
        return this.queue[0];
      }
    }
    ```

  <a name="constructors--chaining"></a><a name="9.3"></a>
  - [9.3](#constructors--chaining) متدها می‌توانند `this` را برگردانند تا به زنجیره‌سازی متدها (method chaining) کمک کنند.

    ```javascript
    // بد
    Jedi.prototype.jump = function () {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function (height) {
      this.height = height;
    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // خوب
    class Jedi {
      jump() {
        this.jumping = true;
        return this;
      }

      setHeight(height) {
        this.height = height;
        return this;
      }
    }

    const luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```

  <a name="constructors--tostring"></a><a name="9.4"></a>
  - [9.4](#constructors--tostring) نوشتن یک متد سفارشی `toString()` اشکالی ندارد، فقط مطمئن شوید که با موفقیت کار می‌کند و هیچ اثر جانبی ایجاد نمی‌کند.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        this.name = options.name || 'no name';
      }

      getName() {
        return this.name;
      }

      toString() {
        return `Jedi - ${this.getName()}`;
      }
    }
    ```

  <a name="constructors--no-useless"></a><a name="9.5"></a>
  - [9.5](#constructors--no-useless) کلاس‌ها در صورت عدم مشخص شدن، یک سازنده (constructor) پیش‌فرض دارند. یک تابع سازنده خالی یا سازنده‌ای که فقط کارها را به کلاس والد واگذار می‌کند، غیرضروری است. eslint: [`no-useless-constructor`](https://eslint.org/docs/rules/no-useless-constructor)

    ```javascript
    // بد
    class Jedi {
      constructor() {}

      getName() {
        return this.name;
      }
    }

    // بد
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
      }
    }

    // خوب
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
        this.name = 'Rey';
      }
    }
    ```

  <a name="classes--no-duplicate-members"></a>
  - [9.6](#classes--no-duplicate-members) از اعضای تکراری در کلاس خودداری کنید. eslint: [`no-dupe-class-members`](https://eslint.org/docs/rules/no-dupe-class-members)

    > چرا؟ اعلان اعضای تکراری کلاس، بی سر و صدا، آخرین مورد را ترجیح می‌دهد - داشتن موارد تکراری تقریباً قطعا یک باگ است.

    ```javascript
    // بد
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // خوب
    class Foo {
      bar() { return 1; }
    }

    // خوب
    class Foo {
      bar() { return 2; }
    }
    ```

  <a name="classes--methods-use-this"></a>
  - [9.7](#classes--methods-use-this) متدهای کلاس باید از `this` استفاده کنند یا به یک متد استاتیک (static) تبدیل شوند، مگر اینکه یک کتابخانه یا فریم‌ورک خارجی، استفاده از متدهای خاصِ غیراستاتیک را ایجاب کند. بودنِ یک متدِ نمونه (instance method) باید نشان‌دهنده این باشد که رفتار آن بر اساس ویژگی‌های گیرنده (receiver) متفاوت است. eslint: [`class-methods-use-this`](https://eslint.org/docs/rules/class-methods-use-this)

    ```javascript
    // بد
    class Foo {
      bar() {
        console.log('bar');
      }
    }

    // خوب - از this استفاده شده است
    class Foo {
      bar() {
        console.log(this.bar);
      }
    }

    // خوب - constructor مستثنی است
    class Foo {
      constructor() {
        // ...
      }
    }

    // خوب - از متدهای استاتیک انتظار نمی‌رود که از this استفاده کنند
    class Foo {
      static bar() {
        console.log('bar');
      }
    }
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## ماژول ها (modules)

  <a name="modules--use-them"></a><a name="10.1"></a>
  - [10.1](#modules--use-them) همیشه به جای سیستم‌های ماژول غیراستاندارد، از ماژول‌ها (`import`/`export`) استفاده کنید. شما همیشه می‌توانید کد را به سیستم ماژول دلخواه خود transpile (تبدیل) کنید.

    > چرا؟ ماژول‌ها آینده هستند، بیایید از همین الان از آینده استفاده کنیم.

    ```javascript
    // بد
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    module.exports = AirbnbStyleGuide.es6;

    // قابل قبول
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default AirbnbStyleGuide.es6;

    // بهترین
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-wildcard"></a><a name="10.2"></a>
  - [10.2](#modules--no-wildcard) از واردات شَخلِه (wildcard imports) استفاده نکنید.

    > چرا؟ این کار تضمین می‌کند که شما یک خروجی پیش‌فرض (default export) واحد داشته باشید.

    ```javascript
    // بد
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // خوب
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  <a name="modules--no-export-from-import"></a><a name="10.3"></a>
  - [10.3](#modules--no-export-from-import) و مستقیماً از یک import، export نگیرید.

    > چرا؟ هرچند نوشتن آن در یک خط مختصر است، اما داشتن یک راه مشخص برای وارد کردن و یک راه مشخص برای صادر کردن، باعث یکپارچگی می‌شود.

    ```javascript
    // بد
    // filename es6.js
    export { es6 as default } from './AirbnbStyleGuide';

    // خوب
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-duplicate-imports"></a>
  - [10.4](#modules--no-duplicate-imports) فقط از یک مسیر را در یک مکان وارد کنید.
  eslint: [`no-duplicate-imports`](https://eslint.org/docs/rules/no-duplicate-imports)
    > چرا؟ داشتن چندین خط که از یک مسیر یکسان وارد می‌کنند، می‌تواند حفظ و نگهداری کد را سخت‌تر کند.

    ```javascript
    // بد
    import foo from 'foo';
    // … some other imports … //
    import { named1, named2 } from 'foo';

    // خوب
    import foo, { named1, named2 } from 'foo';

    // خوب
    import foo, {
      named1,
      named2,
    } from 'foo';
    ```

  <a name="modules--no-mutable-exports"></a>
  - [10.5](#modules--no-mutable-exports) اتصالات (bindings) قابل تغییر (mutable) را صادر نکنید.
  eslint: [`import/no-mutable-exports`](https://github.com/import-js/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)
    > چرا؟ به طور کلی باید از تغییر (mutation) اجتناب کرد، اما به ویژه هنگام صادر کردن اتصالات قابل تغییر. در حالی که این تکنیک ممکن است برای برخی موارد خاص نیاز باشد، به طور کلی فقط باید ارجاعات ثابت (const) صادر شوند.

    ```javascript
    // بد
    let foo = 3;
    export { foo };

    // خوب
    const foo = 3;
    export { foo };
    ```

  <a name="modules--prefer-default-export"></a>
  - [10.6](#modules--prefer-default-export) در ماژول‌هایی با تنها یک خروجی، خروجی پیش‌فرض (default export) را به خروجی نام‌گذاری‌شده (named export) ترجیح دهید.
  eslint: [`import/prefer-default-export`](https://github.com/import-js/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)
    > چرا؟ برای تشویق فایل‌های بیشتری که فقط یک چیز را صادر می‌کنند، که برای خوانایی و قابلیت نگهداری بهتر است.

    ```javascript
    // بد
    export function foo() {}

    // خوب
    export default function foo() {}
    ```

  <a name="modules--imports-first"></a>
  - [10.7](#modules--imports-first) تمام `import`ها را بالاتر از دستورات غیرِ وارداتی قرار دهید.
  eslint: [`import/first`](https://github.com/import-js/eslint-plugin-import/blob/master/docs/rules/first.md)
    > چرا؟ از آنجایی که `import`ها بالا آورده می‌شوند (hoisted)، نگه داشتن همه آن‌ها در بالا از رفتارهای غیرمنتظره جلوگیری می‌کند.

    ```javascript
    // بد
    import foo from 'foo';
    foo.init();

    import bar from 'bar';

    // خوب
    import foo from 'foo';
    import bar from 'bar';

    foo.init();
    ```

  <a name="modules--multiline-imports-over-newlines"></a>
  - [10.8](#modules--multiline-imports-over-newlines) واردات چندخطی باید دقیقاً مانند لیترال‌های چندخطی آرایه و شئ، فاصله گذاری (indent) داشته باشند.
  eslint: [`object-curly-newline`](https://eslint.org/docs/rules/object-curly-newline)

    > چرا؟ آکولادها از همان قوانین فاصله گذاری پیروی می‌کنند که هر بلوک آکولاد دیگری در این راهنما دارد، و ویرگول‌های انتهایی (trailing commas) نیز همینطور.

    ```javascript
    // بد
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

    // خوب
    import {
      longNameA,
      longNameB,
      longNameC,
      longNameD,
      longNameE,
    } from 'path';
    ```

  <a name="modules--no-webpack-loader-syntax"></a>
  - [10.9](#modules--no-webpack-loader-syntax) استفاده از سینتکس لودرهای Webpack در دستورات واردات ماژول ممنوع است.
  eslint: [`import/no-webpack-loader-syntax`](https://github.com/import-js/eslint-plugin-import/blob/master/docs/rules/no-webpack-loader-syntax.md)
    > چرا؟ از آنجایی که استفاده از سینتکس Webpack در واردات، کد را به یک باندلر ماژول وابسته می‌کند. استفاده از سینتکس لودر در `webpack.config.js` ترجیح داده می‌شود.

    ```javascript
    // بد
    import fooSass from 'css!sass!foo.scss';
    import barCss from 'style!css!bar.css';

    // خوب
    import fooSass from 'foo.scss';
    import barCss from 'bar.css';
    ```

  <a name="modules--import-extensions"></a>
  - [10.10](#modules--import-extensions) پسوندهای نام فایل جاوااسکریپت را لحاظ نکنید.
  eslint: [`import/extensions`](https://github.com/import-js/eslint-plugin-import/blob/master/docs/rules/extensions.md)
    > چرا؟ لحاظ کردن پسوندها، بازنویسی کد (refactoring) را محدود می‌کند و جزئیات پیاده‌سازی ماژولی که در حال وارد کردن آن هستید را به صورت نامناسبی در هر مصرف‌کننده، هاردکد (سخت‌کد) می‌کند.

    ```javascript
    // بد
    import foo from './foo.js';
    import bar from './bar.jsx';
    import baz from './baz/index.jsx';

    // خوب
    import foo from './foo';
    import bar from './bar';
    import baz from './baz';
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## تکرارکننده ها و مولد ها (Iterators and Generators)

  <a name="iterators--nope"></a><a name="11.1"></a>
  - [11.1](#iterators--nope) از تکرارکننده‌ها (iterators) استفاده نکنید. به جای حلقه‌هایی مانند `for-in` یا `for-of`، توابع مرتبه بالای جاوااسکریپت را ترجیح دهید. eslint: [`no-iterator`](https://eslint.org/docs/rules/no-iterator) [`no-restricted-syntax`](https://eslint.org/docs/rules/no-restricted-syntax)

    > چرا؟ این کار قانون تغییرناپذیری (immutable) ما را اعمال می‌کند. کار با توابع خالصی که مقادیری را برمی‌گردانند، در مقایسه با اثرات جانبی، استدلال در موردشان آسان‌تر است.

    > برای پیمایش آرایه‌ها از `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... استفاده کنید و برای تولید آرایه‌هایی که بتوانید اشیاء را پیمایش کنید، از `Object.keys()` / `Object.values()` / `Object.entries()` استفاده کنید.

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // بد
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;

    // خوب
    let sum = 0;
    numbers.forEach((num) => {
      sum += num;
    });
    sum === 15;

    // بهترین (از نیروی تابعی استفاده کنید)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;

    // بد
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }

    // خوب
    const increasedByOne = [];
    numbers.forEach((num) => {
      increasedByOne.push(num + 1);
    });

    // بهترین (نگه داشتن حالت تابعی)
    const increasedByOne = numbers.map((num) => num + 1);
    ```

  <a name="generators--nope"></a><a name="11.2"></a>
  - [11.2](#generators--nope) فعلاً از مولدها (Generators) استفاده نکنید.

    > چرا؟ آن‌ها به خوبی به ES5 ترنسپایل نمی‌شوند.

  <a name="generators--spacing"></a>
  - [11.3](#generators--spacing) اگر مجبور به استفاده از مولدها هستید، یا اگر [توصیه ما](#generators--nope) را نادیده می‌گیرید، مطمئن شوید که امضای تابع آن‌ها به درستی فاصله‌گذاری شده است. eslint: [`generator-star-spacing`](https://eslint.org/docs/rules/generator-star-spacing)

    > چرا؟ `function` و `*` بخشی از یک کلمه کلیدی مفهومی یکسان هستند - `*` یک اصلاح‌کننده برای `function` نیست، `function*` یک ساختار منحصر‌به‌فرد است که با `function` متفاوت است.

    ```javascript
    // بد
    function * foo() {
      // ...
    }

    // بد
    const bar = function * () {
      // ...
    };

    // بد
    const baz = function *() {
      // ...
    };

    // بد
    const quux = function*() {
      // ...
    };

    // بد
    function*foo() {
      // ...
    }

    // بد
    function *foo() {
      // ...
    }

    // خیلی بد
    function
    *
    foo() {
      // ...
    }

    // خیلی بد
    const wat = function
    *
    () {
      // ...
    };

    // خوب
    function* foo() {
      // ...
    }

    // خوب
    const foo = function* () {
      // ...
    };
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## ویژگی ها (properties)

  <a name="properties--dot"></a><a name="12.1"></a>
  - [12.1](#properties--dot) هنگام دسترسی به ویژگی‌ها از نمادگذاری نقطه‌ای (dot notation) استفاده کنید. eslint: [`dot-notation`](https://eslint.org/docs/rules/dot-notation)

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    // بد
    const isJedi = luke['jedi'];

    // خوب
    const isJedi = luke.jedi;
    ```

  <a name="properties--bracket"></a><a name="12.2"></a>
  - [12.2](#properties--bracket) هنگام دسترسی به ویژگی‌ها با استفاده از یک متغیر، از نمادگذاری براکتی `[]` استفاده کنید.

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    const isJedi = getProp('jedi');
    ```

  <a name="es2016-properties--exponentiation-operator"></a>
  - [12.3](#es2016-properties--exponentiation-operator) هنگام محاسبه توان، از عملگر توان `**` استفاده کنید. eslint: [`prefer-exponentiation-operator`](https://eslint.org/docs/rules/prefer-exponentiation-operator).

    ```javascript
    // بد
    const binary = Math.pow(2, 10);

    // خوب
    const binary = 2 ** 10;
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## متغیر ها

  <a name="variables--const"></a><a name="13.1"></a>
  - [13.1](#variables--const) همیشه برای اعلان متغیرها از `const` یا `let` استفاده کنید. عدم انجام این کار منجر به ایجاد متغیرهای سراسری (global) می‌شود. ما می‌خواهیم از آلوده کردن فضای نام سراسری جلوگیری کنیم. کاپیتان پلنت به ما در این باره هشدار داده بود. eslint: [`no-undef`](https://eslint.org/docs/rules/no-undef) [`prefer-const`](https://eslint.org/docs/rules/prefer-const)

    ```javascript
    // بد
    superPower = new SuperPower();

    // خوب
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const"></a><a name="13.2"></a>
  - [13.2](#variables--one-const) برای هر متغیر یا انتساب، از یک اعلان `const` یا `let` مجزا استفاده کنید. eslint: [`one-var`](https://eslint.org/docs/rules/one-var)

    > چرا؟ این روش اضافه کردن اعلان‌های متغیر جدید را آسان‌تر می‌کند، و دیگر نیازی نیست نگران جایگزینی `;` با `,` یا ایجاد تفاوت ها (diff) فقط نقطه‌گذاری باشید. همچنین می‌توانید با دیباگر (debugger) هر اعلان را مرحله به مرحله پیش بروید، به جای اینکه همه را به یکباره رد شوید.

    ```javascript
    // بد
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // بد
    // (با بالا مقایسه کنید و سعی کنید اشتباه را پیدا کنید)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // خوب
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  <a name="variables--const-let-group"></a><a name="13.3"></a>
  - [13.3](#variables--const-let-group) ابتدا همهٔ `const`های خود و سپس همهٔ `let`های خود را گروه‌بندی کنید.

    > چرا؟ این کار زمانی مفید است که بعداً ممکن است نیاز داشته باشید متغیری را بر اساس یکی از متغیرهای از پیش اختصاص داده شده، مقداردهی کنید.

    ```javascript
    // بد
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // بد
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // خوب
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  <a name="variables--define-where-used"></a><a name="13.4"></a>
  - [13.4](#variables--define-where-used) متغیرها را جایی مقداردهی کنید که به آن‌ها نیاز دارید، اما در یک مکان منطقی قرارشان دهید.

    > چرا؟ `let` و `const` دامنه بلوکی دارند، نه دامنه تابعی.

    ```javascript
    // بد - فراخوانی تابع غیرضروری
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // خوب
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
    ```

  <a name="variables--no-chain-assignment"></a><a name="13.5"></a>
  - [13.5](#variables--no-chain-assignment) انتساب متغیرها را زنجیره‌ای نکنید. eslint: [`no-multi-assign`](https://eslint.org/docs/rules/no-multi-assign)

    > چرا؟ انتساب زنجیره‌ای متغیرها، متغیرهای سراسری ضمنی ایجاد می‌کند.

    ```javascript
    // بد
    (function example() {
      // جاوااسکریپت این را به این شکل تفسیر می‌کند
      // let a = ( b = ( c = 1 ) );
      // کلمه کلیدی let فقط روی متغیر a اعمال می‌شود؛ متغیرهای b و c به
      // متغیرهای سراسری تبدیل می‌شوند.
      let a = b = c = 1;
    }());

    console.log(a); // خطای ReferenceError پرتاب می‌کند
    console.log(b); // 1
    console.log(c); // 1

    // خوب
    (function example() {
      let a = 1;
      let b = a;
      let c = a;
    }());

    console.log(a); // خطای ReferenceError پرتاب می‌کند
    console.log(b); // خطای ReferenceError پرتاب می‌کند
    console.log(c); // خطای ReferenceError پرتاب می‌کند

    // همین امر برای `const` نیز صدق می‌کند
    ```

  <a name="variables--unary-increment-decrement"></a><a name="13.6"></a>
  - [13.6](#variables--unary-increment-decrement) از افزایش و کاهش یگانه (`++`, `--`) اجتناب کنید. eslint [`no-plusplus`](https://eslint.org/docs/rules/no-plusplus)

    > چرا؟ بر اساس مستندات eslint، دستورات افزایش و کاهش یگانه مستعد درج خودکار سمی‌کالن (automatic semicolon insertion) هستند و می‌توانند باعث خطاهای خاموش در افزایش یا کاهش مقادیر درون یک برنامه شوند. همچنین تغییر مقادیر با دستوراتی مانند `num += 1` به جای `num++` یا `num ++` گویاتر است. ممنوع کردن دستورات افزایش و کاهش یگانه همچنین شما را از افزایش/کاهش پیشین (pre-incrementing/pre-decrementing) مقادیر به صورت ناخواسته باز می‌دارد که می‌تواند باعث رفتارهای غیرمنتظره در برنامه‌های شما شود.

    ```javascript
    // بد

    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;

    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }

    // خوب

    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;

    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

  <a name="variables--linebreak"></a>
  - [13.7](#variables--linebreak) از خط‌شکن (خط جدید) قبل یا بعد از `=` در یک انتساب اجتناب کنید. اگر انتساب شما [`max-len`](https://eslint.org/docs/rules/max-len) را نقض می‌کند، مقدار را داخل پرانتز قرار دهید. eslint [`operator-linebreak`](https://eslint.org/docs/rules/operator-linebreak).

    > چرا؟ خط‌شکن‌های اطراف `=` می‌توانند مقدار یک انتساب را مبهم کنند.

    ```javascript
    // بد
    const foo =
      superLongLongLongLongLongLongLongLongFunctionName();

    // بد
    const foo
      = 'superLongLongLongLongLongLongLongLongString';

    // خوب
    const foo = (
      superLongLongLongLongLongLongLongLongFunctionName()
    );

    // خوب
    const foo = 'superLongLongLongLongLongLongLongLongString';
    ```

  <a name="variables--no-unused-vars"></a>
  - [13.8](#variables--no-unused-vars) متغیرهای استفاده‌نشده را ممنوع کنید. eslint: [`no-unused-vars`](https://eslint.org/docs/rules/no-unused-vars)

    > چرا؟ متغیرهایی که اعلان می‌شوند و هیچ‌جایی در کد استفاده نمی‌شوند، احتمالاً به دلیل بازنویسی ناقص (refactoring) یک خطا هستند. چنین متغیرهایی فضا اشغال می‌کنند و می‌توانند باعث سردرگمی خوانندگان شوند.

    ```javascript
    // بد

    const some_unused_var = 42;

    // متغیرهای فقط-نوشتنی (write-only) به عنوان استفاده‌شده در نظر گرفته نمی‌شوند.
    let y = 10;
    y = 5;

    // خواندن برای اصلاح خودش، به عنوان استفاده‌شده در نظر گرفته نمی‌شود.
    let z = 0;
    z = z + 1;

    // آرگومان‌های استفاده نشده تابع.
    function getX(x, y) {
        return x;
    }

    // خوب

    function getXPlusY(x, y) {
      return x + y;
    }

    const x = 1;
    const y = a + 2;

    alert(getXPlusY(x, y));

    // 'type' حتی اگر استفاده نشود نادیده گرفته می‌شود چون یک ویژگی خواهری (sibling) از نوع rest دارد.
    // این شکلی از استخراج یک شئ است که کلیدهای مشخص شده را حذف می‌کند.
    const { type, ...coords } = data;
    // 'coords' اکنون شئ 'data' بدون ویژگی 'type' آن است.
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## بالا آوردن (Hoisting)

  <a name="hoisting--about"></a><a name="14.1"></a>
  - [14.1](#hoisting--about) اعلان‌های `var` به بالاترین حد دامنه تابعی احاطه‌کنندهٔ خود بالا آورده می‌شوند (hoisted)، اما انتساب آن‌ها بالا آورده نمی‌شود. اعلان‌های `const` و `let` دارای یک مفهوم جدید به نام [منطقه مرده زمانی (Temporal Dead Zones - TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz) هستند. مهم است بدانید چرا [`typeof` دیگر امن نیست](https://web.archive.org/web/20200121061528/http://es-discourse.com/t/why-typeof-is-no-longer-safe/15).

    ```javascript
    // می‌دانیم که این کار نمی‌کند (با فرض اینکه
    // متغیر سراسری notDefined وجود ندارد)
    function example() {
      console.log(notDefined); // => یک خطای ReferenceError پرتاب می‌کند
    }

    // ایجاد یک اعلان متغیر پس از اینکه
    // به متغیر ارجاع داده‌اید، به دلیل بالا آوردن
    // متغیر کار خواهد کرد. نکته: مقدار
    // انتسابیِ `true` بالا آورده نمی‌شود.
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // مفسر اعلان متغیر را به بالای دامنه
    // بالا می‌آورد، به این معنی که مثال ما
    // می‌تواند به این شکل بازنویسی شود:
    function example() {
      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }

    // استفاده از const و let
    function example() {
      console.log(declaredButNotAssigned); // => یک خطای ReferenceError پرتاب می‌کند
      console.log(typeof declaredButNotAssigned); // => یک خطای ReferenceError پرتاب می‌کند
      const declaredButNotAssigned = true;
    }
    ```

  <a name="hoisting--anon-expressions"></a><a name="14.2"></a>
  - [14.2](#hoisting--anon-expressions) عبارات توابع ناشناس (Anonymous function expressions)، نام متغیر خود را بالا می‌آورند، اما انتساب تابع بالا آورده نمی‌شود.

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError: anonymous تابع نیست

      var anonymous = function () {
        console.log('anonymous function expression');
      };
    }
    ```

  <a name="hoisting--named-expresions"></a><a name="hoisting--named-expressions"></a><a name="14.3"></a>
  - [14.3](#hoisting--named-expressions) عبارات توابع نام‌گذاری‌شده (Named function expressions)، نام متغیر را بالا می‌آورند، نه نام تابع یا بدنه تابع را.

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError: named تابع نیست

      superPower(); // => ReferenceError: superPower تعریف نشده است

      var named = function superPower() {
        console.log('Flying');
      };
    }

    // همین امر زمانی صادق است که نام تابع
    // با نام متغیر یکسان باشد.
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError: named تابع نیست

      var named = function named() {
        console.log('named');
      };
    }
    ```

  <a name="hoisting--declarations"></a><a name="14.4"></a>
  - [14.4](#hoisting--declarations) اعلان توابع (Function declarations)، نام و بدنه تابع را بالا می‌آورند.

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  <a name="no-use-before-define"></a>
  - [14.5](#no-use-before-define) متغیرها، کلاس‌ها و توابع باید قبل از استفاده شدن تعریف شوند. eslint: [`no-use-before-define`](https://eslint.org/docs/latest/rules/no-use-before-define)

    > چرا؟ زمانی که متغیرها، کلاس‌ها یا توابع پس از استفاده شدن اعلان می‌شوند، می‌تواند به خوانایی آسیب برساند، زیرا خواننده نمی‌داند آن چیزی که به آن ارجاع داده شده چیست. برای یک خواننده بسیار واضح‌تر است که ابتدا با منبع یک چیز (چه وارد شده از ماژول دیگر، چه تعریف شده در فایل) مواجه شود و سپس با استفاده از آن چیز روبرو شود.

    ```javascript
    // بد

    // متغیر a قبل از تعریف شدنش استفاده می‌شود.
    console.log(a);
    // این undefined خواهد بود، زیرا در حالی که اعلان بالا آورده می‌شود، مقداردهی اولیه (initialization) بالا آورده نمی‌شود
    var a = 10;

    // تابع fun قبل از تعریف شدن فراخوانی می‌شود.
    fun();
    function fun() {}

    // کلاس A قبل از تعریف شدن استفاده می‌شود.
    new A(); // ReferenceError: Cannot access 'A' before initialization
    class A {
    }

    // `let` و `const` بالا آورده می‌شوند، اما مقداردهی اولیه پیش‌فرض ندارند.
    // متغیرهای 'a' و 'b' در یک منطقه مرده زمانی (Temporal Dead Zone) هستند
    // که جاوااسکریپت می‌داند آن‌ها وجود دارند (اعلان بالا آورده شده است)
    // اما قابل دسترسی نیستند (چون هنوز مقداردهی اولیه نشده‌اند).

    console.log(a); // ReferenceError: Cannot access 'a' before initialization
    console.log(b); // ReferenceError: Cannot access 'b' before initialization
    let a = 10;
    const b = 5;


    // خوب

    var a = 10;
    console.log(a); // 10

    function fun() {}
    fun();

    class A {
    }
    new A();

    let a = 10;
    const b = 5;
    console.log(a); // 10
    console.log(b); // 5
    ```

  - برای اطلاعات بیشتر به [محدوده‌سازی و بالا آوردن در جاوااسکریپت (JavaScript Scoping & Hoisting)](https://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting/) اثر [بن چری (Ben Cherry)](https://www.adequatelygood.com/) مراجعه کنید.

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Comparison Operators & Equality

  <a name="comparison--eqeqeq"></a><a name="15.1"></a>
  - [15.1](#comparison--eqeqeq) Use `===` and `!==` over `==` and `!=`. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq)

  <a name="comparison--if"></a><a name="15.2"></a>
  - [15.2](#comparison--if) Conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

    - **Objects** evaluate to **true**
    - **Undefined** evaluates to **false**
    - **Null** evaluates to **false**
    - **Booleans** evaluate to **the value of the boolean**
    - **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
    - **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

    ```javascript
    if ([0] && []) {
      // true
      // an array (even an empty one) is an object, objects will evaluate to true
    }
    ```

  <a name="comparison--shortcuts"></a><a name="15.3"></a>
  - [15.3](#comparison--shortcuts) Use shortcuts for booleans, but explicit comparisons for strings and numbers.

    ```javascript
    // bad
    if (isValid === true) {
      // ...
    }

    // good
    if (isValid) {
      // ...
    }

    // bad
    if (name) {
      // ...
    }

    // good
    if (name !== '') {
      // ...
    }

    // bad
    if (collection.length) {
      // ...
    }

    // good
    if (collection.length > 0) {
      // ...
    }
    ```

  <a name="comparison--moreinfo"></a><a name="15.4"></a>
  - [15.4](#comparison--moreinfo) For more information see [Truth, Equality, and JavaScript](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.

  <a name="comparison--switch-blocks"></a><a name="15.5"></a>
  - [15.5](#comparison--switch-blocks) Use braces to create blocks in `case` and `default` clauses that contain lexical declarations (e.g. `let`, `const`, `function`, and `class`). eslint: [`no-case-declarations`](https://eslint.org/docs/rules/no-case-declarations)

    > Why? Lexical declarations are visible in the entire `switch` block but only get initialized when assigned, which only happens when its `case` is reached. This causes problems when multiple `case` clauses attempt to define the same thing.

    ```javascript
    // bad
    switch (foo) {
      case 1:
        let x = 1;
        break;
      case 2:
        const y = 2;
        break;
      case 3:
        function f() {
          // ...
        }
        break;
      default:
        class C {}
    }

    // good
    switch (foo) {
      case 1: {
        let x = 1;
        break;
      }
      case 2: {
        const y = 2;
        break;
      }
      case 3: {
        function f() {
          // ...
        }
        break;
      }
      case 4:
        bar();
        break;
      default: {
        class C {}
      }
    }
    ```

  <a name="comparison--nested-ternaries"></a><a name="15.6"></a>
  - [15.6](#comparison--nested-ternaries) Ternaries should not be nested and generally be single line expressions. eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary)

    ```javascript
    // bad
    const foo = maybe1 > maybe2
      ? 'bar'
      : value1 > value2 ? 'baz' : null;

    // split into 2 separated ternary expressions
    const maybeNull = value1 > value2 ? 'baz' : null;

    // better
    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // best
    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary"></a><a name="15.7"></a>
  - [15.7](#comparison--unneeded-ternary) Avoid unneeded ternary statements. eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary)

    ```javascript
    // bad
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;
    const quux = a != null ? a : b;

    // good
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    const quux = a ?? b;
    ```

  <a name="comparison--no-mixed-operators"></a>
  - [15.8](#comparison--no-mixed-operators) When mixing operators, enclose them in parentheses. The only exception is the standard arithmetic operators: `+`, `-`, and `**` since their precedence is broadly understood. We recommend enclosing `/` and `*` in parentheses because their precedence can be ambiguous when they are mixed.
  eslint: [`no-mixed-operators`](https://eslint.org/docs/rules/no-mixed-operators)

    > Why? This improves readability and clarifies the developer’s intention.

    ```javascript
    // bad
    const foo = a && b < 0 || c > 0 || d + 1 === 0;

    // bad
    const bar = a ** b - 5 % d;

    // bad
    // one may be confused into thinking (a || b) && c
    if (a || b && c) {
      return d;
    }

    // bad
    const bar = a + b / c * d;

    // good
    const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

    // good
    const bar = a ** b - (5 % d);

    // good
    if (a || (b && c)) {
      return d;
    }

    // good
    const bar = a + (b / c) * d;
    ```

  <a name="nullish-coalescing-operator"></a>
  - [15.9](#nullish-coalescing-operator) The nullish coalescing operator (`??`) is a logical operator that returns its right-hand side operand when its left-hand side operand is `null` or `undefined`. Otherwise, it returns the left-hand side operand.

    > Why? It provides precision by distinguishing null/undefined from other falsy values, enhancing code clarity and predictability.

    ```javascript
    // bad
    const value = 0 ?? 'default';
    // returns 0, not 'default'

    // bad
    const value = '' ?? 'default';
    // returns '', not 'default'

    // good
    const value = null ?? 'default';
    // returns 'default'

    // good
    const user = {
      name: 'John',
      age: null
    };
    const age = user.age ?? 18;
    // returns 18
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Blocks

  <a name="blocks--braces"></a><a name="16.1"></a>
  - [16.1](#blocks--braces) Use braces with all multiline blocks. eslint: [`nonblock-statement-body-position`](https://eslint.org/docs/rules/nonblock-statement-body-position)

    ```javascript
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function foo() { return false; }

    // good
    function bar() {
      return false;
    }
    ```

  <a name="blocks--cuddled-elses"></a><a name="16.2"></a>
  - [16.2](#blocks--cuddled-elses) If you’re using multiline blocks with `if` and `else`, put `else` on the same line as your `if` block’s closing brace. eslint: [`brace-style`](https://eslint.org/docs/rules/brace-style)

    ```javascript
    // bad
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // good
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

  <a name="blocks--no-else-return"></a><a name="16.3"></a>
  - [16.3](#blocks--no-else-return) If an `if` block always executes a `return` statement, the subsequent `else` block is unnecessary. A `return` in an `else if` block following an `if` block that contains a `return` can be separated into multiple `if` blocks. eslint: [`no-else-return`](https://eslint.org/docs/rules/no-else-return)

    ```javascript
    // bad
    function foo() {
      if (x) {
        return x;
      } else {
        return y;
      }
    }

    // bad
    function cats() {
      if (x) {
        return x;
      } else if (y) {
        return y;
      }
    }

    // bad
    function dogs() {
      if (x) {
        return x;
      } else {
        if (y) {
          return y;
        }
      }
    }

    // good
    function foo() {
      if (x) {
        return x;
      }

      return y;
    }

    // good
    function cats() {
      if (x) {
        return x;
      }

      if (y) {
        return y;
      }
    }

    // good
    function dogs(x) {
      if (x) {
        if (z) {
          return y;
        }
      } else {
        return z;
      }
    }
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Control Statements

  <a name="control-statements"></a>
  - [17.1](#control-statements) In case your control statement (`if`, `while` etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line. The logical operator should begin the line.

    > Why? Requiring operators at the beginning of the line keeps the operators aligned and follows a pattern similar to method chaining. This also improves readability by making it easier to visually follow complex logic.

    ```javascript
    // bad
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
      thing1();
    }

    // bad
    if (foo === 123 &&
      bar === 'abc') {
      thing1();
    }

    // bad
    if (foo === 123
      && bar === 'abc') {
      thing1();
    }

    // bad
    if (
      foo === 123 &&
      bar === 'abc'
    ) {
      thing1();
    }

    // good
    if (
      foo === 123
      && bar === 'abc'
    ) {
      thing1();
    }

    // good
    if (
      (foo === 123 || bar === 'abc')
      && doesItLookGoodWhenItBecomesThatLong()
      && isThisReallyHappening()
    ) {
      thing1();
    }

    // good
    if (foo === 123 && bar === 'abc') {
      thing1();
    }
    ```

  <a name="control-statement--value-selection"></a><a name="control-statements--value-selection"></a>
  - [17.2](#control-statements--value-selection) Don't use selection operators in place of control statements.

    ```javascript
    // bad
    !isRunning && startRunning();

    // good
    if (!isRunning) {
      startRunning();
    }
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Comments

  <a name="comments--multiline"></a><a name="17.1"></a>
  - [18.1](#comments--multiline) Use `/** ... */` for multiline comments.

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--singleline"></a><a name="17.2"></a>
  - [18.2](#comments--singleline) Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it’s on the first line of a block.

    ```javascript
    // bad
    const active = true;  // is current tab

    // good
    // is current tab
    const active = true;

    // bad
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // also good
    function getType() {
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }
    ```

  <a name="comments--spaces"></a>
  - [18.3](#comments--spaces) Start all comments with a space to make it easier to read. eslint: [`spaced-comment`](https://eslint.org/docs/rules/spaced-comment)

    ```javascript
    // bad
    //is current tab
    const active = true;

    // good
    // is current tab
    const active = true;

    // bad
    /**
     *make() returns a new element
     *based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--actionitems"></a><a name="17.3"></a>
  - [18.4](#comments--actionitems) Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you’re pointing out a problem that needs to be revisited, or if you’re suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME: -- need to figure this out` or `TODO: -- need to implement`.

  <a name="comments--fixme"></a><a name="17.4"></a>
  - [18.5](#comments--fixme) Use `// FIXME:` to annotate problems.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: shouldn’t use a global here
        total = 0;
      }
    }
    ```

  <a name="comments--todo"></a><a name="17.5"></a>
  - [18.6](#comments--todo) Use `// TODO:` to annotate solutions to problems.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total should be configurable by an options param
        this.total = 0;
      }
    }
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Whitespace

  <a name="whitespace--spaces"></a><a name="18.1"></a>
  - [19.1](#whitespace--spaces) Use soft tabs (space character) set to 2 spaces. eslint: [`indent`](https://eslint.org/docs/rules/indent)

    ```javascript
    // bad
    function foo() {
    ∙∙∙∙let name;
    }

    // bad
    function bar() {
    ∙let name;
    }

    // good
    function baz() {
    ∙∙let name;
    }
    ```

  <a name="whitespace--before-blocks"></a><a name="18.2"></a>
  - [19.2](#whitespace--before-blocks) Place 1 space before the leading brace. eslint: [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    ```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  <a name="whitespace--around-keywords"></a><a name="18.3"></a>
  - [19.3](#whitespace--around-keywords) Place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space between the argument list and the function name in function calls and declarations. eslint: [`keyword-spacing`](https://eslint.org/docs/rules/keyword-spacing)

    ```javascript
    // bad
    if(isJedi) {
      fight ();
    }

    // good
    if (isJedi) {
      fight();
    }

    // bad
    function fight () {
      console.log ('Swooosh!');
    }

    // good
    function fight() {
      console.log('Swooosh!');
    }
    ```

  <a name="whitespace--infix-ops"></a><a name="18.4"></a>
  - [19.4](#whitespace--infix-ops) Set off operators with spaces. eslint: [`space-infix-ops`](https://eslint.org/docs/rules/space-infix-ops)

    ```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
    ```

  <a name="whitespace--newline-at-end"></a><a name="18.5"></a>
  - [19.5](#whitespace--newline-at-end) End files with a single newline character. eslint: [`eol-last`](https://eslint.org/docs/rules/eol-last)

    ```javascript
    // bad
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;
    ```

    ```javascript
    // bad
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ↵
    ```

    ```javascript
    // good
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ```

  <a name="whitespace--chains"></a><a name="18.6"></a>
  - [19.6](#whitespace--chains) Use indentation when making long method chains (more than 2 method chains). Use a leading dot, which
    emphasizes that the line is a method call, not a new statement. eslint: [`newline-per-chained-call`](https://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](https://eslint.org/docs/rules/no-whitespace-before-property)

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // bad
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // good
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // bad
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', `translate(${radius + margin}, ${radius + margin})`)
        .call(tron.led);

    // good
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', `translate(${radius + margin}, ${radius + margin})`)
        .call(tron.led);

    // good
    const leds = stage.selectAll('.led').data(data);
    const svg = leds.enter().append('svg:svg');
    svg.classed('led', true).attr('width', (radius + margin) * 2);
    const g = svg.append('svg:g');
    g.attr('transform', `translate(${radius + margin}, ${radius + margin})`).call(tron.led);
    ```

  <a name="whitespace--after-blocks"></a><a name="18.7"></a>
  - [19.7](#whitespace--after-blocks) Leave a blank line after blocks and before the next statement.

    ```javascript
    // bad
    if (foo) {
      return bar;
    }
    return baz;

    // good
    if (foo) {
      return bar;
    }

    return baz;

    // bad
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // good
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // bad
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // good
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

  <a name="whitespace--padded-blocks"></a><a name="18.8"></a>
  - [19.8](#whitespace--padded-blocks) Do not pad your blocks with blank lines. eslint: [`padded-blocks`](https://eslint.org/docs/rules/padded-blocks)

    ```javascript
    // bad
    function bar() {

      console.log(foo);

    }

    // bad
    if (baz) {

      console.log(quux);
    } else {
      console.log(foo);

    }

    // bad
    class Foo {

      constructor(bar) {
        this.bar = bar;
      }
    }

    // good
    function bar() {
      console.log(foo);
    }

    // good
    if (baz) {
      console.log(quux);
    } else {
      console.log(foo);
    }
    ```

  <a name="whitespace--no-multiple-blanks"></a>
  - [19.9](#whitespace--no-multiple-blanks) Do not use multiple blank lines to pad your code. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    <!-- markdownlint-disable MD012 -->
    ```javascript
    // bad
    class Person {
      constructor(fullName, email, birthday) {
        this.fullName = fullName;


        this.email = email;


        this.setAge(birthday);
      }


      setAge(birthday) {
        const today = new Date();


        const age = this.getAge(today, birthday);


        this.age = age;
      }


      getAge(today, birthday) {
        // ..
      }
    }

    // good
    class Person {
      constructor(fullName, email, birthday) {
        this.fullName = fullName;
        this.email = email;
        this.setAge(birthday);
      }

      setAge(birthday) {
        const today = new Date();
        const age = getAge(today, birthday);
        this.age = age;
      }

      getAge(today, birthday) {
        // ..
      }
    }
    ```

  <a name="whitespace--in-parens"></a><a name="18.9"></a>
  - [19.10](#whitespace--in-parens) Do not add spaces inside parentheses. eslint: [`space-in-parens`](https://eslint.org/docs/rules/space-in-parens)

    ```javascript
    // bad
    function bar( foo ) {
      return foo;
    }

    // good
    function bar(foo) {
      return foo;
    }

    // bad
    if ( foo ) {
      console.log(foo);
    }

    // good
    if (foo) {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-brackets"></a><a name="18.10"></a>
  - [19.11](#whitespace--in-brackets) Do not add spaces inside brackets. eslint: [`array-bracket-spacing`](https://eslint.org/docs/rules/array-bracket-spacing)

    ```javascript
    // bad
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // good
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  <a name="whitespace--in-braces"></a><a name="18.11"></a>
  - [19.12](#whitespace--in-braces) Add spaces inside curly braces. eslint: [`object-curly-spacing`](https://eslint.org/docs/rules/object-curly-spacing)

    ```javascript
    // bad
    const foo = {clark: 'kent'};

    // good
    const foo = { clark: 'kent' };
    ```

  <a name="whitespace--max-len"></a><a name="18.12"></a>
  - [19.13](#whitespace--max-len) Avoid having lines of code that are longer than 100 characters (including whitespace). Note: per [above](#strings--line-length), long strings are exempt from this rule, and should not be broken up. eslint: [`max-len`](https://eslint.org/docs/rules/max-len)

    > Why? This ensures readability and maintainability.

    ```javascript
    // bad
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    // bad
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    // good
    const foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    // better
    const foo = jsonData
      ?.foo
      ?.bar
      ?.baz
      ?.quux
      ?.xyzzy;

    // good
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' },
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```

  <a name="whitespace--block-spacing"></a>
  - [19.14](#whitespace--block-spacing) Require consistent spacing inside an open block token and the next token on the same line. This rule also enforces consistent spacing inside a close block token and previous token on the same line. eslint: [`block-spacing`](https://eslint.org/docs/rules/block-spacing)

    ```javascript
    // bad
    function foo() {return true;}
    if (foo) { bar = 0;}

    // good
    function foo() { return true; }
    if (foo) { bar = 0; }
    ```

  <a name="whitespace--comma-spacing"></a>
  - [19.15](#whitespace--comma-spacing) Avoid spaces before commas and require a space after commas. eslint: [`comma-spacing`](https://eslint.org/docs/rules/comma-spacing)

    ```javascript
    // bad
    const foo = 1,bar = 2;
    const arr = [1 , 2];

    // good
    const foo = 1, bar = 2;
    const arr = [1, 2];
    ```

  <a name="whitespace--computed-property-spacing"></a>
  - [19.16](#whitespace--computed-property-spacing) Enforce spacing inside of computed property brackets. eslint: [`computed-property-spacing`](https://eslint.org/docs/rules/computed-property-spacing)

    ```javascript
    // bad
    obj[foo ]
    obj[ 'foo']
    const x = {[ b ]: a}
    obj[foo[ bar ]]

    // good
    obj[foo]
    obj['foo']
    const x = { [b]: a }
    obj[foo[bar]]
    ```

  <a name="whitespace--func-call-spacing"></a>
  - [19.17](#whitespace--func-call-spacing) Avoid spaces between functions and their invocations. eslint: [`func-call-spacing`](https://eslint.org/docs/rules/func-call-spacing)

    ```javascript
    // bad
    func ();

    func
    ();

    // good
    func();
    ```

  <a name="whitespace--key-spacing"></a>
  - [19.18](#whitespace--key-spacing) Enforce spacing between keys and values in object literal properties. eslint: [`key-spacing`](https://eslint.org/docs/rules/key-spacing)

    ```javascript
    // bad
    const obj = { foo : 42 };
    const obj2 = { foo:42 };

    // good
    const obj = { foo: 42 };
    ```

  <a name="whitespace--no-trailing-spaces"></a>
  - [19.19](#whitespace--no-trailing-spaces) Avoid trailing spaces at the end of lines. eslint: [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces)

  <a name="whitespace--no-multiple-empty-lines"></a>
  - [19.20](#whitespace--no-multiple-empty-lines) Avoid multiple empty lines, only allow one newline at the end of files, and avoid a newline at the beginning of files. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    <!-- markdownlint-disable MD012 -->
    ```javascript
    // bad - multiple empty lines
    const x = 1;


    const y = 2;

    // bad - 2+ newlines at end of file
    const x = 1;
    const y = 2;


    // bad - 1+ newline(s) at beginning of file

    const x = 1;
    const y = 2;

    // good
    const x = 1;
    const y = 2;

    ```
    <!-- markdownlint-enable MD012 -->

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Commas

  <a name="commas--leading-trailing"></a><a name="19.1"></a>
  - [20.1](#commas--leading-trailing) Leading commas: **Nope.** eslint: [`comma-style`](https://eslint.org/docs/rules/comma-style)

    ```javascript
    // bad
    const story = [
        once
      , upon
      , aTime
    ];

    // good
    const story = [
      once,
      upon,
      aTime,
    ];

    // bad
    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    // good
    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

  <a name="commas--dangling"></a><a name="19.2"></a>
  - [20.2](#commas--dangling) Additional trailing comma: **Yup.** eslint: [`comma-dangle`](https://eslint.org/docs/rules/comma-dangle)

    > Why? This leads to cleaner git diffs. Also, transpilers like Babel will remove the additional trailing comma in the transpiled code which means you don’t have to worry about the [trailing comma problem](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas) in legacy browsers.

    ```diff
    // bad - git diff without trailing comma
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    // good - git diff with trailing comma
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };
    ```

    ```javascript
    // bad
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // good
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];

    // bad
    function createHero(
      firstName,
      lastName,
      inventorOf
    ) {
      // does nothing
    }

    // good
    function createHero(
      firstName,
      lastName,
      inventorOf,
    ) {
      // does nothing
    }

    // good (note that a comma must not appear after a "rest" element)
    function createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    ) {
      // does nothing
    }

    // bad
    createHero(
      firstName,
      lastName,
      inventorOf
    );

    // good
    createHero(
      firstName,
      lastName,
      inventorOf,
    );

    // good (note that a comma must not appear after a "rest" element)
    createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    );
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Semicolons

  <a name="semicolons--required"></a><a name="20.1"></a>
  - [21.1](#semicolons--required) **Yup.** eslint: [`semi`](https://eslint.org/docs/rules/semi)

    > Why? When JavaScript encounters a line break without a semicolon, it uses a set of rules called [Automatic Semicolon Insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) to determine whether it should regard that line break as the end of a statement, and (as the name implies) place a semicolon into your code before the line break if it thinks so. ASI contains a few eccentric behaviors, though, and your code will break if JavaScript misinterprets your line break. These rules will become more complicated as new features become a part of JavaScript. Explicitly terminating your statements and configuring your linter to catch missing semicolons will help prevent you from encountering issues.

    ```javascript
    // bad - raises exception
    const luke = {}
    const leia = {}
    [luke, leia].forEach((jedi) => jedi.father = 'vader')

    // bad - raises exception
    const reaction = "No! That’s impossible!"
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }())

    // bad - returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
    function foo() {
      return
        'search your feelings, you know it to be foo'
    }

    // good
    const luke = {};
    const leia = {};
    [luke, leia].forEach((jedi) => {
      jedi.father = 'vader';
    });

    // good
    const reaction = 'No! That’s impossible!';
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }());

    // good
    function foo() {
      return 'search your feelings, you know it to be foo';
    }
    ```

    [Read more](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214#7365214).

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Type Casting & Coercion

  <a name="coercion--explicit"></a><a name="21.1"></a>
  - [22.1](#coercion--explicit) Perform type coercion at the beginning of the statement.

  <a name="coercion--strings"></a><a name="21.2"></a>
  - [22.2](#coercion--strings) Strings: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    // => this.reviewScore = 9;

    // bad
    const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

    // bad
    const totalScore = this.reviewScore + ''; // invokes this.reviewScore.valueOf()

    // bad
    const totalScore = this.reviewScore.toString(); // isn’t guaranteed to return a string

    // good
    const totalScore = String(this.reviewScore);
    ```

  <a name="coercion--numbers"></a><a name="21.3"></a>
  - [22.3](#coercion--numbers) Numbers: Use `Number` for type casting and `parseInt` always with a radix for parsing strings. eslint: [`radix`](https://eslint.org/docs/rules/radix) [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    > Why? The `parseInt` function produces an integer value dictated by interpretation of the contents of the string argument according to the specified radix. Leading whitespace in string is ignored. If radix is `undefined` or `0`, it is assumed to be `10` except when the number begins with the character pairs `0x` or `0X`, in which case a radix of 16 is assumed. This differs from ECMAScript 3, which merely discouraged (but allowed) octal interpretation. Many implementations have not adopted this behavior as of 2013. And, because older browsers must be supported, always specify a radix.

    ```javascript
    const inputValue = '4';

    // bad
    const val = new Number(inputValue);

    // bad
    const val = +inputValue;

    // bad
    const val = inputValue >> 0;

    // bad
    const val = parseInt(inputValue);

    // good
    const val = Number(inputValue);

    // good
    const val = parseInt(inputValue, 10);
    ```

  <a name="coercion--comment-deviations"></a><a name="21.4"></a>
  - [22.4](#coercion--comment-deviations) If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need to use Bitshift for [performance reasons](https://web.archive.org/web/20200414205431/https://jsperf.com/coercion-vs-casting/3), leave a comment explaining why and what you’re doing.

    ```javascript
    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    const val = inputValue >> 0;
    ```

  <a name="coercion--bitwise"></a><a name="21.5"></a>
  - [22.5](#coercion--bitwise) **Note:** Be careful when using bitshift operations. Numbers are represented as [64-bit values](https://es5.github.io/#x4.3.19), but bitshift operations always return a 32-bit integer ([source](https://es5.github.io/#x11.7)). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. [Discussion](https://github.com/airbnb/javascript/issues/109). Largest signed 32-bit Int is 2,147,483,647:

    ```javascript
    2147483647 >> 0; // => 2147483647
    2147483648 >> 0; // => -2147483648
    2147483649 >> 0; // => -2147483647
    ```

  <a name="coercion--booleans"></a><a name="21.6"></a>
  - [22.6](#coercion--booleans) Booleans: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    const age = 0;

    // bad
    const hasAge = new Boolean(age);

    // good
    const hasAge = Boolean(age);

    // best
    const hasAge = !!age;
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Naming Conventions

  <a name="naming--descriptive"></a><a name="22.1"></a>
  - [23.1](#naming--descriptive) Avoid single letter names. Be descriptive with your naming. eslint: [`id-length`](https://eslint.org/docs/rules/id-length)

    ```javascript
    // bad
    function q() {
      // ...
    }

    // good
    function query() {
      // ...
    }
    ```

  <a name="naming--camelCase"></a><a name="22.2"></a>
  - [23.2](#naming--camelCase) Use camelCase when naming objects, functions, and instances. eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase)

    ```javascript
    // bad
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // good
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  <a name="naming--PascalCase"></a><a name="22.3"></a>
  - [23.3](#naming--PascalCase) Use PascalCase only when naming constructors or classes. eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap)

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // good
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

  <a name="naming--leading-underscore"></a><a name="22.4"></a>
  - [23.4](#naming--leading-underscore) Do not use trailing or leading underscores. eslint: [`no-underscore-dangle`](https://eslint.org/docs/rules/no-underscore-dangle)

    > Why? JavaScript does not have the concept of privacy in terms of properties or methods. Although a leading underscore is a common convention to mean “private”, in fact, these properties are fully public, and as such, are part of your public API contract. This convention might lead developers to wrongly think that a change won’t count as breaking, or that tests aren’t needed. tl;dr: if you want something to be “private”, it must not be observably present.

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // good
    this.firstName = 'Panda';

    // good, in environments where WeakMaps are available
    // see https://compat-table.github.io/compat-table/es6/#test-WeakMap
    const firstNames = new WeakMap();
    firstNames.set(this, 'Panda');
    ```

  <a name="naming--self-this"></a><a name="22.5"></a>
  - [23.5](#naming--self-this) Don’t save references to `this`. Use arrow functions or [Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).

    ```javascript
    // bad
    function foo() {
      const self = this;
      return function () {
        console.log(self);
      };
    }

    // bad
    function foo() {
      const that = this;
      return function () {
        console.log(that);
      };
    }

    // good
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```

  <a name="naming--filename-matches-export"></a><a name="22.6"></a>
  - [23.6](#naming--filename-matches-export) A base filename should exactly match the name of its default export.

    ```javascript
    // file 1 contents
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // file 2 contents
    export default function fortyTwo() { return 42; }

    // file 3 contents
    export default function insideDirectory() {}

    // in some other file
    // bad
    import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
    import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
    import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

    // bad
    import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
    import forty_two from './forty_two'; // snake_case import/filename, camelCase export
    import inside_directory from './inside_directory'; // snake_case import, camelCase export
    import index from './inside_directory/index'; // requiring the index file explicitly
    import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

    // good
    import CheckBox from './CheckBox'; // PascalCase export/import/filename
    import fortyTwo from './fortyTwo'; // camelCase export/import/filename
    import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
    // ^ supports both insideDirectory.js and insideDirectory/index.js
    ```

  <a name="naming--camelCase-default-export"></a><a name="22.7"></a>
  - [23.7](#naming--camelCase-default-export) Use camelCase when you export-default a function. Your filename should be identical to your function’s name.

    ```javascript
    function makeStyleGuide() {
      // ...
    }

    export default makeStyleGuide;
    ```

  <a name="naming--PascalCase-singleton"></a><a name="22.8"></a>
  - [23.8](#naming--PascalCase-singleton) Use PascalCase when you export a constructor / class / singleton / function library / bare object.

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      },
    };

    export default AirbnbStyleGuide;
    ```

  <a name="naming--Acronyms-and-Initialisms"></a>
  - [23.9](#naming--Acronyms-and-Initialisms) Acronyms and initialisms should always be all uppercased, or all lowercased.

    > Why? Names are for readability, not to appease a computer algorithm.

    ```javascript
    // bad
    import SmsContainer from './containers/SmsContainer';

    // bad
    const HttpRequests = [
      // ...
    ];

    // good
    import SMSContainer from './containers/SMSContainer';

    // good
    const HTTPRequests = [
      // ...
    ];

    // also good
    const httpRequests = [
      // ...
    ];

    // best
    import TextMessageContainer from './containers/TextMessageContainer';

    // best
    const requests = [
      // ...
    ];
    ```

  <a name="naming--uppercase"></a>
  - [23.10](#naming--uppercase) You may optionally uppercase a constant only if it (1) is exported, (2) is a `const` (it can not be reassigned), and (3) the programmer can trust it (and its nested properties) to never change.

    > Why? This is an additional tool to assist in situations where the programmer would be unsure if a variable might ever change. UPPERCASE_VARIABLES are letting the programmer know that they can trust the variable (and its properties) not to change.
    - What about all `const` variables? - This is unnecessary, so uppercasing should not be used for constants within a file. It should be used for exported constants however.
    - What about exported objects? - Uppercase at the top level of export (e.g. `EXPORTED_OBJECT.key`) and maintain that all nested properties do not change.

    ```javascript
    // bad
    const PRIVATE_VARIABLE = 'should not be unnecessarily uppercased within a file';

    // bad
    export const THING_TO_BE_CHANGED = 'should obviously not be uppercased';

    // bad
    export let REASSIGNABLE_VARIABLE = 'do not use let with uppercase variables';

    // ---

    // allowed but does not supply semantic value
    export const apiKey = 'SOMEKEY';

    // better in most cases
    export const API_KEY = 'SOMEKEY';

    // ---

    // bad - unnecessarily uppercases key while adding no semantic value
    export const MAPPING = {
      KEY: 'value'
    };

    // good
    export const MAPPING = {
      key: 'value',
    };
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Accessors

  <a name="accessors--not-required"></a><a name="23.1"></a>
  - [24.1](#accessors--not-required) Accessor functions for properties are not required.

  <a name="accessors--no-getters-setters"></a><a name="23.2"></a>
  - [24.2](#accessors--no-getters-setters) Do not use JavaScript getters/setters as they cause unexpected side effects and are harder to test, maintain, and reason about. Instead, if you do make accessor functions, use `getVal()` and `setVal('hello')`.

    ```javascript
    // bad
    class Dragon {
      get age() {
        // ...
      }

      set age(value) {
        // ...
      }
    }

    // good
    class Dragon {
      getAge() {
        // ...
      }

      setAge(value) {
        // ...
      }
    }
    ```

  <a name="accessors--boolean-prefix"></a><a name="23.3"></a>
  - [24.3](#accessors--boolean-prefix) If the property/method is a `boolean`, use `isVal()` or `hasVal()`.

    ```javascript
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  <a name="accessors--consistent"></a><a name="23.4"></a>
  - [24.4](#accessors--consistent) It’s okay to create `get()` and `set()` functions, but be consistent.

    ```javascript
    class Jedi {
      constructor(options = {}) {
        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Events

  <a name="events--hash"></a><a name="24.1"></a>
  - [25.1](#events--hash) When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass an object literal (also known as a "hash") instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

    ```javascript
    // bad
    $(this).trigger('listingUpdated', listing.id);

    // ...

    $(this).on('listingUpdated', (e, listingID) => {
      // do something with listingID
    });
    ```

    prefer:

    ```javascript
    // good
    $(this).trigger('listingUpdated', { listingID: listing.id });

    // ...

    $(this).on('listingUpdated', (e, data) => {
      // do something with data.listingID
    });
    ```

  **[⬆ بازگشت به بالا](#فهرست-مطالب)**

## jQuery

  <a name="jquery--dollar-prefix"></a><a name="25.1"></a>
  - [26.1](#jquery--dollar-prefix) Prefix jQuery object variables with a `$`.

    ```javascript
    // bad
    const sidebar = $('.sidebar');

    // good
    const $sidebar = $('.sidebar');

    // good
    const $sidebarBtn = $('.sidebar-btn');
    ```

  <a name="jquery--cache"></a><a name="25.2"></a>
  - [26.2](#jquery--cache) Cache jQuery lookups.

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...

      $('.sidebar').css({
        'background-color': 'pink',
      });
    }

    // good
    function setSidebar() {
      const $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...

      $sidebar.css({
        'background-color': 'pink',
      });
    }
    ```

  <a name="jquery--queries"></a><a name="25.3"></a>
  - [26.3](#jquery--queries) For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](https://web.archive.org/web/20200414183810/https://jsperf.com/jquery-find-vs-context-sel/16)

  <a name="jquery--find"></a><a name="25.4"></a>
  - [26.4](#jquery--find) Use `find` with scoped jQuery object queries.

    ```javascript
    // bad
    $('ul', '.sidebar').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good
    $sidebar.find('ul').hide();
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## ECMAScript 5 Compatibility

  <a name="es5-compat--kangax"></a><a name="26.1"></a>
  - [27.1](#es5-compat--kangax) Refer to [Kangax](https://twitter.com/kangax/)’s ES5 [compatibility table](https://compat-table.github.io/compat-table/es5/).

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

<a name="ecmascript-6-styles"></a>
## ECMAScript 6+ (ES 2015+) Styles

  <a name="es6-styles"></a><a name="27.1"></a>
  - [28.1](#es6-styles) This is a collection of links to the various ES6+ features.

1. [Arrow Functions](#arrow-functions)
1. [Classes](#classes--constructors)
1. [Object Shorthand](#es6-object-shorthand)
1. [Object Concise](#es6-object-concise)
1. [Object Computed Properties](#es6-computed-properties)
1. [Template Strings](#es6-template-literals)
1. [Destructuring](#destructuring)
1. [Default Parameters](#es6-default-parameters)
1. [Rest](#es6-rest)
1. [Array Spreads](#es6-array-spreads)
1. [Let and Const](#references)
1. [Exponentiation Operator](#es2016-properties--exponentiation-operator)
1. [Iterators and Generators](#iterators-and-generators)
1. [Modules](#modules)

  <a name="tc39-proposals"></a>
  - [28.2](#tc39-proposals) Do not use [TC39 proposals](https://github.com/tc39/proposals) that have not reached stage 3.

    > Why? [They are not finalized](https://tc39.github.io/process-document/), and they are subject to change or to be withdrawn entirely. We want to use JavaScript, and proposals are not JavaScript yet.

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Standard Library

  The [Standard Library](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects)
  contains utilities that are functionally broken but remain for legacy reasons.

  <a name="standard-library--isnan"></a>
  - [29.1](#standard-library--isnan) Use `Number.isNaN` instead of global `isNaN`.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > Why? The global `isNaN` coerces non-numbers to numbers, returning true for anything that coerces to NaN.
    > If this behavior is desired, make it explicit.

    ```javascript
    // bad
    isNaN('1.2'); // false
    isNaN('1.2.3'); // true

    // good
    Number.isNaN('1.2.3'); // false
    Number.isNaN(Number('1.2.3')); // true
    ```

  <a name="standard-library--isfinite"></a>
  - [29.2](#standard-library--isfinite) Use `Number.isFinite` instead of global `isFinite`.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > Why? The global `isFinite` coerces non-numbers to numbers, returning true for anything that coerces to a finite number.
    > If this behavior is desired, make it explicit.

    ```javascript
    // bad
    isFinite('2e3'); // true

    // good
    Number.isFinite('2e3'); // false
    Number.isFinite(parseInt('2e3', 10)); // true
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Testing

  <a name="testing--yup"></a><a name="28.1"></a>
  - [30.1](#testing--yup) **Yup.**

    ```javascript
    function foo() {
      return true;
    }
    ```

  <a name="testing--for-real"></a><a name="28.2"></a>
  - [30.2](#testing--for-real) **No, but seriously**:
    - Whichever testing framework you use, you should be writing tests!
    - Strive to write many small pure functions, and minimize where mutations occur.
    - Be cautious about stubs and mocks - they can make your tests more brittle.
    - We primarily use [`mocha`](https://www.npmjs.com/package/mocha) and [`jest`](https://www.npmjs.com/package/jest) at Airbnb. [`tape`](https://www.npmjs.com/package/tape) is also used occasionally for small, separate modules.
    - 100% test coverage is a good goal to strive for, even if it’s not always practical to reach it.
    - Whenever you fix a bug, *write a regression test*. A bug fixed without a regression test is almost certainly going to break again in the future.

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Performance

  - [On Layout & Web Performance](https://www.kellegous.com/j/2013/01/26/layout-performance/)
  - [String vs Array Concat](https://web.archive.org/web/20200414200857/https://jsperf.com/string-vs-array-concat/2)
  - [Try/Catch Cost In a Loop](https://web.archive.org/web/20200414190827/https://jsperf.com/try-catch-in-loop-cost/12)
  - [Bang Function](https://web.archive.org/web/20200414205426/https://jsperf.com/bang-function)
  - [jQuery Find vs Context, Selector](https://web.archive.org/web/20200414200850/https://jsperf.com/jquery-find-vs-context-sel/164)
  - [innerHTML vs textContent for script text](https://web.archive.org/web/20200414205428/https://jsperf.com/innerhtml-vs-textcontent-for-script-text)
  - [Long String Concatenation](https://web.archive.org/web/20200414203914/https://jsperf.com/ya-string-concat/38)
  - [Are JavaScript functions like `map()`, `reduce()`, and `filter()` optimized for traversing arrays?](https://www.quora.com/JavaScript-programming-language-Are-Javascript-functions-like-map-reduce-and-filter-already-optimized-for-traversing-array/answer/Quildreen-Motta)
  - Loading...

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Resources

**Learning ES6+**

  - [Latest ECMA spec](https://tc39.github.io/ecma262/)
  - [ExploringJS](https://exploringjs.com/)
  - [ES6 Compatibility Table](https://compat-table.github.io/compat-table/es6/)
  - [Comprehensive Overview of ES6 Features](https://web.archive.org/web/20240404212626/http://es6-features.org/)
  - [JavaScript Roadmap](https://roadmap.sh/javascript)

**Read This**

  - [Standard ECMA-262](https://www.ecma-international.org/ecma-262/6.0/index.html)

**Tools**

  - Code Style Linters
    - [ESlint](https://eslint.org/) - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)
    - [JSHint](https://jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/.jshintrc)
  - Neutrino Preset - [@neutrinojs/airbnb](https://neutrinojs.org/packages/airbnb/)

**Other Style Guides**

  - [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
  - [Google JavaScript Style Guide (Old)](https://google.github.io/styleguide/javascriptguide.xml)
  - [jQuery Core Style Guidelines](https://contribute.jquery.org/style-guide/js/)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)
  - [StandardJS](https://standardjs.com)

**Other Styles**

  - [Naming this in nested functions](https://gist.github.com/cjohansen/4135065) - Christian Johansen
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
  - [Popular JavaScript Coding Conventions on GitHub](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
  - [Multiple var statements in JavaScript, not superfluous](https://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**Further Reading**

  - [Understanding JavaScript Closures](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [Basic JavaScript for the impatient programmer](https://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [You Might Not Need jQuery](https://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
  - [Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**Books**

  - [JavaScript: The Good Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](https://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](https://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X) - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](https://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](https://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](https://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](https://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](https://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
  - [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
  - [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](https://jsbooks.revolunet.com/) - Julien Bouquillon
  - [Third Party JavaScript](https://www.manning.com/books/third-party-javascript) - Ben Vinegar and Anton Kovalyov
  - [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](https://amzn.com/dp/0321812182) - David Herman
  - [Eloquent JavaScript](https://eloquentjavascript.net/) - Marijn Haverbeke
  - [You Don’t Know JS: ES6 & Beyond](https://shop.oreilly.com/product/0636920033769.do) - Kyle Simpson

**Blogs**

  - [JavaScript Weekly](https://javascriptweekly.com/)
  - [JavaScript, JavaScript...](https://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](https://bocoup.com/weblog)
  - [Adequately Good](https://www.adequatelygood.com/)
  - [NCZOnline](https://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](https://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [nettuts](https://code.tutsplus.com/?s=javascript)

**Podcasts**

  - [JavaScript Air](https://javascriptair.com/)
  - [JavaScript Jabber](https://devchat.tv/js-jabber/)

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## In the Wild

  This is a list of organizations that are using this style guide. Send us a pull request and we'll add you to the list.

  - **123erfasst**: [123erfasst/javascript](https://github.com/123erfasst/javascript)
  - **4Catalyzer**: [4Catalyzer/javascript](https://github.com/4Catalyzer/javascript)
  - **Aan Zee**: [AanZee/javascript](https://github.com/AanZee/javascript)
  - **Airbnb**: [airbnb/javascript](https://github.com/airbnb/javascript)
  - **AloPeyk**: [AloPeyk](https://github.com/AloPeyk)
  - **AltSchool**: [AltSchool/javascript](https://github.com/AltSchool/javascript)
  - **Apartmint**: [apartmint/javascript](https://github.com/apartmint/javascript)
  - **Ascribe**: [ascribe/javascript](https://github.com/ascribe/javascript)
  - **Avant**: [avantcredit/javascript](https://github.com/avantcredit/javascript)
  - **Axept**: [axept/javascript](https://github.com/axept/javascript)
  - **Billabong**: [billabong/javascript](https://github.com/billabong/javascript)
  - **Bisk**: [bisk](https://github.com/Bisk/)
  - **Brainshark**: [brainshark/javascript](https://github.com/brainshark/javascript)
  - **CaseNine**: [CaseNine/javascript](https://github.com/CaseNine/javascript)
  - **Cerner**: [Cerner](https://github.com/cerner/)
  - **Chartboost**: [ChartBoost/javascript-style-guide](https://github.com/ChartBoost/javascript-style-guide)
  - **Coeur d'Alene Tribe**: [www.cdatribe-nsn.gov](https://www.cdatribe-nsn.gov)
  - **ComparaOnline**: [comparaonline/javascript](https://github.com/comparaonline/javascript-style-guide)
  - **Compass Learning**: [compasslearning/javascript-style-guide](https://github.com/compasslearning/javascript-style-guide)
  - **DailyMotion**: [dailymotion/javascript](https://github.com/dailymotion/javascript)
  - **DoSomething**: [DoSomething/eslint-config](https://github.com/DoSomething/eslint-config)
  - **Digitpaint** [digitpaint/javascript](https://github.com/digitpaint/javascript)
  - **Drupal**: [www.drupal.org](https://git.drupalcode.org/project/drupal/blob/8.6.x/core/.eslintrc.json)
  - **Ecosia**: [ecosia/javascript](https://github.com/ecosia/javascript)
  - **Evolution Gaming**: [evolution-gaming/javascript](https://github.com/evolution-gaming/javascript)
  - **EvozonJs**: [evozonjs/javascript](https://github.com/evozonjs/javascript)
  - **ExactTarget**: [ExactTarget/javascript](https://github.com/ExactTarget/javascript)
  - **Flexberry**: [Flexberry/javascript-style-guide](https://github.com/Flexberry/javascript-style-guide)
  - **Gawker Media**: [gawkermedia](https://github.com/gawkermedia/)
  - **General Electric**: [GeneralElectric/javascript](https://github.com/GeneralElectric/javascript)
  - **Generation Tux**: [GenerationTux/javascript](https://github.com/generationtux/styleguide)
  - **GoodData**: [gooddata/gdc-js-style](https://github.com/gooddata/gdc-js-style)
  - **GreenChef**: [greenchef/javascript](https://github.com/greenchef/javascript)
  - **Grooveshark**: [grooveshark/javascript](https://github.com/grooveshark/javascript)
  - **Grupo-Abraxas**: [Grupo-Abraxas/javascript](https://github.com/Grupo-Abraxas/javascript)
  - **Happeo**: [happeo/javascript](https://github.com/happeo/javascript)
  - **How About We**: [howaboutwe/javascript](https://github.com/howaboutwe/javascript-style-guide)
  - **HubSpot**: [HubSpot/javascript](https://github.com/HubSpot/javascript)
  - **Hyper**: [hyperoslo/javascript-playbook](https://github.com/hyperoslo/javascript-playbook/blob/master/style.md)
  - **ILIAS**: [ILIAS](https://github.com/ILIAS-eLearning/ILIAS)
  - **InterCity Group**: [intercitygroup/javascript-style-guide](https://github.com/intercitygroup/javascript-style-guide)
  - **Jam3**: [Jam3/Javascript-Code-Conventions](https://github.com/Jam3/Javascript-Code-Conventions)
  - **JSSolutions**: [JSSolutions/javascript](https://github.com/JSSolutions/javascript)
  - **Kaplan Komputing**: [kaplankomputing/javascript](https://github.com/kaplankomputing/javascript)
  - **KickorStick**: [kickorstick](https://github.com/kickorstick/)
  - **Kinetica Solutions**: [kinetica/javascript](https://github.com/kinetica/Javascript-style-guide)
  - **LEINWAND**: [LEINWAND/javascript](https://github.com/LEINWAND/javascript)
  - **Lonely Planet**: [lonelyplanet/javascript](https://github.com/lonelyplanet/javascript)
  - **M2GEN**: [M2GEN/javascript](https://github.com/M2GEN/javascript)
  - **Mighty Spring**: [mightyspring/javascript](https://github.com/mightyspring/javascript)
  - **MinnPost**: [MinnPost/javascript](https://github.com/MinnPost/javascript)
  - **MitocGroup**: [MitocGroup/javascript](https://github.com/MitocGroup/javascript)
  - **Muber**: [muber](https://github.com/muber/)
  - **National Geographic Society**: [natgeosociety](https://github.com/natgeosociety/)
  - **NullDev**: [NullDevCo/JavaScript-Styleguide](https://github.com/NullDevCo/JavaScript-Styleguide)
  - **Nulogy**: [nulogy/javascript](https://github.com/nulogy/javascript)
  - **Orange Hill Development**: [orangehill/javascript](https://github.com/orangehill/javascript)
  - **Orion Health**: [orionhealth/javascript](https://github.com/orionhealth/javascript)
  - **Peerby**: [Peerby/javascript](https://github.com/Peerby/javascript)
  - **Pier 1**: [Pier1/javascript](https://github.com/pier1/javascript)
  - **Qotto**: [Qotto/javascript-style-guide](https://github.com/Qotto/javascript-style-guide)
  - **React**: [reactjs.org/docs/how-to-contribute.html#style-guide](https://reactjs.org/docs/how-to-contribute.html#style-guide)
  - **Ripple**: [ripple/javascript-style-guide](https://github.com/ripple/javascript-style-guide)
  - **Sainsbury’s Supermarkets**: [jsainsburyplc](https://github.com/jsainsburyplc)
  - **Shutterfly**: [shutterfly/javascript](https://github.com/shutterfly/javascript)
  - **Sourcetoad**: [sourcetoad/javascript](https://github.com/sourcetoad/javascript)
  - **Springload**: [springload](https://github.com/springload/)
  - **StratoDem Analytics**: [stratodem/javascript](https://github.com/stratodem/javascript)
  - **SteelKiwi Development**: [steelkiwi/javascript](https://github.com/steelkiwi/javascript)
  - **StudentSphere**: [studentsphere/javascript](https://github.com/studentsphere/guide-javascript)
  - **SwoopApp**: [swoopapp/javascript](https://github.com/swoopapp/javascript)
  - **SysGarage**: [sysgarage/javascript-style-guide](https://github.com/sysgarage/javascript-style-guide)
  - **Syzygy Warsaw**: [syzygypl/javascript](https://github.com/syzygypl/javascript)
  - **Target**: [target/javascript](https://github.com/target/javascript)
  - **Terra**: [terra](https://github.com/cerner?utf8=%E2%9C%93&q=terra&type=&language=)
  - **TheLadders**: [TheLadders/javascript](https://github.com/TheLadders/javascript)
  - **The Nerdery**: [thenerdery/javascript-standards](https://github.com/thenerdery/javascript-standards)
  - **Tomify**: [tomprats](https://github.com/tomprats)
  - **Traitify**: [traitify/eslint-config-traitify](https://github.com/traitify/eslint-config-traitify)
  - **T4R Technology**: [T4R-Technology/javascript](https://github.com/T4R-Technology/javascript)
  - **UrbanSim**: [urbansim](https://github.com/urbansim/)
  - **VoxFeed**: [VoxFeed/javascript-style-guide](https://github.com/VoxFeed/javascript-style-guide)
  - **WeBox Studio**: [weboxstudio/javascript](https://github.com/weboxstudio/javascript)
  - **Weggo**: [Weggo/javascript](https://github.com/Weggo/javascript)
  - **Zillow**: [zillow/javascript](https://github.com/zillow/javascript)
  - **Zit Software**: [zit-software/javascript](https://github.com/zit-software/javascript)
  - **ZocDoc**: [ZocDoc/javascript](https://github.com/ZocDoc/javascript)

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Translation

  This style guide is also available in other languages:

  - ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [armoucar/javascript-style-guide](https://github.com/armoucar/javascript-style-guide)
  - ![bg](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bulgaria.png) **Bulgarian**: [borislavvv/javascript](https://github.com/borislavvv/javascript)
  - ![ca](https://raw.githubusercontent.com/fpmweb/javascript-style-guide/master/img/catala.png) **Catalan**: [fpmweb/javascript-style-guide](https://github.com/fpmweb/javascript-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [lin-123/javascript](https://github.com/lin-123/javascript)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [jigsawye/javascript](https://github.com/jigsawye/javascript)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [nmussy/javascript-style-guide](https://github.com/nmussy/javascript-style-guide)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [timofurrer/javascript-style-guide](https://github.com/timofurrer/javascript-style-guide)
  - ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [sinkswim/javascript-style-guide](https://github.com/sinkswim/javascript-style-guide)
  - ![jp](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/javascript-style-guide](https://github.com/mitsuruog/javascript-style-guide)
  - ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [ParkSB/javascript-style-guide](https://github.com/ParkSB/javascript-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [leonidlebedev/javascript-airbnb](https://github.com/leonidlebedev/javascript-airbnb)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [paolocarrasco/javascript-style-guide](https://github.com/paolocarrasco/javascript-style-guide)
  - ![th](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Thailand.png) **Thai**: [lvarayut/javascript-style-guide](https://github.com/lvarayut/javascript-style-guide)
  - ![tr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Turkey.png) **Turkish**: [eraycetinay/javascript](https://github.com/eraycetinay/javascript)
  - ![ua](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Ukraine.png) **Ukrainian**: [ivanzusko/javascript](https://github.com/ivanzusko/javascript)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnam**: [dangkyokhoang/javascript-style-guide](https://github.com/dangkyokhoang/javascript-style-guide)

## The JavaScript Style Guide Guide

  - [Reference](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)

## Chat With Us About JavaScript

  - Find us on [gitter](https://gitter.im/airbnb/javascript).

## Contributors

  - [View Contributors](https://github.com/airbnb/javascript/graphs/contributors)

## License

(The MIT License)

Copyright (c) 2012 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## Amendments

We encourage you to fork this guide and change the rules to fit your team’s style guide. Below, you may list some amendments to the style guide. This allows you to periodically update your style guide without having to deal with merge conflicts.

# };
