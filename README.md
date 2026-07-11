برمجة 4 محركات سيرفو (Updated Detailed Report: Programming 4 Servo Motors)###
1. هدف المهمة (Task Objective)
بالعربية:

الهدف الأساسي من المشروع، كما هو موضح في مستند المهمة، هو برمجة 4 محركات سيرفو لتنفيذ إجراءات محددة في الكود.

الإجراء الأول هو التشغيل باستخدام مثال المسح (Sweep) لمدة ثانيتين.

الإجراء الثاني هو جعل جميع المحركات تتوقف وتثبت عند زاوية 90 درجة بعد انقضاء الثانيتين.

In English:

The primary objective of the project, as outlined in the task document, is to program 4 servo motors to perform specific actions in the code.

The first action is to run using the Sweep example for 2 seconds.

The second action is to make all motors hold at 90 degrees after the two seconds have passed.

2. تخصيص المنافذ للمحركات الأربعة (Pin Allocation for the 4 Motors)
بالعربية:
بدلاً من استخدام محرك واحد، تم توسيع المشروع ليشمل 4 محركات مستقلة، حيث يتم تخصيص كود منفصل ومنافذ مختلفة لكل محرك لضمان التحكم الفردي:

المحرك الثاني (servo2) متصل بالمنفذ الرقمي 8.

المحرك الثالث (servo3) متصل بالمنفذ الرقمي 7.

المحرك الرابع (servo4) متصل بالمنفذ الرقمي 6.

In English:
Instead of using a single motor, the project has been expanded to include 4 independent motors, where separate code and distinct pins are allocated for each motor to ensure individual control:

The second motor (servo2) is attached to digital pin 8.

The third motor (servo3) is attached to digital pin 7.

The fourth motor (servo4) is attached to digital pin 6.

3. المنطق البرمجي وحساب الوقت (Code Logic and Time Calculation)
بالعربية:

يعتمد الكود على متغير منطقي isSweeping = true للسماح بحركة المسح.

تتكون الحركة من الارتفاع من 0 إلى 180 درجة ثم النزول من 180 إلى 0 درجة بفاصل زمني مقداره 5 مللي ثانية لكل خطوة.

تم حساب الوقت الإجمالي ليكون تقريباً ثانيتين عن طريق ضرب 360 خطوة في 5 مللي ثانية، مما ينتج 1800 مللي ثانية (1.8 ثانية)، ومع إضافة وقت استجابة المحرك الفعلي نصل إلى الثانيتين المطلوبة تماماً.

بعد انتهاء الدورة، يتم تغيير حالة المتغير إلى isSweeping = false لإيقاف المسح للأبد.

أخيراً، يتم تثبيت المحركات عند الزاوية 90 ضمن الشرط else.

يكرر الكود هذا المنطق نفسه للمحركات الثانية والثالثة والرابعة باستخدام المتغيرات servo2 و servo3 و servo4 على التوالي.

In English:

The code relies on a boolean variable isSweeping = true to allow the sweep motion.

The motion consists of increasing from 0 to 180 degrees, then decreasing from 180 to 0 degrees with a 5 ms delay for each step.

The total time is calculated to be approximately two seconds by multiplying 360 steps by 5 ms, resulting in 1800 ms (1.8 seconds), and by adding the actual motor response time, we reach exactly the required two seconds.

After the cycle ends, the variable's state is changed to isSweeping = false to stop the sweep forever.

Finally, the motors are held at the 90-degree angle within the else condition.

The code replicates this exact logic for the second, third, and fourth motors using the servo2, servo3, and servo4 variables respectively.
