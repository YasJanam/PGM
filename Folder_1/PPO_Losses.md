# ppo در الگوریتم  loss انواع 

## 1.policy_loss

این همون بخش اصلی به‌روزرسانی پالیسی است

 از clip objective استفاده می‌کنیم تا آپدیت پالیسی خیلی بزرگ نباشه و باعث ناپایداری نشه

## 2.value_loss

برای تخمین درست ارزش هر وضعیت

## 3.entropy_loss
یک ترم اضافی که باعث میشود پالیسی متنوع‌تر باشد و زود به یک راه‌حل محدود گیر نکند

## نمونه کد محاسبه انواع زیان

    import torch
    import torch.nn.functional as F

    def ppo_loss(
        old_log_probs,       # log-prob های پالیسی قدیمی
        new_log_probs,       # log-prob های پالیسی جدید
        advantages,          # مزیت‌ها (advantage)
        values,              # خروجی critic
        returns,             # ریترن هدف (target value)
        clip_eps=0.2,        # ε در فرمول clip
        c1=0.5,              # وزن value loss
        c2=0.01              # وزن entropy bonus
    ):
        # نسبت احتمالات پالیسی جدید به قدیمی
        ratios = torch.exp(new_log_probs - old_log_probs)

        # --- 1. Policy Loss ---
        unclipped = ratios * advantages
        clipped = torch.clamp(ratios, 1 - clip_eps, 1 + clip_eps) * advantages
        policy_loss = -torch.mean(torch.min(unclipped, clipped))  # منفی چون می‌خوایم ماکسیمم بشه

        # --- 2. Value Function Loss ---
        value_loss = F.mse_loss(values, returns)

        # --- 3. Entropy Bonus ---
        entropy = -torch.mean(new_log_probs.exp() * new_log_probs)  # H(p) = -sum(p*log p)

        # --- Loss نهایی ---
        total_loss = policy_loss + c1 * value_loss - c2 * entropy

        return total_loss, policy_loss.item(), value_loss.item(), entropy.item()


