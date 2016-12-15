---
layout: post
title: R কিকস্টার্টার - ০২ R ও RStudio ইন্সটলেশন
---
Windows, Linux ও Mac তিনটি অপারেটিং সিস্টেমের জন্যই R এর প্রি-কম্পাইল্ড বাইনারি ভার্সন পাওয়া যায়। আপনাকে যেটা করতে হবে সেটা হল প্রথমেই CRAN এর ওয়েবসাইটে যেতে হবে – https://cran.r-project.org/ , এরপর আপনি নিচের ছবির মত ইন্টারফেস দেখতে পাবেন-

![alt text](https://raw.githubusercontent.com/abdalimran/abdalimran.github.io/master/images/r-install-01.png "Install R")

**Windows এ R ইন্সটলেশনঃ** আপনি যদি Windows ব্যবহারকারি হন তাহলে Download R for Windows এ ক্লিক করুন। এরপর base এ ক্লিক করুন, সেখানে Download R for Windows বাটনে ক্লিক করে ইন্সটলেশন ফাইলটি ডাউনলোড করে নিন। এরপর  ইন্সটলেশন ফাইলটিতে ডাবল ক্লিক করে অন্য সব সফটওয়্যারের মত নেক্সট নেক্সট ক্লিক করে ইন্সটল করে ফেলুন। ব্যস R ইন্সটল হয়ে গেল আপনার সিস্টেমে। এরপর আপনি উইন্ডোজ বাটনে ক্লিক করে R লিখে সার্চ করলে R’এর আইকন ওয়ালা একটি এপ্লিকেশন দেখতে পাবেন। ডাবল ক্লিক করে এপ্লিকেশনটি ওপেন করুন। এটি হল R এর GUI এপ্লিকেশন। শুধুমাত্র উইন্ডোজ ইউজারদের জন্য R’এর এই GUI এডিটরটি পাওয়া যায়। লিনাক্সের জন্য নেই। আপনি চাইলে এখনি এই এপ্লিকেশনের এডিটরে R প্রোগ্রামিংয়ে কোড করা শুরু করে দিতে পারেন, তবে আমরা এই এপ্লিকেশনে R প্রোগ্রামিং করবো না। আমরা আরো সুন্দর ইন্টেয়ারফেসের, আরো অ্যাডভান্সড IDE, RStudio ব্যবহার করবো। IDE কি, IDE ব্যবহারের সুবিধা কি কি তা না জানলে গুগোল করে জেনে নিতে পারেন।

**Ubuntu তে R ইন্সটলেশনঃ** উবুন্তুতে R ইন্সটলেশন আরো সহজ। প্রথমে Ctrl+Alt+T চেপে টার্মিনাল্টি ওপেন করুন। এরপর টার্মিনালে সিরিয়ালি নিচের কমান্ড গুলো রান করান-

আপনি যদি উবুন্টু ১৪.০৪ ব্যবহার করেন তাহলে – `sudo echo "deb http://cran.rstudio.com/bin/linux/ubuntu trusty/" | sudo tee -a /etc/apt/sources.list`

কিংবা যদি উবুন্টু ১৬.০৪ ব্যবহার করেন তাহলে – `sudo echo "deb http://cran.rstudio.com/bin/linux/ubuntu xenial/" | sudo tee -a /etc/apt/sources.list`

এখন আবার টার্মিনালে নিচের কমান্ড গুলো দিন-

```javascript
gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9
gpg -a --export E084DAB9 | sudo apt-key add -
sudo apt-get update
sudo apt-get install r-base r-base-dev
```

ব্যাস কাজ শেষ! আপনার উবুন্টুতে R ইন্সটল হয়ে গেল। এবার টার্মিনালে R লিখে Enter চাপ দিন, তাহলেই R ওপেন হয়ে যাবে। এখানেই আপনি R এর কোড লিখতে পারবেন। তবে উবুন্টুর জন্য R ডিফল্ট ভাবে কোন GUI ইন্টারফেস দেয় না। তাই আমরা RStudio তে কোড করবো।

**RStudio ইন্সটলেশনঃ** R ইন্সটল করার পর এবার আমরা RStudio ইন্সটল করবো।
প্রথমেই [https://www.rstudio.com/products/rstudio/download2/](https://www.rstudio.com/products/rstudio/download2/) এই লিঙ্কে ক্লিক করে RStudio’র ওয়েবসাইটের ডাউনলোড পেইজে যান। এরপর আপনার অপারেটিং সিস্টেমের আর্কিটকচার অনুযায়ী (৩২/৬৪ বিট) Studio’র ইন্সটলেশন ফাইলটি ডাউনলোড করুন এবং সাধারণ ভাবে ইন্সটলার ফাইলটিতে ডাবল ক্লিক করে RStudio ইন্সটল করে ফেলুন।
এরপর RStudio এপ্লিকেশনটি ওপেন করুন। ওপেন করলে নিচের মত একটি ইন্টারফেস দেখতে পাবেন।

![alt text](https://raw.githubusercontent.com/abdalimran/abdalimran.github.io/master/images/r-install-02.png "Install RStudio")

আমাদের R প্রোগ্রামিং এর সকল এনভায়রনমেন্ট সেট করা শেষ। আপনি যদি এরপর সফলভাবে R ও RStudio ইন্সটল করতে না পারেন তাহলে youtube এ সার্চ করে দেখে নিন ঠিক ভাবে ইন্সটল করে ফেলুন।

নেক্সট পোস্ট থেকেই আমরা RStudio তে R প্রোগ্রামিং এর কোড লিখা শুরু করবো ইনশাল্লাহ। :smile:
