#### **برمجة 4 محركات سيرفو (Programming 4 Servo Motors)**


## **- لغة ألوان أسلاك السيرفو (Servo Motor Wire Colors)**

يأتي كل محرك سيرفو قياسي مزوداً بثلاثة أسلاك رئيسية، وتختلف وظيفة كل سلك بناءً على لونه لتسهيل عملية التوصيل:
السلك البني (أو الأسود): يمثل الطرف الأرضي (Ground - GND)، وهو ضروري لإكمال الدائرة الكهربائية.
السلك الأحمر: يمثل طرف الطاقة الموجب (VCC)، وعادة ما يتطلب طاقة مقدارها 5 فولت ليعمل المحرك.
السلك البرتقالي (أو الأصفر/الأبيض): يمثل خط الإشارة (Signal)، وهو السلك الذي ينقل النبضات البرمجية والأوامر من الأردوينو إلى المحرك ليخبره بالزاوية المطلوبة.


Each standard servo motor comes with three main wires, and the function of each wire differs based on its color to facilitate the wiring process:
Brown (or Black) Wire: Represents the Ground (GND), which is essential to complete the electrical circuit.
Red Wire: Represents the positive power pin (VCC) and typically requires a 5V power supply to operate the motor.
Orange (or Yellow/White) Wire: Represents the Signal line, which transmits the programmed pulses and commands from the Arduino to the motor, dictating the required angle.

## **- توزيع التوصيلات (Distribution of Connections)**

لتحقيق تحكم مستقل لكل رجل من أرجل الروبوت الأربعة، يتم التوزيع كالتالي:
منافذ الإشارة (Signal): يتم توصيل السلك البرتقالي لكل محرك بمنفذ رقمي مستقل. استناداً إلى المنطق البرمجي، يتم التوصيل في المنافذ الرقمية (6، 7، 8، 9).
توصيل الأرضي (Ground): تتصل جميع الأسلاك البنية بمسار أرضي سالب مشترك.
توصيل الطاقة (Power): تتصل جميع الأسلاك الحمراء بمسار طاقة موجب مشترك.


To achieve independent control for each of the robot's four legs, the wiring is distributed as follows:

Ground Connection: All brown wires are connected to a common negative ground path.

![img alt](https://github.com/taleensami001-lgtm/Servo-sweeping/blob/b2b9721fc5487df7552310389057459f1865f58b/Screenshot%202026-07-11%20143528.png)

power Connection: All red wires are connected to a common positive power path.

![img alt](https://github.com/taleensami001-lgtm/Servo-sweeping/blob/18049bf51908b6e7102063f41813b623ab9c1dbf/Screenshot%202026-07-11%20143557.png)

Signal Ports: The orange wire of each motor is connected to an independent digital pin. Based on the code logic, they are connected to digital pins (6, 7, 8, 9).

![img alt](https://github.com/taleensami001-lgtm/Servo-sweeping/blob/69728d65ed4f01c22d0f5e2dda7f705736ee4749/Screenshot%202026-07-11%20143639.png)

##  **- تخصيص المنافذ للمحركات الأربعة (Pin Allocation for the 4 Motors)**

بدلاً من استخدام محرك واحد، تم توسيع المشروع ليشمل 4 محركات مستقلة، حيث يتم تخصيص كود منفصل ومنافذ مختلفة لكل محرك لضمان التحكم الفردي:
المحرك الثاني (servo2) متصل بالمنفذ الرقمي 8.
المحرك الثالث (servo3) متصل بالمنفذ الرقمي 7.
المحرك الرابع (servo4) متصل بالمنفذ الرقمي 6.


Instead of using a single motor, the project has been expanded to include 4 independent motors, where separate code and distinct pins are allocated for each motor to ensure individual control:
The second motor (servo2) is attached to digital pin 8.
The third motor (servo3) is attached to digital pin 7.
The fourth motor (servo4) is attached to digital pin 6.

![[img alt](https://github.com/taleensami001-lgtm/Servo-sweeping/blob/42cf5ecbdb89a7c6c92a871e62e97878a1b22069/Screenshot%202026-07-11%20182820.png](https://github.com/taleensami001-lgtm/Servo-sweeping/blob/e625d9ed179bab04dbb5b49b11e4ee53ef845de8/Screenshot%202026-07-12%20150319.png)

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

![img alt](https://github.com/taleensami001-lgtm/Servo-sweeping/blob/2a048cb86c7536be1a847417f66b93e282e55fe5/Screenshot%202026-07-12%20150144.png)
![img alt](https://github.com/taleensami001-lgtm/Servo-sweeping/blob/1b69f6d57fef0b934e122391532aca04c026748d/Screenshot%202026-07-12%20150206.png)
![img alt](https://github.com/taleensami001-lgtm/Servo-sweeping/blob/22cda14860629d8a2ff74a08c0ac23642d66488b/Screenshot%202026-07-12%20150251.png)
  
Finally, the motors are held at the 90-degree angle within the else condition.

![img alt](https://github.com/taleensami001-lgtm/Servo-sweeping/blob/5977851e7f107cf9269b56ff91c665585ae27b00/Screenshot%202026-07-12%20150128.png)

## **and here is the code**

#include <Servo.h>

// Define the servo motor

// تعريف محرك السيرفو

Servo servo1;

Servo servo2;

Servo servo3;

Servo servo4;



// Variable to control the sweep motion to stop it after two seconds
//  متغير للتحكم في تشغيل حركة المسح ليتم إيقافها بعد ثانيتين
bool isSweeping = true; 



void setup() {

  
  // To attach the motor to the Arduino pin
  // لربط المحرك بمنفذ الاردوينو
  
  servo1.attach(9);
  
  servo2.attach(8);
  
  servo3.attach(7);
  
  servo4.attach(6);
  
}


void loop() {


 
  // Check if the sweep motion is running
  // التحقق مما إذا كانت حركة المسح تعمل
  
  
  if (isSweeping == true) {
  
    
    // increase from 0 to 180 degrees for all motors together
    
    // الارتفاع من 0 إلى 180 درجة لجميع المحركات معاً
    
    for (int pos = 0; pos <= 180; pos++) {
      
      servo1.write(pos);
      
      servo2.write(pos);
      
      servo3.write(pos);
      
      servo4.write(pos);
      
      
     
      delay(5); 
      
    }
    
    
    // decrease from 180 to 0 degrees for all motors together
    // النزول من 180 إلى 0 درجة لجميع المحركات معاً
   
    for (int pos = 180; pos >= 0; pos--) {
    
      
      servo1.write(pos);
      
      servo2.write(pos);
      
      servo3.write(pos);
      
      servo4.write(pos);
      
      
      
      delay(5);
      
    }
    
    /* How did we calculate the two seconds?
We have 360 steps in the loop (180 up + 180 down).
360 steps * 5 ms delay = 1800 ms (1.8 seconds).
By adding the slight time the motor naturally takes to move,
the cycle will take approximately two seconds exactly as required in the task.
*/

    /* كيف حسبنا الثانيتين؟ 
     لدينا 360 خطوة في حلقة التكرار (180 صعود + 180 نزول).
     360 خطوة × 5 مللي ثانية تأخير = 1800 مللي ثانية (1.8 ثانية).
     بإضافة الوقت الضئيل الذي يستغرقه المحرك فعلياً للحركة، 
     ستستغرق الدورة حوالي ثانيتين تماماً كما هو مطلوب في المهمة.
    */

    
    
    // Stop the sweep motion forever by changing the variable's state
    // إيقاف حركة المسح للأبد بتغيير حالة المتغير
    
    isSweeping = false; 
    
    
  } else {
  
   // After the two seconds end, hold all motors at 90 degrees
   
   //  بعد انتهاء الثانيتين، تثبيت جميع المحركات عند الزاوية 90
    
    servo1.write(90);
    
    servo2.write(90);
    
    servo3.write(90);
    
    servo4.write(90);
    
   
  }
}
