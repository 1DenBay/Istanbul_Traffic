İstanbul E-5 Trafik Akışı Analizi ve Hız Tahmin Modeli
1. Projeye Genel Bakış
Bu proje, İstanbul'un en işlek arterlerinden biri olan E-5 (D-100) Karayolu'nun Avcılar-Küçükçekmece güzergahına ait, 4 aylık (Temmuz-Ekim 2022) ve 250.000'den fazla kayıttan oluşan sensör verisi üzerinde gerçekleştirilmiş, baştan sona bir veri bilimi çalışmasıdır. Projenin temel amacı, ham ve anonim veriden yola çıkarak trafik desenlerini anlamak, sıkışıklığa neden olan faktörleri tespit etmek ve geleceğe yönelik isabetli tahminler yapabilen bir makine öğrenmesi modeli geliştirmektir.

2. Keşifsel Veri Analizi (EDA) ve Elde Edilen İçgörüler
Analizin bu ilk ve en önemli aşamasında, verinin içindeki gizli hikayeyi ortaya çıkarmak için bir dizi analiz gerçekleştirilmiştir.

Ana Keşifler:
Yolun Çift Karakterli Yapısı: Trafik desenleri incelendiğinde, bu güzergahın sadece bir "işe gidiş-dönüş" yolu olmadığı; hafta içi sabah/akşam piklerine ek olarak, Cumartesi günleri zirve yapan güçlü bir sosyal ve ticari aktivite karakterine sahip olduğu tespit edilmiştir.

Anonim Verilerin Kimliklendirilmesi: Sadece davranışsal verilere (hız, yoğunluk, işgaliye süresi, zamanlama) dayalı analitik bir yaklaşımla, anonim olan araç sınıfları (class_id) ve yol şeritleri (detector_id) yüksek bir isabetle kimliklendirilmiştir:

Araçlar: Otomobil, Motosiklet, Şehir İçi Otobüs, Şehirlerarası Otobüs.

Şeritler: Hızlı Şerit (Sol), Orta Şeritler, Yavaş Şerit (Sağ) ve Yan Yol/Rampa.

Trafik Sıkışıklığının Gizli Dinamiği: Yoğunluk ve hız arasındaki ilişkinin basit bir "yoğunluk artarsa hız düşer" kuralından daha karmaşık olduğu kanıtlanmıştır.

"L" Şeklindeki İlişki: Saçılım grafiği, bu iki değişken arasındaki doğrusal olmayan ilişkiyi ortaya koymuştur.

Kompozisyon Etkisi: Yoğunluk arttıkça ortalama hızın şaşırtıcı bir şekilde yükselebildiği bir anomali tespit edilmiştir. Bu durumun nedeninin, yüksek yoğunluklu pik saatlerde trafiğin "karışık" bir yapıdan (otobüs, kamyon, otomobil bir arada), daha hızlı bir ortalamaya sahip olan "saf" bir otomobil akışına dönüşmesi olduğu kanıtlanmıştır.

Büyük Araçların Etkisinin Ölçülmesi: Ağır vasıtaların (otobüs, kamyon) trafikteki varlığının, otomobillerin ortalama hızını %20 oranında (yaklaşık 18 km/s) düşürdüğü sayısal olarak ölçülmüştür.

3. Makine Öğrenmesi Modeli
Keşifsel analizden elde edilen bu derin içgörüler, gelecekteki trafik hızını tahmin etmeyi amaçlayan bir makine öğrenmesi modeli için temel oluşturmuştur.

3.1. Öznitelik Mühendisliği (Feature Engineering)
Modelin performansını en üst seviyeye çıkarmak için, ham veriden yola çıkarak bir dizi "akıllı ipucu" (öznitelik) oluşturulmuştur:

Temel Özellikler: Saat, gün, ay gibi zaman özellikleri.

İçgörüye Dayalı Özellikler: EDA ile keşfedilen şerit ve araç tipi kimlikleri.

"Hafıza" Özellikleri: Modelin geçmişi hatırlaması için Gecikme (Lag) ve Hareketli Ortalama (Rolling Average) özellikleri.

"Ritim" Özellikleri: Modelin zamanın döngüselliğini anlaması için Sinüs/Kosinüs dönüşümleri ve is_rush_hour gibi etiketler.

3.2. Model Seçimi ve Eğitimi
Model: Karmaşık ve doğrusal olmayan ilişkileri öğrenmedeki başarısı nedeniyle LightGBM (Gradient Boosting) algoritması seçilmiştir.

Eğitim Stratejisi: Modelin geleceği görmesini engelleyerek (veri sızıntısı) performansının doğru ölçülmesi için, veri seti kronolojik olarak Eğitim (Temmuz-Eylül) ve Test (Ekim'den bir kesit) olarak ayrılmıştır.

3.3. Hiperparametre Optimizasyonu
Modelin potansiyelini en üst seviyeye çıkarmak için GridSearchCV tekniği kullanılarak en iyi model ayarları (hiperparametreler) bulunmuştur.

4. Sonuçlar ve Değerlendirme
Tüm bu adımların sonunda, projenin ana hedefine başarıyla ulaşılmıştır.

Nihai Model Performansı:
Metrik

Optimize Edilmiş Model Sonucu

Anlamı

Ortalama Mutlak Hata (MAE)

7.46 km/s

Modelin hız tahminleri, gerçek hızdan ortalama olarak sadece ~7.5 km/s sapmaktadır.

Başarı Oranı (R² Skoru)

0.849

Trafik hızındaki değişkenliğin %84.9'u modelimiz tarafından başarıyla açıklanabilmektedir.

Bu sonuçlar, geliştirdiğimiz modelin, tüm karmaşıklığına rağmen trafik hızını yüksek bir isabet oranıyla tahmin edebildiğini göstermektedir.

5. Kullanılan Teknolojiler
Dil: Python

Kütüphaneler: Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, LightGBM, Xarray
