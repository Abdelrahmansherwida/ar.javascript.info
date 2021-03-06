# الحلقات التكرارية: while و for

أحيانًا نحتاج لتكرار مجموعة من الأوامر.

مثل عرض منتجات من قائمة واحدًا تلو الآخر أو تكرار نفس الأمر عشر مرات.

_الحلقات التكرارية_ هي طريقة لتكرار الأوامر.

## حلقة "while"

إن حلقة `while` تكتب بالطريقة التالية:

```js
while (condition) {
    // code
    // so-called "loop body"
}
```

طالما `condition` محقق يتم تنفيذ الكود المكتوب بداخلها.

على سبيل المثال فإن الكود التالي يعرضقيمة `i` طالما `i < 3`:

```js run
let i = 0;
while (i < 3) {
    // يعرض 0 ثم 1 ثم 2
    alert(i);
    i++;
}
```

تنفيذ الأوامر لمرة واحدة _تكرار_. المثال السابق يقوم بثلاثة عمليات تكرار.

إذا حذفت `i++` سيتم تنفيذ الأوامر (نظريًا) إلى الأبد. ولكن في الحقيقة يقوم المتصفح بمنع حدوث هذا وعند استخدام الجافاسكربت في جانب Server يمكننا لإنهاء العملية.

يمكن لأي تعبير أن يكون شرط للتكرار وليس فقط عمليات المقارنة. يتم تنفيذ العملية وتحويل الناتج إلى قيمة منطقية بواسطة `while`.

على سبيل المثال يمكن اختصار `while (i != 0)` إلى `while (i)`:

```js run
let i = 3;
*!*
while (i) { // عندما i تصبح 0, يصبح الشرط falsy وتتوقف الحلقة
*/!*
  alert( i );
  i--;
}
```

````smart header="الأقواس المعقوفة غير ضرورية عند تنفيذ أمر واحد"
إذا أردنا تنفيذ أمر واحد فقط فيمكن تجاهل الأقواس المعقوفة `{…}`:

```js run
let i = 3;
*!*
while (i) alert(i--);
*/!*
```
````

## حلقة "do..while"

يمكن نقل الشرط إلى بعد الأوامر باستخدام نمط `do..while`:

```js
do {
    // loop body
} while (condition);
```

سيتم أولا تنفيذ الأوامر ثم اختبار الشرط وإذا تحقق سيتم تنفيذ الأوامر مرة أخرى.

على سبيل المثال:

```js run
let i = 0;
do {
    alert(i);
    i++;
} while (i < 3);
```

هذه الطريقة يجب أن تستخدم فقط إذا أرد للأوامر أن تنفذ **مرة واحدة على الأقل** متجاهلًا الشرط. ففي الغالب يفضل استخدام: `while(…) {…}`.

## حلقة "for"

حلقة `for` معقدة أكثر ولكنها الأكثر استخدامًا في تكرار الأوامر.

تكتب كالآتي:

```js
for (begin; condition; step) {
    // ... loop body ...
}
```

لنتعرف على معاني هذه الأجزاء باستخدام مثال. الحلقة التالية تنفذ الأمر `alert(i)` ابتداءًا من `i` تساوي `0` حتى (لكن لا تشمل) `3`:

```js run
for (let i = 0; i < 3; i++) {
    // تعرض 0 ثم 1 ثم 2
    alert(i);
}
```

لنشرح `for` جزء بجزء:

| الجزء     |            |                                                             |
| --------- | ---------- | ----------------------------------------------------------- |
| begin     | `i = 0`    | ينفذ مرة واحدة فقط في البداية.                              |
| condition | `i < 3`    | يتم اختباره قبل كل عملية تكرار وإذا لم يتحقق يتوقف التكرار. |
| body      | `alert(i)` | تنفذ طالما الشرط محقق.                                      |
| step      | `i++`      | ينفذ بعد body في كل عملية تكرار.                            |

الخوارزمية العامة للتكرار تعمل كالتالي:

```
نفذ begin
→ (if condition → نفذ body ثم نفذ step)
→ (if condition → نفذ body ثم نفذ step)
→ (if condition → نفذ body ثم نفذ step)
→ ...
```

وهكذا يتم تنفيذ `begin` مرة واحدة وبعد ذلك يبدأ التكرار: بعد كل عاختبار للشرط `condition` يتم تنفيذ `body` و `step`.

إذا كنت جديد على الحلقات التكرارية فيفضل الرجوع للمثال وتنفيذه خطوة بخطوة على ورقة.

هذا ما يحدث تمامًا في مثالنا:

```js
// for (let i = 0; i < 3; i++) alert(i)

// نفذ begin
let i = 0;
// if condition → نفذ body ثم نفذ step
if (i < 3) {
    alert(i);
    i++;
}
// if condition → نفذ body ثم نفذ step
if (i < 3) {
    alert(i);
    i++;
}
// if condition → نفذ body ثم نفذ step
if (i < 3) {
    alert(i);
    i++;
}
// ...finish, because now i == 3
```

````smart header="Inline variable declaration"
هنا تم تعريف العداد `i` داخل الحلقة. وهذا يسمى "inline" variable declaration. وهذه المتغيرات تكون متاحة فقط داخل الحلقة.

```js run
for (*!*let*/!* i = 0; i < 3; i++) {
  alert(i); // 0, 1, 2
}
alert(i); // خطأ! متغير غير معرف
```

بدلًا من تعريف متغير جديد يمكننا استخدام واحد معرف مسبقًا:

```js run
let i = 0;

for (i = 0; i < 3; i++) { // استخدام متغير معرف مسبقًا
  alert(i); // 0, 1, 2
}

alert(i); // 3, يمكن التعامل معه لأنه معرف خارج الحلقة
```

````

### أجزاء يمكن تخطيها

أي جزء من `for` يمكن الاستغناء عنه.

مثلًا إذا حذفنا `begin` لن يكون لدينا ما نفعله في بداية الحلقة.

مثل:

```js run
let i = 0; // تم تعريف وتخصيص قيمة المتغير

for (; i < 3; i++) {
    // لا نحتاج "begin"
    alert(i); // 0, 1, 2
}
```

يمكن أيضًا حذف جزء `step`:

```js run
let i = 0;

for (; i < 3; ) {
    alert(i++);
}
```

هذا يجعلها تطابق `while (i < 3)`.

يمكننا حذف كل شئ وخلق حلقة لا نهائية فارغة:

```js
for (;;) {
    // تتكرر دائمًا
}
```

لاحظ أن كلتا الفاصلتين المنقوطتين `;` داخل `for` يجب أن يوضعا وإلا سيظهر خطأ لغوي.

## إيقاف الحلقة

في العادة تتوقف الحلقة عندما يصبح الشرط غير محقق.

ولكن يمكننا اجبارها على التوقف في أي وقت باستخدام كلمة `break`.

على سبيل المثال فإن الحلقة التالية تطلب من المستخدم إدخال مجموعة أرقام وتتوقف إذا لم يدخل رقم:

```js run
let sum = 0;

while (true) {

  let value = +prompt("ادخل رقم", '');

*!*
  if (!value) break; // (*)
*/!*

  sum += value;

}
alert( 'المجموع: ' + sum );
```

تم تنشيط `break` في السطر `(*)` إذا قام المستخدم بإدخال سطر فارغ أو إيقاف الإدخال. وهذا يوقف الحلقة مباشرة ويذهب إلى السطر المكتوب بعدها والذي هو `alert`.

دمج "الحلقات اللانهائية + `break`" يستخدم في الحالات التي نريد فيها اختبار الشرط في منتصف التكرار أو في عدة أماكن وليس في بداية التكرار.

## المتابعة للتكرار التالي [#continue]

كلمة `continue` هي نسخة أخف من `break`. هي لا توقف الحلقة كلها ولكنها توقف التكرار الحالي وتبدأ تكرار جديد.

يمكننا استخدامها إذا انتهينا من التكرار الحالي ونريد الانتقال إلى تكرار جديد.

الكود التالي يستخدم `continue` لعرض القيم الفردية فقط:

```js run no-beautify
for (let i = 0; i < 10; i++) {

  // if true, تخطي الجزء الباقي من التكرار
  *!*if (i % 2 == 0) continue;*/!*

  alert(i); // 1, then 3, 5, 7, 9
}
```

في القيم الزوجية من `i` تقوم `continue` بإيقاف التكرار الحالى وتنتقل لتكرار جديد من `for` (بالرقم التالي). ولهذا فإن `alert` ينفذ فقط مع القيم الفردية.

``smart header="تساعد `continue` على تقليل التداخل"
يمكن عرض الأرقام الفردية بالطريقة التالية:

```js run
for (let i = 0; i < 10; i++) {
    if (i % 2) {
        alert(i);
    }
}
```

هذا الكود مطابق تمامًا للسابق. يمكننا فقط وضع الكود داخل `if` بدلًا من استخدام `continue`.

ولكن هذا ينتج مستوى آخر من التداخل (استدعاء `alert` داخل أقواس معقوفة). إذا كان ما بداخل `if` سطور كثيرة فهذا سيقلل من إمكانية قراءة الكود بوضوح.

`````

````warn header="لا يمكن استخدام `break/continue` في الجانب الأيمن من '?'"
لا يمكن استخدام هذه التعبيرات `break/continue` مع العامل الشرطي `?`.

على سبيل المثال إذا أخذنا هذا الكود:

```js
if (i > 5) {
  alert(i);
} else {
  continue;
}
```

...وكتبناه باستخدام علامة الاستفهام:


```js no-beautify
(i > 5) ? alert(i) : *!*continue*/!*; // continue لا يسمح باستخدامها هنا
```

...يتوقف عن العمل مع خطأ لغوي.

وهذا سبب آخر لعدم استخدام `?` بدلًا من `if`.
`````

## عنونة break/continue

أحيانا نريد الخروج من مجموعة حلقات متداخلة مرة واحدة.

في المثال التالي نقوم بالتكرار باستخدام `i` و `j`, ونطلب احداثيات `(i, j)` من `(0,0)` إلى `(2,2)`:

```js run no-beautify
for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        let input = prompt(`Value at coords (${i},${j})`, "");

        // إذا أردنا الخروج من هنا إلى Done (بالأسفل)?
    }
}

alert("Done!");
```

نحتاج إلى طريقة لإيقاف العملية إذا قام المستخدم بإلغاء الإدخال.

وضع `break` بعد `input` سيوقف فقط الحلقة الداخلية. وهذا غير مجدي--جاءت العنونة لإنقاذ الموقف!

إن _label_ يقوم بتعريف الحلقة باستخدام نقطتين قبلها:

```js
labelName: for (...) {
  ...
}
```

استخدام `break <labelName>` في الحلقة سيوقف الحلقة ذات العنوان المحدد:

```js run no-beautify
*!*outer:*/!* for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // إذا أدخل نص فارغ أو ألغى الإدخال قم بإيقاف الحلقتين
    if (!input) *!*break outer*/!*; // (*)

    // أفعل شئ ما بالقيمة...
  }
}
alert('Done!');
```

في الكود السابق تقوم `break outer` بالبحث عن label اسمه `outer` وتوقف هذه الحلقة.

لذلك ينتقل من `(*)` إلى `alert('Done!')`.

يمكن أيضا وضع العنوان في سطر منفصل:

```js no-beautify
outer:
for (let i = 0; i < 3; i++) { ... }
```

يمكن استخدام `continue` أيضًا مع label. وفي هذه الحالة سينتقل للتكرار التالي من الحلقة المحددة.

````warn header="Labels لا تستخدم للإنتقال إلى أي مكان"
Labels لا تسمح لنا بالإنتقال إلى أي مكان داخل الكود.

فعلى سبيل المثال لا يمكننا فعل التالي:
```js
break label; // لن تنتقل إلى label بالأسفل

label: for (...)
```

استخدام `break/continue` ممكن فقط من داخل الحلقة ويجب أن يكون Label موجود قبلهم.
````

## ملخص

تحدثنا عن 3 أنواع من الحلقات:

-   `while` -- يتم فحص الشرط قبل التكرار.
-   `do..while` -- يتم فحص الشرط بعد التكرار.
-   `for (;;)` -- يتم فحص الشرط قبل التكرار, بعض المتغيرات الأخرى للإعداد.

لعمل حلقة لانهائية غالبا يتم استخدام `while(true)`. ويمكن إيقافها مثل أي حلقة أخرى باستخدام `break`.

إذا لم نرد فعل أي شئ في التكرار الحالي ونريد الإنتقال إلى التكرار التالي يمكننا استخدام `continue`.

`break/continue` تدعم العناوين قبل الحلقة. العنوان هو الطريقة الوحيدة ل `break/continue` للإنتقال بين الحلقات المتداخلة إلى الحلقة الخارجية.
