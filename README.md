# راهنمای نوشتاری جاوااسکریپتِ Airbnb() {

*رویکردی، تا حد زیاد معقول به جاوااسکریپت*

> **نکته**: این راهنما فرض می‌کند از [Babel](https://babeljs.io) استفاده می‌کنید و نیاز دارد از [babel-preset-airbnb](https://npmjs.com/babel-preset-airbnb) یا معادل آن استفاده کنید. همچنین فرض می‌کند شیم/پُلی‌فیل‌ها را در نرم افزار خود نصب می‌کنید، با [airbnb-browser-shims](https://npmjs.com/airbnb-browser-shims) یا معادل آن.

[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb.svg)](https://www.npmjs.com/package/eslint-config-airbnb)
[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb-base.svg)](https://www.npmjs.com/package/eslint-config-airbnb-base)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/airbnb/javascript?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

این راهنما به زبان‌های دیگری هم در دسترس است. [ترجمه](#ترجمه) را ببینید

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
1. [عملگرهای مقایسه و برابری](#عملگرهای-مقایسه-و-برابری)
1. [بلوک ها](#بلوک-ها)
1. [دستورهای کنترلی](#دستورهای-کنترلی)
1. [توضیحات (comments)](#توضیحات-Comments)
1. [فاصله گذاری](#فاصله-گذاری)
1. [ویرگول ها](#ویرگول-ها)
1. [نقطه ویرگول ها](#نقطه-ویرگول-ها)
1. [تبدیل نوع و واداشتن به تبدیل (Coercion)](#تبدیل-نوع-و-واداشتن-به-تبدیل-Coercion)
1. [مقررات نام گذاری](#مقررات-نام-گذاری)
1. [اکسسورها (Accessors)](#اکسسورها-Accessors)
1. [رویدادها (events)](#رویدادها-Events)
1. [jQuery](#jquery)
1. [سازگاری با ECMAScript 5](#سازگاری-با-ECMAScript-5)
1. [سبک‌های ECMAScript 6+ (ES 2015+)](#ecmascript-6-es-2015-styles)
1. [کتابخانه استاندارد](#کتابخانه-استاندارد)
1. [آزمایش کردن (testing)](#آزمایش-کردن-Testing)
1. [کارایی (performance)](#کارایی-Performance)
1. [منابع](#منابع)
1. [در دنیای واقعی](#در-دنیای-واقعی)
1. [ترجمه](#ترجمه)
1. [راهنمای راهنمای سبک جاوااسکریپت](#راهنمای-راهنمای-سبک-جاوااسکریپت)
1. [با ما درباره جاوااسکریپت گپ بزنید](#با-ما-درباره-جاوااسکریپت-گپ-بزنید)
1. [همکاران (contributors)](#همکاران-Contributors)
1. [مجوز](#مجوز)
1. [اصلاحیه ها](#اصلاحیه-ها)


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
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) اگر مجبورید ارجاع‌ها را دوباره انتساب دهید، به‌جای `var` از `let` استفاده کنید. eslint: [`no-var`](https://eslint.org/docs/rules/no-var)

    > چرا؟ `let` دامنهٔ بلوکی دارد، نه دامنهٔ تابعی مثل `var`.

    ```javascript
    // bad
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
    // bad
    const item = new Object();

    // good
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
    // bad
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // good
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
    // bad
    const bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };

    // good
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
    // bad
    console.log(object.hasOwnProperty(key));

    // good
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    // better
    const has = Object.prototype.hasOwnProperty; // جستجو را یک بار، در دامنه ماژول کش کنید.
    console.log(has.call(object, key));

    // best
    console.log(Object.hasOwn(object, key)); // فقط در مرورگرهایی که از ES2022 پشتیبانی می‌کنند، پشتیبانی می‌شود

    /* or */
    import has from 'has'; // https://www.npmjs.com/package/has
    console.log(has(object, key));
    /* or */
    console.log(Object.hasOwn(object, key)); // https://www.npmjs.com/package/object.hasown
    ```

  <a name="objects--rest-spread"></a>
  - [3.8](#objects--rest-spread) برای کپی سطحی (shallow-copy) کردن شئ‌ها، به جای [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) از سینتکس spread شئ‌ها استفاده کنید. برای به دست آوردن یک شئ جدید با حذف شدن برخی ویژگی‌ها، از سینتکس پارامتر rest شئ‌ها استفاده کنید. eslint: [`prefer-object-spread`](https://eslint.org/docs/rules/prefer-object-spread)

    ```javascript
    // very bad
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); // این کار `original` را تغییر می‌دهد ಠ_ಠ
    delete copy.a; // این هم همینطور

    // bad
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // good
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## آرایه ها

  <a name="arrays--literals"></a><a name="4.1"></a>
  - [4.1](#arrays--literals) برای ساخت آرایه‌ها از ساختار دقیق (literal syntax) استفاده کنید. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor)

    ```javascript
    // bad
    const items = new Array();

    // good
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
    // bad
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // good
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
    // bad
    const baz = [...foo].map(bar);

    // good
    const baz = Array.from(foo, bar);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.7](#arrays--callback-return) در توابع کال‌بک (callback) متدهای آرایه، از دستور `return` استفاده کنید. اگر بدنهٔ تابع از یک دستور واحد تشکیل شده باشد که یک عبارت بدون اثرات جانبی را برمی‌گرداند، طبق قانون [8.2](#arrows--implicit-return) حذف کردن `return` مشکلی ندارد. eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)

    ```javascript
    // good - خوب
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
    // bad
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

    // good
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
    // bad
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // good
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // best
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
    // bad - بد
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
    // bad - بد
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
    // bad
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // bad
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // good
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals"></a><a name="6.4"></a>
  - [6.3](#es6-template-literals) هنگام ساخت رشته‌ها به صورت برنامه‌نویسی‌شده، به جای الحاق از رشته‌های قالبی (template strings) استفاده کنید. eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

    > چرا؟ رشته‌های قالبی سینتکسی خوانا و مختصر با قابلیت‌های خطوط جدید مناسب و درج متغیر به شما می‌دهند.

    ```javascript
    // bad
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // bad
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // bad
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // good
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
    // bad
    const foo = '\'this\' \i\s \"quoted\"';

    // good
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## توابع

  <a name="functions--declarations"></a><a name="7.1"></a>
  - [7.1](#functions--declarations) به جای اعلان توابع (function declarations)، از عبارات توابعِ نام‌گذاری‌شده (named function expressions) استفاده کنید. eslint: [`func-style`](https://eslint.org/docs/rules/func-style), [`func-names`](https://eslint.org/docs/latest/rules/func-names)

    > چرا؟ اعلان توابع بالا آورده می‌شوند (hoisted)، به این معنی که ارجاع به تابع قبل از تعریف آن در فایل، بسیار آسان است - بیش از حد آسان. این کار به خوانایی و قابلیت نگهداری آسیب می‌زند. اگر متوجه شدید که تعریف یک تابع به قدری بزرگ یا پیچیده است که در درک بقیه فایل اختلال ایجاد می‌کند، شاید زمان آن رسیده که آن را در ماژول جداگانه‌ای استخراج کنید! فراموش نکنید که نام عبارت را صریحاً مشخص کنید، صرف نظر از اینکه آیا نام از متغیر نگهدارنده‌اش استخراج می‌شود یا خیر (که اغلب در مرورگرهای مدرن یا هنگام استفاده از کامپایلرهایی مانند Babel اینطور است). این کار هرگونه فرضیاتی را که درباره پشته فراخوانی (call stack) خطا (Error) وجود دارد، از بین می‌برد. ([بحث](https://github.com/airbnb/javascript/issues/794))

    ```javascript
    // bad - بد
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
    // IIFE - عبارت تابع بلافاصله فراخوانی‌شده
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks"></a><a name="7.3"></a>
  - [7.3](#functions--in-blocks) هرگز تابعی را در یک بلوک غیرتابعی (مثل `if`، `while` و غیره) اعلان نکنید. در عوض، تابع را به یک متغیر انتساب دهید. مرورگرها به شما اجازه می‌دهند این کار را انجام دهید، اما همگی آن را به شکل متفاوتی تفسیر می‌کنند که خبر بدی است. eslint: [`no-loop-func`](https://eslint.org/docs/rules/no-loop-func)

  <a name="functions--note-on-blocks"></a><a name="7.4"></a>
  - [7.4](#functions--note-on-blocks) **نکته:** ECMA-262 یک بلوک را به عنوان فهرستی از دستورات (statements) تعریف می‌کند. اعلان تابع (function declaration) یک دستور نیست.

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
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
    // bad
    function foo(name, options, arguments) {
      // ...
    }

    // good
    function foo(name, options, args) {
      // ...
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  - [7.6](#es6-rest) هرگز از `arguments` استفاده نکنید، در عوض از سینتکس rest یعنی `...` استفاده کنید. eslint: [`prefer-rest-params`](https://eslint.org/docs/rules/prefer-rest-params)

    > چرا؟ `...` صریحاً مشخص می‌کند که کدام آرگومان‌ها را می‌خواهید استخراج کنید. علاوه بر این، آرگومان‌های rest یک آرایه واقعی هستند، نه فقط شبیه به آرایه (مانند `arguments`).

    ```javascript
    // bad
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // good
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  - [7.7](#es6-default-parameters) به جای تغییر آرگومان‌های تابع، از سینتکس پارامترهای پیش‌فرض استفاده کنید.

    ```javascript
    // very bad - خیلی بد
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
    // bad
    function handleThings(opts = {}, name) {
      // ...
    }

    // good
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  - [7.10](#functions--constructor) برای ساخت یک تابع جدید، هرگز از سازنده Function استفاده نکنید. eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

    > چرا؟ ایجاد تابع به این روش، رشته‌ای را به شکلی مشابه `eval()` ارزیابی می‌کند که باعث ایجاد آسیب‌پذیری می‌شود.

    ```javascript
    // bad
    const add = new Function('a', 'b', 'return a + b');

    // still bad - هنوز هم بد
    const subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) فاصله‌گذاری در امضای یک تابع. eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    > چرا؟ یکپارچگی خوب است و شما نباید هنگام اضافه یا حذف کردن یک نام، مجبور به اضافه یا حذف کردن فاصله باشید.

    ```javascript
    // bad
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // good
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  - [7.12](#functions--mutate-params) هرگز پارامترها را دستخوش تغییر (mutate) نکنید. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign)

    > چرا؟ دستکاری اشیایی که به عنوان پارامتر پاس داده شده‌اند، می‌تواند باعث ایجاد اثرات جانبی ناخواسته متغیر در فراخواننده اصلی شود.

    ```javascript
    // bad
    function f1(obj) {
      obj.key = 1;
    }

    // good
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  - [7.13](#functions--reassign-params) هرگز پارامترها را مجدداً انتساب ندهید. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign)

    > چرا؟ انتساب مجدد پارامترها می‌تواند منجر به رفتارهای غیرمنتظره شود، به ویژه هنگام دسترسی به شئ `arguments`. همچنین می‌تواند مشکلاتی در بهینه‌سازی ایجاد کند، به خصوص در V8.

    ```javascript
    // bad
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // good
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
    // bad
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // good
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // bad
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // good
    new Date(...[2016, 8, 5]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  - [7.15](#functions--signature-invocation-indentation) توابعی که امضا (signature) یا فراخوانی (invocation) چند خطی دارند، باید دقیقاً مانند هر فهرست چند خطی دیگری در این راهنما تورفتگی (indent) داشته باشند: با قرار گرفتن هر آیتم در یک خط مجزا، همراه با یک ویرگول انتهایی (trailing comma) در آخرین آیتم. eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)

    ```javascript
    // bad
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    // good
    function foo(
      bar,
      baz,
      quux,
    ) {
      // ...
    }

    // bad
    console.log(foo,
      bar,
      baz);

    // good
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
    // bad
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--implicit-return"></a><a name="8.2"></a>
  - [8.2](#arrows--implicit-return) اگر بدنهٔ تابع از یک دستور واحد تشکیل شده باشد که یک [عبارت](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) بدون اثرات جانبی را برمی‌گرداند، آکولادها را حذف کرده و از بازگشت ضمنی (implicit return) استفاده کنید. در غیر این صورت، آکولادها را نگه دارید و از دستور `return` استفاده کنید. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens), [`arrow-body-style`](https://eslint.org/docs/rules/arrow-body-style)

    > چرا؟ راه را هموار کردن (Syntactic sugar). هنگامی که چند تابع به هم زنجیر می‌شوند، خوانایی خوبی دارد.

    ```javascript
    // bad - بد
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
    // bad
    ['get', 'post', 'put'].map((httpMethod) => Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    );

    // good
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
    // bad
    [1, 2, 3].map(x => x * x);

    // good
    [1, 2, 3].map((x) => x * x);

    // bad
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // good
    [1, 2, 3].map((number) => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // bad
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });

    // good
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--confusing"></a><a name="8.5"></a>
  - [8.5](#arrows--confusing) از اشتباه گرفتن سینتکس تابع پیکانی (`=>`) با عملگرهای مقایسه‌ای (`<=`، `>=`) اجتناب کنید. eslint: [`no-confusing-arrow`](https://eslint.org/docs/rules/no-confusing-arrow)

    ```javascript
    // bad
    const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

    // bad
    const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

    // good
    const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

    // good
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height <= 256 ? largeSize : smallSize;
    };
    ```

  <a name="whitespace--implicit-arrow-linebreak"></a>
  - [8.6](#whitespace--implicit-arrow-linebreak) مکان بدنهٔ توابع پیکانی که دارای بازگشت ضمنی هستند را یکسان نگه دارید. eslint: [`implicit-arrow-linebreak`](https://eslint.org/docs/rules/implicit-arrow-linebreak)

    ```javascript
    // bad
    (foo) =>
      bar;

    (foo) =>
      (bar);

    // good
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
    // bad
    function Queue(contents = []) {
      this.queue = [...contents];
    }
    Queue.prototype.pop = function () {
      const value = this.queue[0];
      this.queue.splice(0, 1);
      return value;
    };

    // good
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
    // bad
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function () {
      return this.queue[0];
    };

    // good
    class PeekableQueue extends Queue {
      peek() {
        return this.queue[0];
      }
    }
    ```

  <a name="constructors--chaining"></a><a name="9.3"></a>
  - [9.3](#constructors--chaining) متدها می‌توانند `this` را برگردانند تا به زنجیره‌سازی متدها (method chaining) کمک کنند.

    ```javascript
    // bad
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

    // good
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
    // bad
    class Jedi {
      constructor() {}

      getName() {
        return this.name;
      }
    }

    // bad
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
      }
    }

    // good
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
    // bad
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // good
    class Foo {
      bar() { return 1; }
    }

    // good
    class Foo {
      bar() { return 2; }
    }
    ```

  <a name="classes--methods-use-this"></a>
  - [9.7](#classes--methods-use-this) متدهای کلاس باید از `this` استفاده کنند یا به یک متد استاتیک (static) تبدیل شوند، مگر اینکه یک کتابخانه یا فریم‌ورک خارجی، استفاده از متدهای خاصِ غیراستاتیک را ایجاب کند. بودنِ یک متدِ نمونه (instance method) باید نشان‌دهنده این باشد که رفتار آن بر اساس ویژگی‌های گیرنده (receiver) متفاوت است. eslint: [`class-methods-use-this`](https://eslint.org/docs/rules/class-methods-use-this)

    ```javascript
    // bad - بد
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
    // bad - بد
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
    // bad
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // good
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  <a name="modules--no-export-from-import"></a><a name="10.3"></a>
  - [10.3](#modules--no-export-from-import) و مستقیماً از یک import، export نگیرید.

    > چرا؟ هرچند نوشتن آن در یک خط مختصر است، اما داشتن یک راه مشخص برای وارد کردن و یک راه مشخص برای صادر کردن، باعث یکپارچگی می‌شود.

    ```javascript
    // bad
    // filename es6.js
    export { es6 as default } from './AirbnbStyleGuide';

    // good
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-duplicate-imports"></a>
  - [10.4](#modules--no-duplicate-imports) فقط از یک مسیر را در یک مکان وارد کنید.
  eslint: [`no-duplicate-imports`](https://eslint.org/docs/rules/no-duplicate-imports)
    > چرا؟ داشتن چندین خط که از یک مسیر یکسان وارد می‌کنند، می‌تواند حفظ و نگهداری کد را سخت‌تر کند.

    ```javascript
    // bad
    import foo from 'foo';
    // … some other imports … //
    import { named1, named2 } from 'foo';

    // good
    import foo, { named1, named2 } from 'foo';

    // good
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
    // bad
    let foo = 3;
    export { foo };

    // good
    const foo = 3;
    export { foo };
    ```

  <a name="modules--prefer-default-export"></a>
  - [10.6](#modules--prefer-default-export) در ماژول‌هایی با تنها یک خروجی، خروجی پیش‌فرض (default export) را به خروجی نام‌گذاری‌شده (named export) ترجیح دهید.
  eslint: [`import/prefer-default-export`](https://github.com/import-js/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)
    > چرا؟ برای تشویق فایل‌های بیشتری که فقط یک چیز را صادر می‌کنند، که برای خوانایی و قابلیت نگهداری بهتر است.

    ```javascript
    // bad
    export function foo() {}

    // good
    export default function foo() {}
    ```

  <a name="modules--imports-first"></a>
  - [10.7](#modules--imports-first) تمام `import`ها را بالاتر از دستورات غیرِ وارداتی قرار دهید.
  eslint: [`import/first`](https://github.com/import-js/eslint-plugin-import/blob/master/docs/rules/first.md)
    > چرا؟ از آنجایی که `import`ها بالا آورده می‌شوند (hoisted)، نگه داشتن همه آن‌ها در بالا از رفتارهای غیرمنتظره جلوگیری می‌کند.

    ```javascript
    // bad
    import foo from 'foo';
    foo.init();

    import bar from 'bar';

    // good
    import foo from 'foo';
    import bar from 'bar';

    foo.init();
    ```

  <a name="modules--multiline-imports-over-newlines"></a>
  - [10.8](#modules--multiline-imports-over-newlines) واردات چندخطی باید دقیقاً مانند لیترال‌های چندخطی آرایه و شئ، فاصله گذاری (indent) داشته باشند.
  eslint: [`object-curly-newline`](https://eslint.org/docs/rules/object-curly-newline)

    > چرا؟ آکولادها از همان قوانین فاصله گذاری پیروی می‌کنند که هر بلوک آکولاد دیگری در این راهنما دارد، و ویرگول‌های انتهایی (trailing commas) نیز همینطور.

    ```javascript
    // bad
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

    // good
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
    // bad
    import fooSass from 'css!sass!foo.scss';
    import barCss from 'style!css!bar.css';

    // good
    import fooSass from 'foo.scss';
    import barCss from 'bar.css';
    ```

  <a name="modules--import-extensions"></a>
  - [10.10](#modules--import-extensions) پسوندهای نام فایل جاوااسکریپت را لحاظ نکنید.
  eslint: [`import/extensions`](https://github.com/import-js/eslint-plugin-import/blob/master/docs/rules/extensions.md)
    > چرا؟ لحاظ کردن پسوندها، بازنویسی کد (refactoring) را محدود می‌کند و جزئیات پیاده‌سازی ماژولی که در حال وارد کردن آن هستید را به صورت نامناسبی در هر مصرف‌کننده، هاردکد (سخت‌کد) می‌کند.

    ```javascript
    // bad
    import foo from './foo.js';
    import bar from './bar.jsx';
    import baz from './baz/index.jsx';

    // good
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
    // bad - بد
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
    // bad
    const binary = Math.pow(2, 10);

    // good
    const binary = 2 ** 10;
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## متغیر ها

  <a name="variables--const"></a><a name="13.1"></a>
  - [13.1](#variables--const) همیشه برای اعلان متغیرها از `const` یا `let` استفاده کنید. عدم انجام این کار منجر به ایجاد متغیرهای سراسری (global) می‌شود. ما می‌خواهیم از آلوده کردن فضای نام سراسری جلوگیری کنیم. کاپیتان پلنت به ما در این باره هشدار داده بود. eslint: [`no-undef`](https://eslint.org/docs/rules/no-undef) [`prefer-const`](https://eslint.org/docs/rules/prefer-const)

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const"></a><a name="13.2"></a>
  - [13.2](#variables--one-const) برای هر متغیر یا انتساب، از یک اعلان `const` یا `let` مجزا استفاده کنید. eslint: [`one-var`](https://eslint.org/docs/rules/one-var)

    > چرا؟ این روش اضافه کردن اعلان‌های متغیر جدید را آسان‌تر می‌کند، و دیگر نیازی نیست نگران جایگزینی `;` با `,` یا ایجاد تفاوت ها (diff) فقط نقطه‌گذاری باشید. همچنین می‌توانید با دیباگر (debugger) هر اعلان را مرحله به مرحله پیش بروید، به جای اینکه همه را به یکباره رد شوید.

    ```javascript
    // bad - بد
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
    // bad
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // good
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
    // bad - بد - فراخوانی تابع غیرضروری
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
    // bad - بد
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
    // bad

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

    // good

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
    // bad
    const foo =
      superLongLongLongLongLongLongLongLongFunctionName();

    // bad
    const foo
      = 'superLongLongLongLongLongLongLongLongString';

    // good
    const foo = (
      superLongLongLongLongLongLongLongLongFunctionName()
    );

    // good
    const foo = 'superLongLongLongLongLongLongLongLongString';
    ```

  <a name="variables--no-unused-vars"></a>
  - [13.8](#variables--no-unused-vars) متغیرهای استفاده‌نشده را ممنوع کنید. eslint: [`no-unused-vars`](https://eslint.org/docs/rules/no-unused-vars)

    > چرا؟ متغیرهایی که اعلان می‌شوند و هیچ‌جایی در کد استفاده نمی‌شوند، احتمالاً به دلیل بازنویسی ناقص (refactoring) یک خطا هستند. چنین متغیرهایی فضا اشغال می‌کنند و می‌توانند باعث سردرگمی خوانندگان شوند.

    ```javascript
    // bad - بد

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
    // this won't work - می‌دانیم که این کار نمی‌کند
    // (با فرض اینکه متغیر سراسری notDefined وجود ندارد)
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
    // bad - بد

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

## عملگرهای مقایسه و برابری

  <a name="comparison--eqeqeq"></a><a name="15.1"></a>
  - [15.1](#comparison--eqeqeq) به جای `==` و `!=` از `===` و `!==` استفاده کنید. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq)

  <a name="comparison--if"></a><a name="15.2"></a>
  - [15.2](#comparison--if) دستورهای شرطی مانند دستور `if` عبارت خود را با استفاده از تبدیل (coercion) از طریق متد انتزاعی `ToBoolean` ارزیابی می‌کنند و همیشه این قوانین ساده را دنبال می‌کنند:

    - **اشیاء (Objects)** به **true** ارزیابی می‌شوند
    - **مقدار Undefined** به **false** ارزیابی می‌شود
    - **مقدار Null** به **false** ارزیابی می‌شود
    - **بولین‌ها (Booleans)** به **مقدار خودِ بولین** ارزیابی می‌شوند
    - **اعداد (Numbers)** در صورتی که **+0، -0 یا NaN** باشند به **false** ارزیابی می‌شوند، در غیر این صورت **true**
    - **رشته‌ها (Strings)** در صورتی که رشته خالی `''` باشند به **false** ارزیابی می‌شوند، در غیر این صورت **true**

    ```javascript
    if ([0] && []) {
      // true
      // یک آرایه (حتی آرایه خالی) یک شئ است، و اشیاء به true ارزیابی می‌شوند
    }
    ```

  <a name="comparison--shortcuts"></a><a name="15.3"></a>
  - [15.3](#comparison--shortcuts) برای بولین‌ها از میان‌برها، اما برای رشته‌ها و اعداد از مقایسه‌های صریح استفاده کنید.

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
  - [15.4](#comparison--moreinfo) برای اطلاعات بیشتر به مرجع [حقیقت، برابری و جاوااسکریپت (Truth, Equality, and JavaScript)](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) اثر آنگوس کرول (Angus Croll) مراجعه کنید.

  <a name="comparison--switch-blocks"></a><a name="15.5"></a>
  - [15.5](#comparison--switch-blocks) برای ایجاد بلوک در بندهای `case` و `default` که حاوی اعلان‌های لغوی (مانند `let`، `const`، `function` و `class`) هستند، از آکولاد استفاده کنید. eslint: [`no-case-declarations`](https://eslint.org/docs/rules/no-case-declarations)

    > چرا؟ اعلان‌های لغوی در کل بلوک `switch` قابل مشاهده هستند اما تنها زمانی مقداردهی اولیه می‌شوند که انتساب داده شوند، که این اتفاق فقط زمانی می‌افتد که به `case` مربوطه برسید. این موضوع زمانی که چندین بند `case` سعی می‌کنند یک چیز واحد را تعریف کنند، باعث ایجاد مشکل می‌شود.

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
  - [15.6](#comparison--nested-ternaries) سه‌تایی‌ها (Ternaries) نباید تودرتو باشند و به طور کلی باید عبارات تک‌خطی باشند. eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary)

    ```javascript
    // bad - بد
    const foo = maybe1 > maybe2
      ? 'bar'
      : value1 > value2 ? 'baz' : null;

    // تقسیم به 2 عبارت سه‌تایی مجزا
    const maybeNull = value1 > value2 ? 'baz' : null;

    // بهتر
    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // بهترین
    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary"></a><a name="15.7"></a>
  - [15.7](#comparison--unneeded-ternary) از دستورات سه‌تایی غیرضروری اجتناب کنید. eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary)

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
  - [15.8](#comparison--no-mixed-operators) هنگام ترکیب عملگرها، آن‌ها را داخل پرانتز قرار دهید. تنها استثنا عملگرهای ریاضی استاندارد: `+`، `-` و `**` هستند، زیرا اولویت آن‌ها به طور گسترده درک شده است. ما توصیه می‌کنیم `/` و `*` را داخل پرانتز قرار دهید زیرا اولویت آن‌ها هنگام ترکیب می‌تواند مبهم باشد.
  eslint: [`no-mixed-operators`](https://eslint.org/docs/rules/no-mixed-operators)

    > چرا؟ این کار خوانایی را بهبود می‌بخشد و قصد توسعه‌دهنده را روشن می‌کند.

    ```javascript
    // bad - بد
    const foo = a && b < 0 || c > 0 || d + 1 === 0;

    // بد
    const bar = a ** b - 5 % d;

    // بد
    // ممکن است فرد فکر کند (a || b) && c است
    if (a || b && c) {
      return d;
    }

    // بد
    const bar = a + b / c * d;

    // خوب
    const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

    // خوب
    const bar = a ** b - (5 % d);

    // خوب
    if (a || (b && c)) {
      return d;
    }

    // خوب
    const bar = a + (b / c) * d;
    ```

  <a name="nullish-coalescing-operator"></a>
  - [15.9](#nullish-coalescing-operator) عملگر ادغام تهی (nullish coalescing operator - `??`) یک عملگر منطقی است که در صورتی که عملوند سمت چپ آن `null` یا `undefined` باشد، عملوند سمت راست را برمی‌گرداند. در غیر این صورت، عملوند سمت چپ را برمی‌گرداند.

    > چرا؟ با متمایز کردن null/undefined از سایر مقادیر falsy، دقت را فراهم می‌کند و وضوح و پیش‌بینی‌پذیری کد را افزایش می‌دهد.

    ```javascript
    // bad - بد
    const value = 0 ?? 'default';
    // 0 را برمی‌گرداند، نه 'default'

    // بد
    const value = '' ?? 'default';
    // '' را برمی‌گرداند، نه 'default'

    // خوب
    const value = null ?? 'default';
    // 'default' را برمی‌گرداند

    // خوب
    const user = {
      name: 'John',
      age: null
    };
    const age = user.age ?? 18;
    // 18 را برمی‌گرداند
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## بلوک ها

  <a name="blocks--braces"></a><a name="16.1"></a>
  - [16.1](#blocks--braces) در تمام بلوک‌های چندخطی از آکولاد استفاده کنید. eslint: [`nonblock-statement-body-position`](https://eslint.org/docs/rules/nonblock-statement-body-position)

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
  - [16.2](#blocks--cuddled-elses) اگر از بلوک‌های چندخطی با `if` و `else` استفاده می‌کنید، `else` را در همان خطی قرار دهید که آکولاد بسته‌شده‌ی بلوک `if` قرار دارد. eslint: [`brace-style`](https://eslint.org/docs/rules/brace-style)

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
  - [16.3](#blocks--no-else-return) اگر یک بلوک `if` همیشه یک دستور `return` را اجرا می‌کند، بلوک `else` بعدی غیرضروری است. یک `return` در یک بلوک `else if` که بعد از یک بلوک `if` حاوی `return` می‌آید، می‌تواند به چندین بلوک `if` جداگانه تقسیم شود. eslint: [`no-else-return`](https://eslint.org/docs/rules/no-else-return)

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

## دستورهای کنترلی

  <a name="control-statements"></a>
  - [17.1](#control-statements) در صورتی که دستور کنترلی شما (`if`، `while` و غیره) بیش از حد طولانی شد یا از حداکثر طول خط فراتر رفت، می‌توان هر شرط (یا گروهی از شروط) را در یک خط جدید قرار داد. عملگر منطقی باید در ابتدای خط قرار گیرد.

    > چرا؟ الزام به قرار دادن عملگرها در ابتدای خط، باعث می‌شود عملگرها تراز شده باقی بمانند و از الگویی مشابه زنجیره‌سازی متدها پیروی کند. این کار همچنین با راحت‌تر کردن پیگیری بصری منطق پیچیده، خوانایی را بهبود می‌بخشد.

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
  - [17.2](#control-statements--value-selection) از عملگرهای انتخابی (selection operators) به جای دستورهای کنترلی استفاده نکنید.

    ```javascript
    // bad
    !isRunning && startRunning();

    // good
    if (!isRunning) {
      startRunning();
    }
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## توضیحات (Comments)

  <a name="comments--multiline"></a><a name="17.1"></a>
  - [18.1](#comments--multiline) برای توضیحات چندخطی از `/** ... */` استفاده کنید.

    ```javascript
    // bad - بد
    // make() یک المان جدید بر اساس
    // نام تگ پاس داده شده برمی‌گرداند
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...

      return element;
    }

    // خوب
    /**
     * make() یک المان جدید بر اساس
     * نام تگ پاس داده شده برمی‌گرداند
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--singleline"></a><a name="17.2"></a>
  - [18.2](#comments--singleline) برای توضیحات تک‌خطی از `//` استفاده کنید. توضیحات تک‌خطی را در یک خط جدید، بالای موضوعِ توضیح قرار دهید. مگر اینکه توضیح در خط اول یک بلوک باشد، یک خط خالی قبل از آن قرار دهید.

    ```javascript
    // bad - بد
    const active = true;  // تب جاری است

    // خوب
    // تب جاری است
    const active = true;

    // بد
    function getType() {
      console.log('fetching type...');
      // نوع پیش‌فرض را روی 'no type' تنظیم کنید
      const type = this.type || 'no type';

      return type;
    }

    // خوب
    function getType() {
      console.log('fetching type...');

      // نوع پیش‌فرض را روی 'no type' تنظیم کنید
      const type = this.type || 'no type';

      return type;
    }

    // همچنین خوب است
    function getType() {
      // نوع پیش‌فرض را روی 'no type' تنظیم کنید
      const type = this.type || 'no type';

      return type;
    }
    ```

  <a name="comments--spaces"></a>
  - [18.3](#comments--spaces) برای خوانایی بهتر، تمام توضیحات را با یک فاصله شروع کنید. eslint: [`spaced-comment`](https://eslint.org/docs/rules/spaced-comment)

    ```javascript
    // bad - بد
    //تب جاری است
    const active = true;

    // خوب
    // تب جاری است
    const active = true;

    // بد
    /**
     *make() یک المان جدید بر اساس
     *نام تگ پاس داده شده برمی‌گرداند
     */
    function make(tag) {

      // ...

      return element;
    }

    // خوب
    /**
     * make() یک المان جدید بر اساس
     * نام تگ پاس داده شده برمی‌گرداند
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--actionitems"></a><a name="17.3"></a>
  - [18.4](#comments--actionitems) قرار دادن پیشوند `FIXME` یا `TODO` قبل از توضیحات به توسعه‌دهندگان دیگر کمک می‌کند تا به سرعت بفهمند که آیا شما به مشکلی اشاره می‌کنید که نیاز به بررسی مجدد دارد، یا آیا راه حلی برای مشکلی پیشنهاد می‌دهید که نیاز به پیاده‌سازی دارد. این موارد با توضیحات معمولی متفاوت هستند زیرا قابل اجرا (actionable) هستند. این اقدامات به شکل `FIXME: -- باید این مورد را بررسی کرد` یا `TODO: -- نیاز به پیاده‌سازی دارد` هستند.

  <a name="comments--fixme"></a><a name="17.4"></a>
  - [18.5](#comments--fixme) برای نشانه‌گذاری مشکلات از `// FIXME:` استفاده کنید.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: نباید از یک متغیر سراسری اینجا استفاده شود
        total = 0;
      }
    }
    ```

  <a name="comments--todo"></a><a name="17.5"></a>
  - [18.6](#comments--todo) برای نشانه‌گذاری راه‌حل مشکلات از `// TODO:` استفاده کنید.

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: مقدار total باید توسط یک پارامتر options قابل پیکربندی باشد
        this.total = 0;
      }
    }
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## فاصله گذاری

  <a name="whitespace--spaces"></a><a name="18.1"></a>
  - [19.1](#whitespace--spaces) از تب‌های نرم (کاراکتر فاصله) تنظیم‌شده روی ۲ فاصله استفاده کنید. eslint: [`indent`](https://eslint.org/docs/rules/indent)

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
  - [19.2](#whitespace--before-blocks) قبل از آکولادِ شروع، ۱ فاصله قرار دهید. eslint: [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

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
  - [19.3](#whitespace--around-keywords) قبل از پرانتز بازِ دستورهای کنترلی (`if`، `while` و غیره) ۱ فاصله قرار دهید. بین لیست آرگومان‌ها و نام تابع در فراخوانی‌ها و اعلان‌های توابع، فاصله‌ای قرار ندهید. eslint: [`keyword-spacing`](https://eslint.org/docs/rules/keyword-spacing)

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
  - [19.4](#whitespace--infix-ops) اطراف عملگرها فاصله قرار دهید. eslint: [`space-infix-ops`](https://eslint.org/docs/rules/space-infix-ops)

    ```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
    ```

  <a name="whitespace--newline-at-end"></a><a name="18.5"></a>
  - [19.5](#whitespace--newline-at-end) فایل‌ها را با یک کاراکتر خط جدید (newline) به پایان برسانید. eslint: [`eol-last`](https://eslint.org/docs/rules/eol-last)

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
  - [19.6](#whitespace--chains) هنگام ایجاد زنجیره‌های طولانیِ متد (بیش از ۲ زنجیره متد)، از فاصله گذاری (indent) استفاده کنید. از نقطه ابتدایی (leading dot) استفاده کنید، که تأکید می‌کند این خط یک فراخوانی متد است، نه یک دستور جدید. eslint: [`newline-per-chained-call`](https://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](https://eslint.org/docs/rules/no-whitespace-before-property)

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
  - [19.7](#whitespace--after-blocks) بعد از بلوک‌ها و قبل از دستور بعدی، یک خط خالی بگذارید.

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
  - [19.8](#whitespace--padded-blocks) بلوک‌های خود را با خطوط خالی پد (pad - پُر) نکنید. eslint: [`padded-blocks`](https://eslint.org/docs/rules/padded-blocks)

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
  - [19.9](#whitespace--no-multiple-blanks) برای پد (پُر) کردن کد خود از چندین خط خالی استفاده نکنید. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

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
  - [19.10](#whitespace--in-parens) داخل پرانتزها فاصله اضافه نکنید. eslint: [`space-in-parens`](https://eslint.org/docs/rules/space-in-parens)

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
  - [19.11](#whitespace--in-brackets) داخل براکت‌ها فاصله اضافه نکنید. eslint: [`array-bracket-spacing`](https://eslint.org/docs/rules/array-bracket-spacing)

    ```javascript
    // bad
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // good
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  <a name="whitespace--in-braces"></a><a name="18.11"></a>
  - [19.12](#whitespace--in-braces) داخل آکولادها فاصله اضافه کنید. eslint: [`object-curly-spacing`](https://eslint.org/docs/rules/object-curly-spacing)

    ```javascript
    // bad
    const foo = {clark: 'kent'};

    // good
    const foo = { clark: 'kent' };
    ```

  <a name="whitespace--max-len"></a><a name="18.12"></a>
  - [19.13](#whitespace--max-len) از داشتن خطوط کد طولانی‌تر از ۱۰۰ کاراکتر (شامل فاصله‌ها) خودداری کنید. توجه: بر اساس [بخش بالا](#strings--line-length)، رشته‌های طولانی از این قانون مستثنی هستند و نباید شکسته شوند. eslint: [`max-len`](https://eslint.org/docs/rules/max-len)

    > چرا؟ این کار خوانایی و قابلیت نگهداری را تضمین می‌کند.

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
  - [19.14](#whitespace--block-spacing) فاصله‌گذاری یکپارچه را داخل توکنِ بلوکِ باز و توکن بعدی در همان خط الزامی کنید. این قانون همچنین فاصله‌گذاری یکپارچه را داخل توکنِ بلوکِ بسته و توکن قبلی در همان خط اعمال می‌کند. eslint: [`block-spacing`](https://eslint.org/docs/rules/block-spacing)

    ```javascript
    // bad
    function foo() {return true;}
    if (foo) { bar = 0;}

    // good
    function foo() { return true; }
    if (foo) { bar = 0; }
    ```

  <a name="whitespace--comma-spacing"></a>
  - [19.15](#whitespace--comma-spacing) از فاصله قبل از ویرگول‌ها خودداری کنید و یک فاصله بعد از ویرگول‌ها الزامی کنید. eslint: [`comma-spacing`](https://eslint.org/docs/rules/comma-spacing)

    ```javascript
    // bad
    const foo = 1,bar = 2;
    const arr = [1 , 2];

    // good
    const foo = 1, bar = 2;
    const arr = [1, 2];
    ```

  <a name="whitespace--computed-property-spacing"></a>
  - [19.16](#whitespace--computed-property-spacing) فاصله‌گذاری داخل براکت‌های ویژگی محاسبه‌شده (computed property) را اعمال کنید. eslint: [`computed-property-spacing`](https://eslint.org/docs/rules/computed-property-spacing)

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
  - [19.17](#whitespace--func-call-spacing) بین توابع و فراخوانی‌های آن‌ها فاصله‌ای قرار ندهید. eslint: [`func-call-spacing`](https://eslint.org/docs/rules/func-call-spacing)

    ```javascript
    // bad
    func ();

    func
    ();

    // good
    func();
    ```

  <a name="whitespace--key-spacing"></a>
  - [19.18](#whitespace--key-spacing) فاصله‌گذاری بین کلیدها و مقادیر در ویژگی‌های لیترالِ شئ را اعمال کنید. eslint: [`key-spacing`](https://eslint.org/docs/rules/key-spacing)

    ```javascript
    // bad
    const obj = { foo : 42 };
    const obj2 = { foo:42 };

    // good
    const obj = { foo: 42 };
    ```

  <a name="whitespace--no-trailing-spaces"></a>
  - [19.19](#whitespace--no-trailing-spaces) از فاصله‌های پشت سرهم (trailing spaces) در انتهای خطوط خودداری کنید. eslint: [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces)

  <a name="whitespace--no-multiple-empty-lines"></a>
  - [19.20](#whitespace--no-multiple-empty-lines) از چندین خط خالی خودداری کنید، فقط اجازه دهید یک خط جدید در انتهای فایل وجود داشته باشد، و از خط جدید در ابتدای فایل‌ها اجتناب کنید. eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines)

    <!-- markdownlint-disable MD012 -->
    ```javascript
    // bad - بد - چندین خط خالی
    const x = 1;


    const y = 2;

    // بد - 2+ خط جدید در انتهای فایل
    const x = 1;
    const y = 2;


    // بد - 1+ خط(های) جدید در ابتدای فایل

    const x = 1;
    const y = 2;

    // خوب
    const x = 1;
    const y = 2;

    ```
    <!-- markdownlint-enable MD012 -->

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## ویرگول ها

  <a name="commas--leading-trailing"></a><a name="19.1"></a>
  - [20.1](#commas--leading-trailing) ویرگول‌های ابتدایی: **نخیر.** eslint: [`comma-style`](https://eslint.org/docs/rules/comma-style)

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
  - [20.2](#commas--dangling) ویرگول انتهایی اضافه کردن: **بله.** eslint: [`comma-dangle`](https://eslint.org/docs/rules/comma-dangle)

    > چرا؟ این کار منجر به تمیزتر شدن تفاوت‌های گیت (git diffs) می‌شود. همچنین ترنسپایلرهایی مانند Babel، ویرگول انتهایی اضافی را در کد ترنسپایل شده حذف می‌کنند که به این معنی است که نیازی نیست نگران [مشکل ویرگول انتهایی](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas) در مرورگرهای قدیمی باشید.

    ```diff
    // بد - git diff بدون ویرگول انتهایی
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    // خوب - git diff با ویرگول انتهایی
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };
    ```

    ```javascript
    // bad - بد
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // خوب
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];

    // بد
    function createHero(
      firstName,
      lastName,
      inventorOf
    ) {
      // کاری انجام نمی‌دهد
    }

    // خوب
    function createHero(
      firstName,
      lastName,
      inventorOf,
    ) {
      // کاری انجام نمی‌دهد
    }

    // خوب (توجه کنید که ویرگول نباید بعد از یک عنصر "rest" ظاهر شود)
    function createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    ) {
      // کاری انجام نمی‌دهد
    }

    // بد
    createHero(
      firstName,
      lastName,
      inventorOf
    );

    // خوب
    createHero(
      firstName,
      lastName,
      inventorOf,
    );

    // خوب (توجه کنید که ویرگول نباید بعد از یک عنصر "rest" ظاهر شود)
    createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    );
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## نقطه ویرگول ها

  <a name="semicolons--required"></a><a name="20.1"></a>
  - [21.1](#semicolons--required) **بله.** eslint: [`semi`](https://eslint.org/docs/rules/semi)

    > چرا؟ وقتی جاوااسکریپت با یک خط شکسته بدون نقطه ویرگول مواجه می‌شود، از مجموعه‌ای از قوانین به نام [درج خودکار نقطه‌ویرگول (Automatic Semicolon Insertion)](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) استفاده می‌کند تا تعیین کند آیا باید آن خط شکسته را به عنوان پایان یک دستور در نظر بگیرد یا خیر و (همان‌طور که از نامش پیداست) اگر چنین تصور کند، یک نقطه‌ویرگول قبل از خط شکسته در کد شما قرار دهد. با این حال، ASI شامل چندین رفتار عجیب و غریب است و اگر جاوااسکریپت خط شکسته شما را اشتباه تفسیر کند، کد شما خراب می‌شود. این قوانین با اضافه شدن ویژگی‌های جدید به جاوااسکریپت پیچیده‌تر خواهند شد. پایان دادن صریح به دستورات خود و پیکربندی لینتر برای گرفتن نقطه‌ویرگول‌های جاودان شده به شما کمک می‌کند تا از مواجهه با مشکلات جلوگیری کنید.

    ```javascript
    // bad - بد - خطا پرتاب می‌کند
    const luke = {}
    const leia = {}
    [luke, leia].forEach((jedi) => jedi.father = 'vader')

    // بد - خطا پرتاب می‌کند
    const reaction = "No! That’s impossible!"
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }())

    // بد - به جای مقدار در خط بعدی، `undefined` برمی‌گرداند - این همیشه وقتی `return` در یک خط به تنهایی قرار دارد به دلیل ASI رخ می‌دهد!
    function foo() {
      return
        'search your feelings, you know it to be foo'
    }

    // خوب
    const luke = {};
    const leia = {};
    [luke, leia].forEach((jedi) => {
      jedi.father = 'vader';
    });

    // خوب
    const reaction = 'No! That’s impossible!';
    (async function meanwhileOnTheFalcon() {
      // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }());

    // خوب
    function foo() {
      return 'search your feelings, you know it to be foo';
    }
    ```

    [بیشتر بخوانید](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214#7365214).

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## تبدیل نوع و واداشتن به تبدیل (Coercion)

  <a name="coercion--explicit"></a><a name="21.1"></a>
  - [22.1](#coercion--explicit) واداشتن به تبدیل نوع (type coercion) را در ابتدای دستور انجام دهید.

  <a name="coercion--strings"></a><a name="21.2"></a>
  - [22.2](#coercion--strings) رشته ها: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    // => this.reviewScore = 9;

    // bad
    const totalScore = new String(this.reviewScore); // typeof totalScore is "object" not "string"

    // bad
    const totalScore = this.reviewScore + ''; // این کار باعث فراخوانی this.reviewScore.valueOf() می‌شود

    // bad
    const totalScore = this.reviewScore.toString(); // تضمین نمی‌کند که یک رشته برگرداند

    // good
    const totalScore = String(this.reviewScore);
    ```

  <a name="coercion--numbers"></a><a name="21.3"></a>
  - [22.3](#coercion--numbers) اعداد: برای تبدیل نوع از `Number` و برای تجزیه رشته‌ها همیشه از `parseInt` به همراه یک مبنای عددی (radix) استفاده کنید. eslint: [`radix`](https://eslint.org/docs/rules/radix) [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    > چرا؟ تابع `parseInt` یک مقدار صحیح تولید می‌کند که بر اساس تفسیر محتویات آرگومان رشته‌ای طبق مبنای مشخص شده، دیکته می‌شود. فاصله‌های سفید ابتدایی در رشته نادیده گرفته می‌شود. اگر مبنای عددی (radix) `undefined` یا `0` باشد، فرض می‌شود که `10` است، مگر اینکه عدد با جفت کاراکترهای `0x` یا `0X` شروع شود، که در این صورت مبنای 16 فرض می‌شود. این با ECMAScript 3 که صرفاً تفسیر هشت‌تایی (octal) را منع می‌کرد (اما اجازه می‌داد) متفاوت است. بسیاری از پیاده‌سازی‌ها تا سال 2013 این رفتار را اتخاذ نکرده‌اند. و از آنجا که باید از مرورگرهای قدیمی پشتیبانی کرد، همیشه یک مبنای عددی مشخص کنید.

    ```javascript
    const inputValue = '4';

    // بد
    const val = new Number(inputValue);

    // بد
    const val = +inputValue;

    // بد
    const val = inputValue >> 0;

    // بد
    const val = parseInt(inputValue);

    // خوب
    const val = Number(inputValue);

    // خوب
    const val = parseInt(inputValue, 10);
    ```

  <a name="coercion--comment-deviations"></a><a name="21.4"></a>
  - [22.4](#coercion--comment-deviations) اگر به هر دلیلی کاری عجیب و غریب انجام می‌دهید و `parseInt` گلوگاه (bottleneck) شماست و به دلیل [مسائل مربوط به کارایی](https://web.archive.org/web/20200414205431/https://jsperf.com/coercion-vs-casting/3) مجبور به استفاده از عملیات شیفت بیتی (Bitshift) هستید، توضیحی گذاشته و دلیل کارتان و آنچه انجام می‌دهید را شرح دهید.

    ```javascript
    // good
    /**
     * parseInt دلیل کندی کد من بود.
     * شیفت بیتیِ رشته برای واداشتن آن به یک عدد
     * باعث شد بسیار سریع‌تر شود.
     */
    const val = inputValue >> 0;
    ```

  <a name="coercion--bitwise"></a><a name="21.5"></a>
  - [22.5](#coercion--bitwise) **نکته:** هنگام استفاده از عملیات شیفت بیتی محتاط باشید. اعداد به صورت [مقادیر ۶۴ بیتی](https://es5.github.io/#x4.3.19) نمایش داده می‌شوند، اما عملیات شیفت بیتی همیشه یک عدد صحیح ۳۲ بیتی برمی‌گردانند ([منبع](https://es5.github.io/#x11.7)). شیفت بیتی می‌تواند منجر به رفتارهای غیرمنتظره برای مقادیر صحیح بزرگتر از ۳۲ بیت شود. [بحث](https://github.com/airbnb/javascript/issues/109). بزرگترین عدد صحیح علامت‌دار ۳۲ بیتی 2,147,483,647 است:

    ```javascript
    2147483647 >> 0; // => 2147483647
    2147483648 >> 0; // => -2147483648
    2147483649 >> 0; // => -2147483647
    ```

  <a name="coercion--booleans"></a><a name="21.6"></a>
  - [22.6](#coercion--booleans) بولین‌ها: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

    ```javascript
    const age = 0;

    // بد
    const hasAge = new Boolean(age);

    // خوب
    const hasAge = Boolean(age);

    // بهترین
    const hasAge = !!age;
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## مقررات نام گذاری

  <a name="naming--descriptive"></a><a name="22.1"></a>
  - [23.1](#naming--descriptive) از نام‌های تک‌حرفی اجتناب کنید. نام‌گذاری‌هایتان باید توصیفی باشند. eslint: [`id-length`](https://eslint.org/docs/rules/id-length)

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
  - [23.2](#naming--camelCase) هنگام نام‌گذاری اشیاء، توابع و نمونه‌ها (instances) از `camelCase` استفاده کنید. eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase)

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
  - [23.3](#naming--PascalCase) از `PascalCase` فقط هنگام نام‌گذاری سازنده‌ها (constructors) یا کلاس‌ها استفاده کنید. eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap)

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
  - [23.4](#naming--leading-underscore) از خط زیر (_) انتهایی یا ابتدایی استفاده نکنید. eslint: [`no-underscore-dangle`](https://eslint.org/docs/rules/no-underscore-dangle)

    > چرا؟ جاوااسکریپت از نظر ویژگی‌ها یا متدها، مفهوم خصوصی‌سازی (privacy) ندارد. اگرچه خط زیر ابتدایی یک قرارداد رایج برای به معنای "خصوصی" است، اما در واقع این ویژگی‌ها کاملاً عمومی هستند و در نتیجه، بخشی از قرارداد API عمومی شما محسوب می‌شوند. این قرارداد ممکن است باعث شود توسعه‌دهندگان به اشتباه فکر کنند که یک تغییر، فوری (تکان دهنده - breaking) محسوب نمی‌شود، یا نیازی به تست ندارد. خلاصه: اگر می‌خواهید چیزی "خصوصی" باشد، نباید به صورت مشهود حضور داشته باشد.

    ```javascript
    // bad - بد
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // خوب
    this.firstName = 'Panda';

    // خوب، در محیط‌هایی که WeakMap در دسترس است
    // ببینید https://compat-table.github.io/compat-table/es6/#test-WeakMap
    const firstNames = new WeakMap();
    firstNames.set(this, 'Panda');
    ```

  <a name="naming--self-this"></a><a name="22.5"></a>
  - [23.5](#naming--self-this) ارجاعات `this` را ذخیره نکنید. از توابع پیکانی یا [Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) استفاده کنید.

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
  - [23.6](#naming--filename-matches-export) نام فایلِ پایه باید دقیقاً با نام خروجی پیش‌فرض (default export) آن مطابقت داشته باشد.

    ```javascript
    // file 1 contents - محتوای فایل 1
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // محتوای فایل 2
    export default function fortyTwo() { return 42; }

    // محتوای فایل 3
    export default function insideDirectory() {}

    // در برخی فایل‌های دیگر
    // بد
    import CheckBox from './checkBox'; // ورودی/خروجی PascalCase، نام فایل camelCase
    import FortyTwo from './FortyTwo'; // ورودی/نام فایل PascalCase، خروجی camelCase
    import InsideDirectory from './InsideDirectory'; // ورودی/نام فایل PascalCase، خروجی camelCase

    // بد
    import CheckBox from './check_box'; // ورودی/خروجی PascalCase، نام فایل snake_case
    import forty_two from './forty_two'; // ورودی/نام فایل snake_case، خروجی camelCase
    import inside_directory from './inside_directory'; // ورودی snake_case، خروجی camelCase
    import index from './inside_directory/index'; // صراحتاً درخواست فایل index
    import insideDirectory from './insideDirectory/index'; // صراحتاً درخواست فایل index

    // خوب
    import CheckBox from './CheckBox'; // خروجی/ورودی/نام فایل PascalCase
    import fortyTwo from './fortyTwo'; // خروجی/ورودی/نام فایل camelCase
    import insideDirectory from './insideDirectory'; // خروجی/ورودی/نام دایرکتوری/"index" ضمنی camelCase
    // ^ از هر دو مورد insideDirectory.js و insideDirectory/index.js پشتیبانی می‌کند
    ```

  <a name="naming--camelCase-default-export"></a><a name="22.7"></a>
  - [23.7](#naming--camelCase-default-export) هنگام export-default کردن یک تابع از `camelCase` استفاده کنید. نام فایل شما باید دقیقاً با نام تابع شما یکسان باشد.

    ```javascript
    function makeStyleGuide() {
      // ...
    }

    export default makeStyleGuide;
    ```

  <a name="naming--PascalCase-singleton"></a><a name="22.8"></a>
  - [23.8](#naming--PascalCase-singleton) هنگام صادر کردن یک سازنده / کلاس / سینگلتون (singleton) / کتابخانه تابع / شئ خام (bare object) از `PascalCase` استفاده کنید.

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      },
    };

    export default AirbnbStyleGuide;
    ```

  <a name="naming--Acronyms-and-Initialisms"></a>
  - [23.9](#naming--Acronyms-and-Initialisms) مخفف‌ها و سرنام‌ها (Acronyms and initialisms) همیشه باید کاملاً با حروف بزرگ یا کاملاً با حروف کوچک نوشته شوند.

    > چرا؟ نام‌ها برای خوانایی هستند، نه برای ارضای یک الگوریتم کامپیوتری.

    ```javascript
    // bad - بد
    import SmsContainer from './containers/SmsContainer';

    // بد
    const HttpRequests = [
      // ...
    ];

    // خوب
    import SMSContainer from './containers/SMSContainer';

    // خوب
    const HTTPRequests = [
      // ...
    ];

    // همچنین خوب است
    const httpRequests = [
      // ...
    ];

    // بهترین
    import TextMessageContainer from './containers/TextMessageContainer';

    // بهترین
    const requests = [
      // ...
    ];
    ```

  <a name="naming--uppercase"></a>
  - [23.10](#naming--uppercase) شما می‌توانید به صورت اختیاری یک ثابت را با حروف بزرگ بنویسید تنها در صورتی که (۱) صادر شده (export) باشد، (۲) یک `const` باشد (نمی‌تواند مجدداً انتساب داده شود)، و (۳) برنامه‌نویس بتواند به آن (و ویژگی‌های تودرتویش) اعتماد کند که هرگز تغییر نمی‌کند.

    > چرا؟ این یک ابزار اضافی برای کمک در شرایطی است که برنامه‌نویس مطمئن نیست آیا یک متغیر ممکن است تغییر کند یا خیر. متغیرهای_بزرگ‌نویسی_شده (UPPERCASE_VARIABLES) به برنامه‌نویس اطلاع می‌دهند که می‌توانند به متغیر (و ویژگی‌های آن) اعتماد کنند که تغییر نخواهند کرد.
    - در مورد همه متغیرهای `const` چه اتفاقی می‌افتد؟ - این کار غیرضروری است، بنابراین نباید برای ثابت‌های درون یک فایل از بزرگ‌نویسی استفاده کرد. با این حال، باید برای ثابت‌های صادر شده (exported) استفاده شود.
    - در مورد اشیاء صادر شده چه؟ - در سطح بالای صادرات بزرگ‌نویسی کنید (مثلاً `EXPORTED_OBJECT.key`) و تضمین کنید که تمام ویژگی‌های تودرتو تغییر نمی‌کنند.

    ```javascript
    // bad - بد
    const PRIVATE_VARIABLE = 'نباید درون یک فایل به طور غیرضروری بزرگ‌نویسی شود';

    // بد
    export const THING_TO_BE_CHANGED = 'واضح است که نباید بزرگ‌نویسی شود';

    // بد
    export let REASSIGNABLE_VARIABLE = 'از let همراه با متغیرهای بزرگ‌نویسی شده استفاده نکنید';

    // ---

    // مجاز است اما ارزش معنایی (semantic value) ارائه نمی‌دهد
    export const apiKey = 'SOMEKEY';

    // در بیشتر موارد بهتر است
    export const API_KEY = 'SOMEKEY';

    // ---

    // بد - در حالی که هیچ ارزش معنایی ارائه نمی‌دهد، به صورت غیرضروری کلید را بزرگ‌نویسی می‌کند
    export const MAPPING = {
      KEY: 'value'
    };

    // خوب
    export const MAPPING = {
      key: 'value',
    };
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## اکسسورها (Accessors)

  <a name="accessors--not-required"></a><a name="23.1"></a>
  - [24.1](#accessors--not-required) توابع اکسسور برای ویژگی‌ها الزامی نیستند.

  <a name="accessors--no-getters-setters"></a><a name="23.2"></a>
  - [24.2](#accessors--no-getters-setters) از گِتِرها/سِتِرهای جاوااسکریپت (getters/setters) استفاده نکنید زیرا آن‌ها باعث ایجاد اثرات جانبی غیرمنتظره می‌شوند و تست، نگهداری و استدلال در مورد آن‌ها دشوارتر است. در عوض، اگر توابع اکسسور می‌سازید، از `getVal()` و `setVal('hello')` استفاده کنید.

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
  - [24.3](#accessors--boolean-prefix) اگر ویژگی/متد از نوع `boolean` است، از `isVal()` یا `hasVal()` استفاده کنید.

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
  - [24.4](#accessors--consistent) ایجاد توابع `get()` و `set()` اشکالی ندارد، اما یکپارچه باشید.

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

## رویدادها (Events)

  <a name="events--hash"></a><a name="24.1"></a>
  - [25.1](#events--hash) هنگام پیوست کردن داده‌های محموله (data payloads) به رویدادها (چه رویدادهای DOM و چه چیزهای اختصاصی‌تر مانند رویدادهای Backbone)، به جای یک مقدار خام، یک لیترال شئ (که به عنوان "هش" نیز شناخته می‌شود) را پاس دهید. این امر به مشارکت‌کننده‌afterی اجازه می‌دهد تا بدون نیاز به پیدا کردن و به‌روزرسانی هر هندلر (handler) برای آن رویداد، داده‌های بیشتری به محموله رویداد اضافه کند. برای مثال، به جای:

    ```javascript
    // bad
    $(this).trigger('listingUpdated', listing.id);

    // ...

    $(this).on('listingUpdated', (e, listingID) => {
      // کاری با listingID انجام دهید
    });
    ```

    این مورد ترجیح داده می‌شود:

    ```javascript
    // good
    $(this).trigger('listingUpdated', { listingID: listing.id });

    // ...

    $(this).on('listingUpdated', (e, data) => {
      // کاری با data.listingID انجام دهید
    });
    ```

  **[⬆ بازگشت به بالا](#فهرست-مطالب)**

## jQuery

  <a name="jquery--dollar-prefix"></a><a name="25.1"></a>
  - [26.1](#jquery--dollar-prefix) به متغیرهای شئ jQuery پیشوند `$` اضافه کنید.

    ```javascript
    // bad
    const sidebar = $('.sidebar');

    // good
    const $sidebar = $('.sidebar');

    // good
    const $sidebarBtn = $('.sidebar-btn');
    ```

  <a name="jquery--cache"></a><a name="25.2"></a>
  - [26.2](#jquery--cache) جستجوهای jQuery را کَش (Cache) کنید.

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
  - [26.3](#jquery--queries) برای جستجوهای DOM از حالت آبشاری `$('.sidebar ul')` یا والد > فرزند `$('.sidebar > ul')` استفاده کنید. [jsPerf](https://web.archive.org/web/20200414183810/https://jsperf.com/jquery-find-vs-context-sel/16)

  <a name="jquery--find"></a><a name="25.4"></a>
  - [26.4](#jquery--find) از `find` به همراه جستجوهای شئ jQuery دارای دامنه (scoped) استفاده کنید.

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

## سازگاری با ECMAScript 5

  <a name="es5-compat--kangax"></a><a name="26.1"></a>
  - [27.1](#es5-compat--kangax) به [جدول سازگاری ES5](https://compat-table.github.io/compat-table/es5/) اثر [Kangax](https://twitter.com/kangax/) مراجعه کنید.

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

<a name="ecmascript-6-styles"></a>
## ECMAScript 6+ (ES 2015+) Styles

  <a name="es6-styles"></a><a name="27.1"></a>
  - [28.1](#es6-styles) این مجموعه‌ای از لینک‌ها به ویژگی‌های مختلف ES6+ است.

1. [Arrow Functions](#توابع-پیکانی)
1. [Classes](#کلاس-ها-و-سازنده-ها)
1. [Object Shorthand](#es6-object-shorthand)
1. [Object Concise](#es6-object-concise)
1. [Object Computed Properties](#es6-computed-properties)
1. [Template Strings](#es6-template-literals)
1. [Destructuring](#ساختارزدایی-Destructuring)
1. [Default Parameters](#es6-default-parameters)
1. [Rest](#es6-rest)
1. [Array Spreads](#es6-array-spreads)
1. [Let and Const](#ارجاعات-references)
1. [Exponentiation Operator](#es2016-properties--exponentiation-operator)
1. [Iterators and Generators](#تکرارکننده-ها-و-مولد-ها-Iterators-and-Generators)
1. [Modules](#ماژول-ها-modules)

  <a name="tc39-proposals"></a>
  - [28.2](#tc39-proposals) از [پروپوزال‌های TC39](https://github.com/tc39/proposals) که به مرحله ۳ نرسیده‌اند استفاده نکنید.

    > چرا؟ [آن‌ها هنوز نهایی نشده‌اند](https://tc39.github.io/process-document/) و ممکن است تغییر کنند یا به طور کامل پس گرفته شوند. ما می‌خواهیم از جاوااسکریپت استفاده کنیم، و پروپوزال‌ها هنوز جاوااسکریپت نیستند.

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## کتابخانه استاندارد

  [کتابخانه استاندارد](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects)
  شامل ابزارهایی است که از نظر عملکردی خراب هستند اما به دلایل میراثی (legacy) باقی مانده‌اند.

  <a name="standard-library--isnan"></a>
  - [29.1](#standard-library--isnan) به جای `isNaN` سراسری، از `Number.isNaN` استفاده کنید.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > چرا؟ `isNaN` سراسری، غیراعداد را به عدد تبدیل (coerce) می‌کند و برای هر چیزی که به NaN تبدیل شود، `true` برمی‌گرداند.
    > اگر این رفتار مورد نظر است، آن را به صراحت انجام دهید.

    ```javascript
    // bad
    isNaN('1.2'); // false
    isNaN('1.2.3'); // true

    // good
    Number.isNaN('1.2.3'); // false
    Number.isNaN(Number('1.2.3')); // true
    ```

  <a name="standard-library--isfinite"></a>
  - [29.2](#standard-library--isfinite) به جای `isFinite` سراسری، از `Number.isFinite` استفاده کنید.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > چرا؟ `isFinite` سراسری، غیراعداد را به عدد تبدیل می‌کند و برای هر چیزی که به یک عدد متناهی تبدیل شود، `true` برمی‌گرداند.
    > اگر این رفتار مورد نظر است، آن را به صراحت انجام دهید.

    ```javascript
    // bad
    isFinite('2e3'); // true

    // good
    Number.isFinite('2e3'); // false
    Number.isFinite(parseInt('2e3', 10)); // true
    ```

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## آزمایش کردن (Testing)

  <a name="testing--yup"></a><a name="28.1"></a>
  - [30.1](#testing--yup) **بله.**

    ```javascript
    function foo() {
      return true;
    }
    ```

  <a name="testing--for-real"></a><a name="28.2"></a>
  - [30.2](#testing--for-real) **نه، اما جدی بگیرید**:
    - هر فریم‌ورک تستی که استفاده می‌کنید، باید تست بنویسید!
    - برای نوشتن توابع خالصِ کوچک و متعدد تلاش کنید و جاهایی که تغییرات (mutations) رخ می‌دهد را به حداقل برسانید.
    - در مورد stubها و mockها محتاط باشید - می‌توانند تست‌های شما را شکننده‌تر کنند.
    - ما در Airbnb عمدتاً از [`mocha`](https://www.npmjs.com/package/mocha) و [`jest`](https://www.npmjs.com/package/jest) استفاده می‌کنیم. [`tape`](https://www.npmjs.com/package/tape) نیز گاهی برای ماژول‌های کوچک و مجزا استفاده می‌شود.
    - پوشش تست (test coverage) ۱۰۰٪ هدف خوبی است که باید برای آن تلاش کنید، حتی اگر همیشه رسیدن به آن عملی نباشد.
    - هر بار که یک باگ را برطرف می‌کنید، *یک تست رِگرِسیون (regression test) بنویسید*. باگی که بدون تست رِگرِسیون اصلاح شود، تقریباً قطعا در آینده دوباره خراب خواهد شد.

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## کارایی (Performance)

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

## منابع

**یادگیری ES6+**

  - [آخرین مشخصات ECMA](https://tc39.github.io/ecma262/)
  - [ExploringJS](https://exploringjs.com/)
  - [جدول سازگاری ES6](https://compat-table.github.io/compat-table/es6/)
  - [نمای کلی جامع از ویژگی‌های ES6](https://web.archive.org/web/20240404212626/http://es6-features.org/)
  - [نقشه راه جاوااسکریپت (JavaScript Roadmap)](https://roadmap.sh/javascript)

**این را بخوانید**

  - [استاندارد ECMA-262](https://www.ecma-international.org/ecma-262/6.0/index.html)

**ابزار ها**

  - لینترهای سبک کد (Code Style Linters)
    - [ESlint](https://eslint.org/) - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)
    - [JSHint](https://jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/.jshintrc)
  - Neutrino Preset - [@neutrinojs/airbnb](https://neutrinojs.org/packages/airbnb/)

**راهنماهای سبک دیگر (Other Style Guides)**

  - [راهنمای سبک جاوااسکریپت گوگل](https://google.github.io/styleguide/jsguide.html)
  - [راهنمای سبک جاوااسکریپت گوگل (قدیمی)](https://google.github.io/styleguide/javascriptguide.xml)
  - [دستورالعمل‌های سبک اصلی جی‌کوئری](https://contribute.jquery.org/style-guide/js/)
  - [اصول نوشتن جاوااسکریپت یکپارچه و اصولی (Idiomatic)](https://github.com/rwaldron/idiomatic.js)
  - [StandardJS](https://standardjs.com)

**سبک‌های دیگر (Other Styles)**

  - [نام‌گذاری this در توابع تو در تو (nested functions)](https://gist.github.com/cjohansen/4135065) - Christian Johansen
  - [کال‌بک‌های شرطی (Conditional Callbacks)](https://github.com/airbnb/javascript/issues/52) - Ross Allen
  - [کنوانسیون‌های (conventions) محبوب کدنویسی جاوااسکریپت در گیت‌هاب](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
  - [چندین دستور var در جاوااسکریپت، غیرضروری نیستند](https://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**مطالعه بیشتر**

  - [درک بسته‌های جاوااسکریپت (Closures)](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [جاوااسکریپت پایه برای برنامه‌نویسان عجول](https://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [شاید به جی‌کوئری نیازی نداشته باشید](https://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 ویژگی‌های](https://github.com/lukehoban/es6features) - Luke Hoban
  - [دستورالعمل‌های فرانت‌اند](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**کتاب ها**

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

**وبلاگ ها**

  - [JavaScript Weekly](https://javascriptweekly.com/)
  - [JavaScript, JavaScript...](https://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](https://bocoup.com/weblog)
  - [Adequately Good](https://www.adequatelygood.com/)
  - [NCZOnline](https://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](https://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [nettuts](https://code.tutsplus.com/?s=javascript)

**پادکست ها**

  - [JavaScript Air](https://javascriptair.com/)
  - [JavaScript Jabber](https://devchat.tv/js-jabber/)

**[⬆ بازگشت به بالا](#فهرست-مطالب)**

## در دنیای واقعی

  این فهرستی از سازمان‌هایی است که از این راهنمای سبک استفاده می‌کنند. یک Pull Request برای ما بفرستید تا شما را به فهرست اضافه کنیم.

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

## ترجمه

  این راهنمای سبک به زبان‌های دیگری نیز در دسترس است:

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

## راهنمای راهنمای سبک جاوااسکریپت

  - [مرجع](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)

## با ما درباره جاوااسکریپت گپ بزنید

  - ما را در [گِیتر (gitter)](https://gitter.im/airbnb/javascript) پیدا کنید.

## همکاران (Contributors)

  - [مشاهده مشارکت‌کنندگان](https://github.com/airbnb/javascript/graphs/contributors)

## مجوز

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

## اصلاحیه ها

ما شما را تشویق می‌کنیم که این راهنما را فورک (fork) کنید و قوانین را برای تطبیق با راهنمای سبک تیم خود تغییر دهید. در زیر، می‌توانید فهرستی از اصلاحیه‌های مربوط به راهنمای سبک را لیست کنید. این امر به شما اجازه می‌دهد تا راهنمای سبک خود را به صورت دوره‌ای به‌روزرسانی کنید بدون اینکه مجبور باشید با تضادهای ادغام (merge conflicts) دست و پنجه نرم کنید.

# };
