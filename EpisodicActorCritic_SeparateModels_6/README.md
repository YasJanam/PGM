## EpisodicActorCritic_SeparateModels
پیاده سازی الگوریتم actor-critic به شکل episodic. (نسخه آنلاینش هم هست)   
مدل های actor , critic جدا هستن. دو روش برای پیاده سازی مدل های actor , critic وجود داره. یکی اینکه shared باشن؛ یعنی کلا یک مدل داریم با دو head. یک head برای actor و یک head برای critic.  
روش دیگه به صورت SeparateModels هستش. یعنی مدل های actor , critc کاملا جدا هستن.(چیزی در این کد استفاده شده)   

#### ActorCriticTrainer
کلاس ActorCriticTrainer الگوریتم actor-critic رو پیاده میکند. در این کلاس یک متد هست با نام  ComputeMeanGrad که برای محاسبه میانگین گرادیان های مدل استفاده میشود. کاربردش این هست که چک کنیم ببینیم مدل مورد نظر آموزش میبینه یا نه. در واقع این متد جنبه لاگ گیری داره و در پیاده سازی الگوریتم actor-critic نقشی نداره. فقط برای اینه که چک کنیم ببینیم یادگیری انجام میشه یا نه. 

در این کد یک بار actor-critic دستی پیاده شده و یک بار با کتابخونه stable-baselines3.
