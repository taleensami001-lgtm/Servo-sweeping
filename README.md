#### **برمجة 4 محركات سيرفو (Updated Detailed Report: Programming 4 Servo Motors)**
 . لغة ألوان أسلاك السيرفو (Servo Motor Wire Colors)
بالعربية:
يأتي كل محرك سيرفو قياسي مزوداً بثلاثة أسلاك رئيسية، وتختلف وظيفة كل سلك بناءً على لونه لتسهيل عملية التوصيل:

السلك البني (أو الأسود): يمثل الطرف الأرضي (Ground - GND)، وهو ضروري لإكمال الدائرة الكهربائية.

السلك الأحمر: يمثل طرف الطاقة الموجب (VCC)، وعادة ما يتطلب طاقة مقدارها 5 فولت ليعمل المحرك.

السلك البرتقالي (أو الأصفر/الأبيض): يمثل خط الإشارة (Signal)، وهو السلك الذي ينقل النبضات البرمجية والأوامر من الأردوينو إلى المحرك ليخبره بالزاوية المطلوبة.

In English:
Each standard servo motor comes with three main wires, and the function of each wire differs based on its color to facilitate the wiring process:

Brown (or Black) Wire: Represents the Ground (GND), which is essential to complete the electrical circuit.

Red Wire: Represents the positive power pin (VCC) and typically requires a 5V power supply to operate the motor.

Orange (or Yellow/White) Wire: Represents the Signal line, which transmits the programmed pulses and commands from the Arduino to the motor, dictating the required angle.

3. توزيع التوصيلات (Distribution of Connections)
بالعربية:
لتحقيق تحكم مستقل لكل رجل من أرجل الروبوت الأربعة، يتم التوزيع كالتالي:

منافذ الإشارة (Signal): يتم توصيل السلك البرتقالي لكل محرك بمنفذ رقمي مستقل. استناداً إلى المنطق البرمجي، يتم التوصيل في المنافذ الرقمية (6، 7، 8، 9).

توصيل الأرضي (Ground): تتصل جميع الأسلاك البنية بمسار أرضي سالب مشترك.

توصيل الطاقة (Power): تتصل جميع الأسلاك الحمراء بمسار طاقة موجب مشترك.

In English:
To achieve independent control for each of the robot's four legs, the wiring is distributed as follows:

Signal Ports: The orange wire of each motor is connected to an independent digital pin. Based on the code logic, they are connected to digital pins (6, 7, 8, 9).

Ground Connection: All brown wires are connected to a common negative ground path.

Power Connection: All red wires are connected to a common positive power path.
##  **- تخصيص المنافذ للمحركات الأربعة (Pin Allocation for the 4 Motors)**

بدلاً من استخدام محرك واحد، تم توسيع المشروع ليشمل 4 محركات مستقلة، حيث يتم تخصيص كود منفصل ومنافذ مختلفة لكل محرك لضمان التحكم الفردي:
المحرك الثاني (servo2) متصل بالمنفذ الرقمي 8.
المحرك الثالث (servo3) متصل بالمنفذ الرقمي 7.
المحرك الرابع (servo4) متصل بالمنفذ الرقمي 6.


Instead of using a single motor, the project has been expanded to include 4 independent motors, where separate code and distinct pins are allocated for each motor to ensure individual control:
The second motor (servo2) is attached to digital pin 8.
The third motor (servo3) is attached to digital pin 7.
The fourth motor (servo4) is attached to digital pin 6.

 ## **- المنطق البرمجي وحساب الوقت (Code Logic and Time Calculation)**

يعتمد الكود على متغير منطقي isSweeping = true للسماح بحركة المسح.
تتكون الحركة من الارتفاع من 0 إلى 180 درجة ثم النزول من 180 إلى 0 درجة بفاصل زمني مقداره 5 مللي ثانية لكل خطوة.
تم حساب الوقت الإجمالي ليكون تقريباً ثانيتين عن طريق ضرب 360 خطوة في 5 مللي ثانية، مما ينتج 1800 مللي ثانية (1.8 ثانية)، ومع إضافة وقت استجابة المحرك الفعلي نصل إلى الثانيتين المطلوبة تماماً.
بعد انتهاء الدورة، يتم تغيير حالة المتغير إلى isSweeping = false لإيقاف المسح للأبد.
أخيراً، يتم تثبيت المحركات عند الزاوية 90 ضمن الشرط else.
يكرر الكود هذا المنطق نفسه للمحركات الثانية والثالثة والرابعة باستخدام المتغيرات servo2 و servo3 و servo4 على التوالي.


The code relies on a boolean variable isSweeping = true to allow the sweep motion.
The motion consists of increasing from 0 to 180 degrees, then decreasing from 180 to 0 degrees with a 5 ms delay for each step.
The total time is calculated to be approximately two seconds by multiplying 360 steps by 5 ms, resulting in 1800 ms (1.8 seconds), and by adding the actual motor response time, we reach exactly the required two seconds.
After the cycle ends, the variable's state is changed to isSweeping = false to stop the sweep forever.
Finally, the motors are held at the 90-degree angle within the else condition.
The code replicates this exact logic for the second, third, and fourth motors using the servo2, servo3, and servo4 variables respectively.
