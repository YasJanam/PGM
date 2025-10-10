
# train_with_ppo

## اجزای اصلی کد : 

---
### Class DialoGPTWithValueHead : 

دراین کلاس ما دو مدل داریم.یکی مدل سیاست و یکی مدل ارزش : policy-model , value-model

##### policy-model : همان مدل زبانی ای که میخواهیم آموزشش دهیم

 microsoft/DialoGPT-small مثلا


 تمرکز اصلی الگوریتم روی مدل سیاست است.الگوریتم ppo یک الگوریتم on-policy است.

##### value-model : مدلی که برای ارزش در نظر گرفته ایم بسیار ساده است یک مدل خطی تک لایه 

class-methods : init , forward

---
### Class PPOTrainer : 

در این کلاس انجام میگیرد ppo پیاده سازی الگوریتم 

class-methods : init , compute_advantages , update

##### compute_advantages : متدی برای محاسبه مزیت
یک لیست از ارزش وضعیت ها و اکشن ها به این متد داده میشود و این متد مزیت ها را محاسبه میکند

##### update :  ppo پیاده سازی الگوریتم 

 هسته اصلی کد ->>

          advantages = self.compute_advantages(rewards,values)
          surr1 = ratios*advantages
          surr2 = torch.clamp( ratios,1.0 - self.clip_epsilon ,1.0 + self.clip_epsilon )*advantages
          policy_loss = -torch.min(surr1,surr2).mean()


---
### generate_response Function : 
متدی برای تولید پاسخ

---
### calculate_rewards Function : 

متدی برای محاسبه پاداش

---
### train loop : 
حلقه ای بسیار ساده برای آموزش با تنها 4 پرامپت

در این کد تمرکز بر آموزش است و از دیتاست خاصی براس آموزش استفاده نشده است




