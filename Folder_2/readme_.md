# dialogpt_ppotrainer
## خلاصه کلی عناصر کد : 
### class ChatbotEnv

پیاده سازی محیط چت بات

متدی از این کلاس که فرآیند یادگیری بر اساس آن انجام میشود : _calculate_reward

معمولا مدل به سمتی پیش میرود که پاداش دریافتی در هر گام بیشتر شود

_calculate_reward : این متد بسیار ساده است.زیرا هدف در این کد پیاده سازی الگوریتم بوده است 

### class ValueNetwork

یک شبکه عصبی با دو لایه خطی
### class PPOTrainer

در این کلاس انجام میگیرد ppo پیاده سازی الگوریتم 

ppo قلب الگوریتم : 

    surr1 = ratios*advantages
    surr2 = torch.clamp(ratios,1-self.clip_eps,1+self.clip_eps)*advantages
    policy_loss = -torch.min(surr1,surr2).mean()
    value_loss = F.mse_loss(values , rewards)
    loss = policy_loss + value_loss

### حلقه آموزش : Rollout + train

کل فرآیند آموزش 10 ایپاک است.در هر ایپاک 100 بار جمع آوری داده میکنیم

1 epoch - > 100 rollout
