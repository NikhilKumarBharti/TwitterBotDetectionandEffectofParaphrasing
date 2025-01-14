# Does Paraphrasing Affect Bot Detection?
Nikhil Kumar Bharti and Koustav Rudra
# Introduction
<p>Nowadays, the presence of bots, or automated programs, is becoming increasingly commonplace on the internet. Bots on social media, especially, hamper the user experience in many ways. The bots may spread false information, fake news, spam, affect political campaigns or any other form of nuisance. Some bots may be created for malicious purposes, which also includes stealing user information.</p>
<p>Because of these reasons, developers and moderators need to employ the use of bot detectors to combat the trouble caused by the bots. As a result, bot creators use different tactics to evade bot detection algorithms. To mimic human behaviour, bot creators use paraphrasing. In paraphrasing, the text is rephrased by using synonyms, voice-change, or changing sentence structure to keep its overall meaning intact. This becomes especially difficult for the bot-detection algorithms as they cannot correctly identify whether a tweet is written by a human or a bot. In this project, we aim to analyze if paraphrasing has any effects on bot-detection algorithm. We consider a dataset containing tweets written by both humans and bots.</p>

# Analysis
We develop an LSTM-based approach to identify whether a tweet is written by a human or a bot. We consider two different setups
<p>
* Setup 1: In the first setup, we only consider tweets as a feature, and do not consider any metadata and try to identify whether it is written by a human or a bot. To check the role of paraphrasing, we paraphrase the test data using OpenAI's davinci model. Note that: We just paraphrase the test data, not the training data, to check the performance of the bot-detection algorithms under paraphrased version. In figure 1, the red bars indicate the performance on original test data, and the green bars indicate the performance on paraphrased data.
</p>
<p>
  Setup 2: In the second setup, along with tweet we also consider two metadata: the location of the user and whether the user is verified. Similar to the first setup, we check the performance of original test data and the paraphrased test data.
</p>
<p>
  Setup 3: Here, we have considered only tweet text as a feature. But, instead of paraphrasing the entire test set, we just paraphrase the tweets written by bots. Tweets written by humans remain unaltered.
</p>
<p>
  Setup 4: This is similar to Setup 3, but we consider two metadata (location, verification status) along with the text, as the features.
</p>
<p>
  Setup 5: Here, we have considered only tweet text as a feature. But, instead of paraphrasing the entire test set, we just paraphrase the tweets written by humans. Tweets written by bots remain unaltered.
</p>
<p>
  Setup 6: This is similar to Setup 5, but we consider two metadata (location, verification status) along with the text, as the features.
</p>

![label0_1feat](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/83082700-60fb-426b-9f85-470ce81b5b72)
![label1_1feat](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/bfc601b4-6906-42b4-9d10-731b06e88c1c)

Figure 1: Comparison of performance of the bot detection model of bot written tweets under Setup 1 (text): The performance has dropped by 1.1% due to paraphrasing

![label0_3feat](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/b5c8ef94-a02b-44e8-8cb4-6eeabd236f0e)
![label1_3feat](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/195dc8d2-4405-4f71-911a-e121f6e2ede7)

Figure 2: Comparison of performance of the bot detection model of bot written tweets under Setup 2 (text+metadata): The performance has dropped by 1.55% due to paraphrasing

![label0_1feat_setup3](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/cc9d2528-5003-4901-9268-d349fb47467a)
![label1_1feat_setup3](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/1e0855e3-32ce-4215-9520-8963073e836c)

Figure 3: Comparison of performance of the bot detection model of bot written tweets under Setup 3 (text): The performance has increased by 0.32% due to paraphrasing

![label0_3feat_setup3](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/e639058c-5627-4282-8de5-9a6380d1dd97)
![label1_3feat_setup3](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/58f87505-0268-4e0e-b4da-c66f6e1c6b81)

Figure 4: Comparison of performance of the bot detection model of bot written tweets under Setup 4 (text+metadata): The performance has dropped by 0.52% due to paraphrasing


![label0_1feat_setup5](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/fe50f26d-1dad-4ea4-bb72-0a721939b601)
![label1_1feat_setup5](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/fa37a07b-67a3-4d97-a65c-1303c7ce155a)

Figure 5: Comparison of performance of the bot detection model of bot written tweets under Setup 5 (text): The performance has dropped by 1.42% due to paraphrasing

![label0_3feat_setup6](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/2e4a0511-f4d2-4f9a-b81d-e8686905b3ce)
![label1_3feat_setup6](https://github.com/NikhilKumarBharti/TwitterBotDetectionandEffectofParaphrasing/assets/88152449/decf00e4-7fd3-4da3-ab7b-c9f405e93507)

Figure 6: Comparison of performance of the bot detection model of bot written tweets under Setup 6 (text+metadata): The performance has dropped by 1.03% due to paraphrasing

As a general trend, we observe a decrease in Precision and Recall and F1-Score after paraphrasing. This trend can have the following reasons:

*Re-phrasing a text can lead to some information loss. The original sentence contains vital information or structure that may be lost after paraphrasing, leading to misclassification. E.g., ‘tiny adventures of tiny astronauts injected into @x's tiny star fields. by @y’ is a tweet originally by a bot. Still, its paraphrased version, ‘@y introduced the small journeys of little astronauts into @y's small star fields.’ breaks the effect of alliteration present in the original tweet, leading it to get misclassified as a human tweet.
*Paraphrasing can introduce noise or other variations that make it harder for the bot detection model to distinguish between human written and bot generated content. After paraphrasing, the output may result in grammar or structural changes, leading to incorrect classification.  E.g., in one of the cases, the original tweet is ‘Good life, good health, good work.’, and its paraphrased version is ‘Living well, being in good health, and having a successful job’. Here, we see that work can have different interpretations, whereas the paraphrased version narrows the meaning to ‘job’. Adding extra phrases in the paraphrased version might confuse the model to misclassify the tweet as written by a bot.

# Conclusion
<p>In this project, we analysed the effect paraphrasing on bot detection. It turns out that paraphrasing could be used to fool the bot detection models. Further research and better models will serve towards a better future in ensuring a hassle-free user experience and better access to information.</p>

# Acknowledgement
<p>This work is supported by the Science and Engineering Research Board, Department of Science and Technology, Government of India, under Project SRG/2022/001548.</p>


