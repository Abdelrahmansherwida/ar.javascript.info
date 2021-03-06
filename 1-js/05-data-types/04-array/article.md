# المصفوفات

تسمح لك الكائنات بتخزين مجموعه من المفاتيح ذات قيم .الي الان هذا جيد .

ولكن في كثير من الأحيان نجد أننا بحاجة إلى *مجموعة مرتبة*, حيث لدينا عنصر الأول والثاني والثالث وما إلى ذلك. علي سبيل المثال, نحن نحتاج الي تخزين مجموعه من الشياء: مسخدمين, بضائع, عناصر HTML الخ.

ليس من المناسب ان نستخدم كائن هنا, لانه لايمتلك اي وسائل او طرق لترتيب العناصر. لايمكنا ادراج خاصيه جديده “بين” الموجوده بالفعل. الكائنات ليست معده لهذا الاستخدام فقط.

يوجد هيكل بيانات خاص يسمي `Array`, لتخزين المجموعات المرتبه.

## الاعلان

هناك طريقتين لإنشاء مصفوفه فارغه:

```js
let arr = new Array();
let arr = [];
```

في جميع الأوقات تقريبًا ، يتم استخدام بناء الجملة الثاني. يمكننا توفير العناصر الأولية في الأقواس:

```js
let fruits = ["البرقوق", "البرتقال", "التفاح"];
```

يتم ترقيم عناصر المصفوفه ، بدءًا من صفر.
يمكننا الحصول على عنصر من خلال الترقيم بين قوسين معقوفين:

```js run
let fruits = ["البرقوق", "البرتقال", "التفاح"];

alert( fruits[0] ); // التفاح
alert( fruits[1] ); // البرتقال
alert( fruits[2] ); // البرقوق
```

يمكننا استبدال عنصر:

```js
fruits[2] = 'الكمثري'; // الآن ["التفاح", "البرتقال", "الكمثري"]
```

...او اضف واحد جديد الي المصفوفه :

```js
fruits[3] = 'الليمون'; // الآن ["الليمون", "الكمثري", "البرتقال", "التفاح"]
```

العدد الإجمالي للعناصر في المصفوفه هو `length`:

```js run
let fruits = ["البرقوق", "البرتقال", "التفاح"];

alert( fruits.length ); // 3
```

يمكن ان نستخدم `alert` حتي نعرض المصفوفه كامله.

```js run
let fruits = ["البرقوق", "البرتقال", "التفاح"];

alert( fruits ); // البرقوق,البرتقال,التفاح
```

يمكن للمصفوفه ان تخزن عناصر من جميع الانواع.

على سبيل المثال:

```js run no-beautify
// مزيج من القيم
let arr = [ 'التفاح', { name: 'جوهان' }, true, function() { alert('اهلا'); } ];

// احصل على الكائن في الفهرس 1 ثم إظهار اسمه
alert( arr[1].name ); // جوهان

// احصل على الكائن في الفهرس 3 ثم إظهار اسمه
arr[3](); // اهلا
```


````smart header="الفاصلة اللاحقة"
المصفوفه ، تمامًا مثل الكائن ، قد تنتهي بفاصلة:
```js
let fruits = [
  "التفاح",
  "البرتقال",
  "البرقوق"*!*,*/!*
];
```

يسهّل نمط "الفاصلة اللاحقة" إدراج / إزالة العناصر ، لأن جميع الخطوط متشابهة.````


## وسائل pop/push, shift/unshift

 [الطابور](https://en.wikipedia.org/wiki/Queue_(abstract_data_type)) هو أحد الاستخدامات الأكثر شيوعًا للمصفوفة. في علوم الحاسب, هذا يعني مجموعة مرتبة من العناصر التي تدعم عمليتين:

- `push`إلحاق عنصر إلي النهاية.
- `shift` احصل على عنصر من البداية ، بدفع قائمة الانتظار ، بحيث يصبح العنصر الثاني هو الأول.

![](queue.svg)

تدعم المصفوفات كلا من العمليتين.
في الممارسة العملية نحن بحاجة إليها في كثير من الأحيان. على سبيل المثال ،مجموعه الرسائل التي يجب عرضها على الشاشة.
هناك حالة استخدام أخرى للمصفوفات -- هيكل البيانات يسمي [stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)).

يدعم عمليتين:

- `push` يضيف عنصرًا إلى النهاية.
- `pop` يأخذ عنصر من النهاية.

لذلك يتم إضافة عناصر جديدة أو أخذها دائمًا من "النهايه".

 الكومه(stack) عادة ما يتم توضيحها كحزمة من البطاقات: تتم إضافة بطاقات جديدة إلى الأعلى أو مأخوذة من الأعلى:

![](stack.svg)

بالنسبه للكومه(stacks), يتم استلام أحدث عنصر مدفوع أولاً ، وهذا ما يسمى  بمبدأ LIFO (Last-In-First-Out). بالنسبة لقوائم الانتظار ، لدينا FIFO (First-In-First-Out).

يمكن أن تعمل المصفوفات في JavaScript كقائمة انتظار وكمجموعة(stack). تتيح لك إضافة / إزالة عناصر من / إلى البداية أو النهاية.

في علم الحاسوب يسمى هيكل البيانات الذي يسمح بذلك [deque](https://en.wikipedia.org/wiki/Double-ended_queue).

**الأساليب التي تعمل مع نهاية المصفوفه:**

`pop`
:تعمل علي استخراج العنصر الأخير من المصفوفة وتعيده :

    ```js run
     ;["الكمثري", "البرتقال", "التفاح"] = let fruits

     ;alert( fruits.pop() ) // قم بإزاله "الكمثري" وقم بالعرض في تنبيه

     ;alert( fruits ) // البرتقال, التفاح
    ```

`push`
: ألحق العنصر بنهاية المصفوفة:

    ```js run
    let fruits = ["البرتقال", "التفاح"];

    fruits.push("الكمثري");

    alert( fruits ); // الكمثري, البرتقال, التفاح
    ```

    تنفيذ هذا الكود الاتي `(...)fruits.push` يساوي تماما `fruits[fruits.length] = ...`.

**الأساليب التي تعمل مع بدايه المصفوفه:**

`shift`
: تعمل علي استخراج العنصر الاول من المصفوفة وتعيده:

    ```js run
    let fruits = ["الكمثري", "البرتقال", "التفاح"];

    alert( fruits.shift() ); // قم بإزاله التفاح وقم بالعرض في تنبيه

    alert( fruits ); // الكمثري, البرتقال
    ```

`unshift`
: إضافه العنصر في بدايه المصفوفه:

    ```js run
    let fruits = ["الكمثري", "البرتقال"];

    fruits.unshift('التفاح');

    alert( fruits ); // الكمثري, البرتقال, التفاح
    ```

الوسائل `push` و `unshift` يمكنهم إضافة عناصر متعددة في وقت واحد:

```js run
let fruits = ["التفاح"];

fruits.push("خوخ", "البرتقال");
fruits.unshift("الليمون", "أناناس");

// ["الخوخ", "البرتقال", "التفاح", "الليمون", "أناناس"]
alert( fruits );
```

## البنيه الداخليه للمصفوفه

المصفوفه هي نوع خاص من الكائن. الأقواس المربعة تستخدم للتحكم في الخاصيه `arr[0]` في الواقع تأتي من بناء الكائن. هذا في الاساس نفس `obj[key]`, عندما تكون `arr` كائن, بينما الارقام تستخدم كمفاتيح.

إنها تمد الكائنات التي توفر وسائل خاصة للعمل مع مجموعات البيانات المطلوبة وكذلك خاصية `length '. ولكن في جوهرها لا يزال كائن.
تذكر,لا يوجد سوى 7 أنواع أساسية في جافا سكريبت. المصفوفه عباره عن كائن لذالك هي تتصرف مثله.

على سبيل المثال, يتم نسخه حسب المرجع:

```js run
let fruits = ["الموز"]

let arr = fruits; // نسخ عن طريق المرجع (متغيران يشيران إلى نفس المصفوفة)
alert( arr === fruits ); // صحيح

arr.push("الكمثري"); // تعديل المصفوفه حسب المرجع

alert( fruits ); // الموز ، الكمثرى - 2 من العناصر الآن
```

...ولكن ما يجعل المصفوفات مميزة حقًا هو بنيتها الداخليه. يحاول المحرك تخزين عناصره في منطقة الذاكرة المجاورة, واحد تلو الآخر, تمامًا كما هو موضح في الرسوم التوضيحية في هذا الفصل ، وهناك تحسينات أخرى أيضًا ، لجعل المصفوفات تعمل بسرعة كبيرة.

لكن جميعها تنكسر إذا توقفنا عن العمل مع مصفوفة كما هو الحال مع "مجموعة مرتبة" وبدأنا في العمل معها كما لو كانت كائنًا عاديًا.

على سبيل المثال ، من الناحية الفنية يمكننا القيام بذلك:

```js
let fruits = []; // إنشاء مصفوفه

fruits[99999] = 5; // قم بتعيين الخاصيه مع الفهرس أكبر بكثير من طوله

fruits.age = 25; // أنشئ الخاصيه باسم افتراضي 
```

هذا ممكن ، لأن المصفوفات هي كائن في أساسها. يمكننا إضافة أي خصائص لهم.

لكن المحرك سيرى أننا نعمل مع المصفوفه كما هو الحال مع كائن عادي. التحسينات الخاصة بالمصفوفه غير مناسبة لمثل هذه الحالات وسيتم إيقافها ، وتختفي فوائدها.

طرق إساءة استخدام مصفوفة:

- أضف خاصية غير رقمية مثل `arr.test = 5`.
- اصنع فراغ, مثل: إضافه `arr[0]` وثم `arr[1000]` (ولا شيء بينهما).
- املأ المصفوفة بالترتيب العكسي, مثل `arr[1000]`, `arr[999]` وما إلي ذالك.

يرجى التفكير في المصفوفات كبنى خاصة للعمل مع * البيانات المطلوبة *. أنها توفر أساليب خاصة لذلك.يتم ضبط المصفوفات بعنايةداخل محركات JavaScript للعمل مع البيانات المرتبة المتجاورة ، يرجى استخدامها بهذه الطريقة. وإذا كنت بحاجة إلى مفاتيح عشوائية ،هناك احتمالات عالية بأنك تحتاج بالفعل إلى كائن عادي `{}`.

## الأداء

الوسائل `push/pop` يتم تنفيذها أسرع, بينما `shift/unshift` تكون أبطئ.

![](array-speed.svg)

لماذا يكون العمل مع نهاية المصفوفة أسرع من بدايته؟ دعونا نرى ما يحدث أثناء التنفيذ:

```js
fruits.shift(); // قم بأخذ عنصر من البدايه
```

لا يكفي أخذ العنصر وإزالته بالرقم `0`.يجب إعادة ترقيم العناصر الأخرى أيضًا.

 `shift` هذه العمليه يجب ان تفعل 3 أشياء:

1. إزالة العنصر باستخدام الفهرس `0`.
2. انقل كل العناصر إلى اليسار, ترقيمها من الفهرس `1` الي `0`, من `2` الي `1` وما الي ذالك.
3.  قم بتحديث خاصيه `length` .

![](array-shift.svg)

**مزيد من العناصر في المصفوفه, مزيد من الوقت لتحريكها, المزيد من العمليات في الذاكرة.**

نفس الشئ يحدث مع `unshift`: حتي تضيف عنصر في بدايه المصفوفه, نحتاج أولاً إلى نقل العناصر الموجودة إلى اليمين, زياده ترقيمهم لدي الفهرس.

 وماذا مع الوسائل `push/pop`? لا يحتاجون لتحريك أي شيء. حتي تستخلص عنصر من النهايه,  `pop`  هذه الوسيله تمسح الفهرس وتقلل من الطول `length`.

 `pop` الإجراءت التشغليه لهذه الوسيله:

```js
fruits.pop(); // تأخذ عنصر واحد من النهايه
```

![](array-pop.svg)

** `pop` لاتحتاج هذه الوسيله الي نقل أي شئ, لان العناصر الاخري تحتفظ بفهارسها. هذا هو السبب في أنها سريعه للغايه.**

  نفس الشئ يحدث مع الوسيله`push` .

## الحلقات التكراريه

واحده من اقدم الطرق لتكرار لستخدام عناصر المصفوفه هي الحلقه   `for` عبر الفهارس:

```js run
let arr = ["الكمثري", "البرتقال", "التفاح"];

*!*
for (let i = 0; i < arr.length; i++) {
*/!*
  alert( arr[i] );
}
```

ولكن بالنسبة للمصفوفات ، هناك شكل آخر من أشكال الحلقات, `for..of`:

```js run
let fruits = ["البرقوق", "البرتقال", "التفاح"];

// يتكرر عبر عناصر المصفوفه
for (let fruit of fruits) {
  alert( fruit );
}
```

The `for..of` لا يمنح الوصول إلى رقم العنصر الحالي, فقط قيمته ,ولكن في معظم الحالات يكون ذلك كافيًا. وهي أقصر.

من الناحية الفنية ، نظرًا لأن المصفوفات هي كائنات ، فمن الممكن أيضًا استخدامها `for..in`:

```js run
let arr = ["الكمثري", "البرتقال", "التفاح"];

*!*
for (let key in arr) {
*/!*
  alert( arr[key] ); // الكمثري, البرتقال, التفاح
}
```

لكن هذه في الواقع فكرة سيئة. هناك مشاكل محتملة معها:

1. تتكرر الحلقة `for ... in` على * جميع الخصائص * ، وليس فقط الخصائص الرقمية.

    هناك ما يسمى بكائنات "مثل المصفوفة" في المتصفح وفي بيئات أخرى, انها *تبدوا مثل المصفوفات*. أي ، لديهم `length` ولديهم خصائص الفهرس, ولكن قد يكون لديهم أيضًا خصائص وسائل غير رقمية أخرى, التي لا نحتاجها عادةً.  `for..in` هذه الحلقه سوف ترتبهم بالرغم من ذلك. لذا إذا احتجنا للعمل مع كائنات تشبه المصفوفة ، فقد تصبح هذه الخصائص "الإضافية" مشكلة.
2. تم تحسين الحلقة `for..in` للعناصر العامة ، وليس للمصفوفات ، وبالتالي فهي أبطأ بمقدار 10-100 مرة. بالطبع ، إنها لا تزال سريعة جدًا. قد يكون التسريع مهمًا فقط في الاختناقات. ولكن لا يزال يتعين علينا أن ندرك الفرق.

بشكل عام ، لا يجب استخدام "for..in" للمصفوفات.


## كلمه عن "length"

 `length` يتم تحديث هذه الخاصيه تلقائيًا عندما نقوم بتعديل المصفوفه. على وجه الدقة ، في الواقع هو ليس عدد القيم في المصفوفة ، ولكنه أكبر  من مؤشرالفهرس بواحد صحيح.

على سبيل المثال ، عنصر واحد بمؤشر كبير يعطي طولًا كبيرًا:

```js run
let fruits = [];
fruits[123] = "التفاح";

alert( fruits.length ); // 124
```

لاحظ أننا عادة لا نستخدم مصفوفات من هذا القبيل.

شيء آخر مثير للاهتمام حول خاصية `length` هو أنه قابل للكتابة.

إذا تم تزوديها يدويًا ، فلن يحدث شيء مثير للاهتمام. ولكن إذا قللناه ، فسيتم اقتطاع المصفوفة. العملية لا رجعة فيها ، وإليك المثال:

```js run
let arr = [1, 2, 3, 4, 5];

arr.length = 2; // يتم اقتطاعها إلى عنصرين
alert( arr ); // [1, 2]

arr.length = 5; // أعد قيمه الطول
alert( arr[3] ); // غيرمعرف: لذالك القيم لن تعد
```

لذا ، فإن أبسط طريقة لمسح المصفوفه هي: `;arr.length = 0`.


## ()new Array [#new-array]

يوجد اكثر من طريقه لإنشاء مصفوفه:

```js
let arr = *!*new Array*/!*("الخ", "الكمثري", "التفاح");
```

نادرًا ما يتم استخدامه ، لأن الأقواس المربعة `[] أقصر. أيضا هناك ميزة صعبة معها.

إذا تم استدعاء `مصفوفه جديده`  باستخدام وسيله واحدة عبارة عن رقم ، فإنه ينشئ مصفوفة * بدون عناصر ، ولكن بالطول المحدد *.

دعونا نرى كيف يمكن للمرء أن يطلق النار على قدمه:

```js run
let arr = new Array(2); //هل سينشئ مصفوفه مكونه من [2] ?

alert( arr[0] ); // غير معرف! لا توجد عناصر.

alert( arr.length ); // الطول 2
```

في الكود أعلاه, `مصفوفه جديده(رقم)` تكون لديها كل العناصر `غير معرفه`.

للتهرب من هذه المفاجآت ، نستخدم عادةً الأقواس المربعة ، إلا إذا كنا نعرف حقًا ما نقوم به.

## مصفوفات متعدده الأبعاد

يمكن أن تحتوي المصفوفات على عناصر عبارة عن مصفوفات أيضًا. يمكننا استخدامه للمصفوفات متعددة الأبعاد ، على سبيل المثال لتخزين المصفوفات:

```js run
let matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

alert( matrix[1][1] ); // 5, العنصر المركزي
```

## التحويل إلي نص

المصفوفات لها تنفيذها الخاص لطريقة `toString` التي تُرجع قائمة من العناصر مفصولة بفواصل.

علي سبيل المثال:


```js run
let arr = [1, 2, 3];

alert( arr ); // 1,2,3
alert( String(arr) === '1,2,3' ); // صحيح
```

أيضا ، دعنا نجرب هذا:

```js run
alert( [] + 1 ); // "1"
alert( [1] + 1 ); // "11"
alert( [1,2] + 1 ); // "1,21"
```

لا تحتوي المصفوفات على `Symbol.toPrimitive` ، ولا على` valueOf` قابلة للتطبيق ، فهي تنفذ تحويل `toString` فقط ، لذلك هنا` [] تصبح سلسلة فارغة ، `[1]` تصبح "" 1 "" و "[ 1،2] `تصبح" 1،2 ".
عندما تضيف the binaryn plus بالإضافة إلى علامة "+" فإن هذا العامل يضيف هذا الشئ إلى سلسله نصيه ، فإنه يحولها إلى سلسلة أيضًا ، لذا تبدو الخطوة التالية كما يلي:

```js run
alert( "" + 1 ); // "1"
alert( "1" + 1 ); // "11"
alert( "1,2" + 1 ); // "1,21"
```

## الملخص

المصفوفات هو نوع خاص من الكائنات ، مناسب لتخزين وإدارة عناصر البيانات المطلوبة.

- الإعلان:

    ```js
    // الأقواس المربعة (المعتادة)
    let arr = [العنصر2, العنصر1...];

    // مصفوفه جديده (نادره للغايه)
    let arr = new Array(العنصر2, العنصر1...);
    ```

    يؤدي استدعاء "مصفوفه جديده (رقم) " إلى إنشاء مصفوفة بطول معين ، ولكن بدون عناصر..

- الخاصية `length` هي طول المصفوفة أو ، على وجه الدقة ، آخر فهرس رقمي بالإضافة إلى واحد. يتم ضبطه تلقائيًا بواسطة طرق للمصفوفه.
- إذا اختصرنا "الطول" يدويًا ، فسيتم اقتطاع المصفوفة.

يمكننا استخدام مصفوفة كمادة مع العمليات التالية:

- `push(...عناصر)`تضيف `العناصر` إلى النهاية.
- `pop()`إزالة العنصر من النهاية وإعادته.
- `shift()` يزيل العنصر من البداية ويعيده.
- `unshift(...عناصر)` تضيف `العناصر` إلي البدايه.

للتكرار فوق عناصر المصفوفة:
  - `for (let i=0; i<arr.length; i++)` --يعمل بشكل أسرع ومتوافق مع المتصفح القديم.
  - `for (let item of arr)` -- البنية الحديثة للعناصر فقط ،
  - `for (let i in arr)` -- لم يستعمل أبدا.

سنعود إلى المصفوفات ودراسة المزيد من الطرق لإضافة العناصر وإزالتها واستخراجها وفرز المصفوفات في الفصل <info:array-methods>.
