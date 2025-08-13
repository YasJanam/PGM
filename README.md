# PPO1
الگوریتم ppo  در حال حاضر پرکاربردترین الگوریتم RL است.این الگوریتم یک الگوریتم on_policy , actor-critic  است.

# actor-critic
 در الگوریتم های actor-critic دو شبکه اصلی داریم : policy-Network , value-Network

 شبکه policy ( همون actor ) : یادگرفتن استراتژی

 شبکه value ( همون critic ): تخمین مقدار ارزش حالت فعلی

# خلاصه گام ها در ppo 

1-جمع کردن داده ها از محیط (rollout) با سیاست فعلی

2-تخمین ارزش ( critic) و محاسبه advantages

3-آپدیت critic با MSE

4-تکرار برای چند epoch , سپس rollout جدید

# ویژگی های کلی ساختار actor-critic

1-یادگیری مبتنی بر مزیت ( advantage-Based learning ) -> یادگیری پایدارتر

2-از بین رفتن بیش برازش با clipping

3- تابع مزیت ( advantage function ) : درک مفهوم مزیت 

# Advantage Function

مزیت نشان دهنده انتخاب یک اکشن در یک وضعیت خاص نسبت به میانگین پاداش است.

__A(s,a) =  Q(s,a) - V(s)__

V(s) = state-value function   :  ارزش یک وضعیت

Q(s,a) = Action-value function : یعنی ارزش انتخاب یک اکشن در یک وضعیت

A(s,a) = Advantage : مزیت انتخاب یک اکشن در یک وضعیت

