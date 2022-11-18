# مـعرف_عالمي Uuid
[[English]](readme.md)

ربط للأسس مع مكتبة libuuid.

## إضافة المكتبة للمشروع
 
اشمل المكتبة في مشروعك كالتالي:
```
اشمل "مـحا"؛
مـحا.اشمل_ملف("Alusus/Uuid"، "مـعرف_عالمي.أسس")؛
```
```
import "Apm";
Apm.importFile("Alusus/Uuid");
```


## الدالات

### أنشئ generate

دالة توليد معرف عشوائي. تأخذ متغيرًا من النمط uuid_t وتضع قيمة عشوائية فيه.
```
دالة أنشئ (معرف: سند[مـعرف])؛
```
```
function generate (uuid: ref[uuid_t]);
```

### قارن compare

تقارن بين معرفين. تعيد 0 في حال كانا متطابقين و1 فيما عدا ذلك.
```
دالة قارن (معرف1: سند[مـعرف]، معرف2: سند[مـعرف]): صـحيح؛
```
```
function compare (uuid1: ref[uuid_t], uuid2: ref[uuid_t]): Int;
```

### فرغ clear

تمحو القيمة الموجودة في متغير.
```
دالة فرغ (معرف: سند[مـعرف])؛
```
```
function clear (uuid: ref[uuid_t]);
```

### انسخ copy

تنسخ معرفا من متغير إلى آخر. تستلم الدالة معطيين وتنسخ الثاني إلى الأول.
```
دالة انسخ (المقصد: سند[مـعرف]، المصدر: سند[مـعرف])؛
```
```
function copy (dest: ref[uuid_t], src: ref[uuid_t]);
```

### اقرأ_نصا parse

تحول معرفا من شكله النصي إلى الشكل الرقمي.
```
دالة اقرأ_نصا (نص: مؤشر[مصفوفة[مـحرف]]، معرف: سند[مـعرف]): صـحيح؛
```
```
function parse (uuid: ptr[array[char]],uuid2: ref[uuid_t]): Int;
```

### اكتب_نصا unparse

تحول معرفا من شكله الرقمي إلى الشكل النصي.
```
دالة اكتب_نصا (معرف: سند[مـعرف]، ناتج: مؤشر[مصفوفة[مـحرف]])؛
```
```
function unparse (uuid: ref[uuid_t], out: ptr[array[char]]);
```

### أهو_فارغ isNull

تتحقق فيما إذا كان المعطى يحمل معرفاً أم أنه فارغ. تعيد 1 في حال كان المعطى فارغًا وإلا فترجع 0.
```
دالة أهو_فارغ (معرف: سند[مـعرف]): صـحيح؛
```
```
function isNull (uuid: ref[uuid_t]): Int;
``` 

## مثال

```
اشمل "مـتم/طـرفية"؛
اشمل "مـحا"؛
مـحا.اشمل_ملف("Alusus/Uuid"، "مـعرف_عالمي.أسس")؛

دالة اختبر {
    استخدم مـعرف_عالمي؛
    استخدم مـتم.طـرفية؛

    عرف ع1: مـعرف؛
    عرف ع2: مـعرف؛
    عرف نص: مصفوفة[محرف, 100]؛

    // توليد معرف عشوائي.
    أنشئ(ع1)؛

    // نحتاج لتحويل القيمة لصيغة نصية قبل أن نتمكن من طباعتها.
    اكتب_نصا(ع1, نص~مؤشر)؛
    اطبع("معرف عشوائي: %s\ج", نص~مؤشر)؛

    // سيكون الناتج كالتالي:
    // معرف عشوائي: 5126ead0-be18-494f-a403-034c75d9cf93 

    اطبع("تفريغ المعرف.\ج")؛
    فرغ(ع2)؛

    // تأكد أن المعرف الآن فارغ
    إذا أهو_فارغ(ع2) == 1 اطبع("المعرف تم تفريغه.\ج")
    وإلا اطبع("المعرف لم يتم تفريغه.\ج")؛

    // سيكون الناتج:
    // تفريغ المعرف.
    // المعرف تم تفريغه.

    اطبع("أدخل معرفًا: ")؛
    أدخل_محارف(نص~مؤشر, 100)؛ 

    // حول للصيغة الرقمية.
    اقرأ_نصا(نص~مؤشر, ع2)؛

    // هل أدخل المستخدم نفس المعرف المولد أعلاه؟
    إذا قارن(ع1, ع2) == 0 اطبع("المعرفان متطابقان.\ج")
    وإلا اطبع("المعرفان غير متطابقين.\ج")؛

    انسخ(ع1, ع2)؛
    
    إذا قارن(ع1, ع2) == 0 اطبع("المعرفان متطابقان.\ج")
    وإلا اطبع("المعرفان غير متطابقين.\ج")؛
    
    // الناتج سيكون:
    // المعرفان متطابقان.
}

اختبر()؛
```

```
import "Srl/Console";
import "Apm";
Apm.importFile("Alusus/Uuid");

func test {
    use Uuid;
    use Srl.Console;

    def u1: uuid_t;
    def u2: uuid_t;
    def str: array[char, 100];

    // Generate a random UUID.
    generate(u1);

    // We need to convert the value to a string before we can print it.
    unparse(u1, str~ptr);
    print("Randomly generated UUID: %s\n", str~ptr);

    // Output will be something like this:
    // Randomly generated UUID as array of chars: 5126ead0-be18-494f-a403-034c75d9cf93 

    print("clearning the uuid\n");
    clear(u2);

    // Check if the uuid has been cleared.
    if isNull(u2) == 1 print("uuid is cleared!\n")
    else print("uuid is not cleared\n");

    // output:
    // clearning the uuid
    // uuid is cleared!

    print("Enter Uuid as a string: ");
    getString(str~ptr, 100);

    // Convert to uuid_t
    parse(str~ptr, u2);

    // Did the user enter the same value as the generated one?
    if compare (u1, u2) == 0 print("u1 and u2 are equal.\n")
    else print("u1 and u2 are not equal.\n");

    copy(u1, u2);
    
    if compare (u1, u2) == 0 print("u1 and u2 are equal.\n")
    else print("u1 and u2 are not equal.\n");

    // Output will be:
    // u1 and u2 are equal.
}

test();
```

