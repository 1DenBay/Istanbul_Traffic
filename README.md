# 🚦 İstanbul Trafik Yoğunluğu ve Hız Tahmini

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=for-the-badge&logo=jupyter&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active-green?style=for-the-badge)

Bu proje, İstanbul'un çeşitli lokasyonlarından toplanan sensör verilerini kullanarak trafik akış hızını tahmin eden ve trafik yoğunluğunu sınıflandıran bir **Makine Öğrenmesi (Machine Learning)** projesidir.

Proje; mekansal (GeoHash) ve zamansal (Time-Series) verileri işleyerek hem **Regresyon** (Hız Tahmini) hem de **Sınıflandırma** (Yoğunluk Durumu) modelleri geliştirir.

---

## 📊 Veri Seti

Veri seti `data/` klasörü altında saklanmaktadır. İstanbul Büyükşehir Belediyesi (İBB) Açık Veri Portalı formatlarına uygun sensör verileri kullanılmıştır.

| Sütun Adı                  | Açıklama                                                            |
| :--------------------------- | :-------------------------------------------------------------------- |
| **DATE**               | Verinin alındığı tarih ve saat                                    |
| **GEOHASH**            | Lokasyonun coğrafi kodlaması (Konum ID)                             |
| **MINIMUM_SPEED**      | O periyottaki en düşük araç hızı                                |
| **MAXIMUM_SPEED**      | O periyottaki en yüksek araç hızı                                 |
| **AVERAGE_SPEED**      | **(Hedef 1)** Tahmin edilen ortalama akış hızı              |
| **NUMBER_OF_VEHICLES** | **(Hedef 2)** Sınıflandırma için kullanılan araç sayısı |

---

## 🧠 Modeller ve Yöntemler

### 1. Hız Tahmini (Regression)

* **Amaç:** `AVERAGE_SPEED` değerini tahmin etmek.
* **Dosya:** `traffic_model.ipynb`
* **Kullanılan Modeller:** Linear Regression, Random Forest Regressor, Gradient Boosting.
* **Öne Çıkan Sonuç:** Random Forest, verinin lineer olmayan yapısını (mekansal karmaşıklık) en iyi yakalayan model olmuştur.

### 2. Yoğunluk Sınıflandırması (Classification)

* **Amaç:** Bölgedeki trafik yoğunluğunu `Düşük`, `Orta`, `Yüksek`, `Çok Yüksek` olarak sınıflandırmak.
* **Dosya:** `arac_sinif_tahmini.ipynb`
* **Yöntem:** Araç sayıları "Binning" yöntemi ile kategorize edilip Random Forest Classifier ile eğitilmiştir.

### 3. Veri Analizi (EDA)

* **Dosyalar:** `performans.ipynb`, `zaman.ipynb`
* **İçerik:** Saatlik hız değişimleri, konum bazlı yoğunluk haritaları ve korelasyon analizleri (Heatmap).

---

## 🛠️ Kurulum ve Çalıştırma

Projeyi yerel ortamınızda çalıştırmak için aşağıdaki adımları izleyin:

### 1. Repoyu Klonlayın

```
git clone [https://github.com/1DenBay/Istanbul_Traffic.git](https://github.com/1DenBay/Istanbul_Traffic.git)
cd Istanbul_Traffic
```

### 2. Sanal Ortamı Kurun (Önerilen)

**Bash**

```
python -m venv venv
# Windows:
venv\Scripts\activate
# Mac/Linux:
source venv/bin/activate
```

### 3. Gereksinimleri Yükleyin

**Bash**

```
pip install -r requirements.txt
```

### 4. Projeyi Başlatın

**Bash**

```
jupyter notebook
```

---

## 📂 Proje Yapısı

Veri dosyaları `data/` klasöründe düzenlenmiştir.

**Plaintext**

```
Istanbul_Traffic/
├── data/                     # Veri Setleri
│   ├── birlesik_veri.csv     # İşlenmiş Ana Veri
│   └── data_0.nc             # Ham Geospatial Veriler
│   └── data_0.nc2
│   └── data_0.nc3
│   └── data_0.nc4
├── traffic_model.ipynb       # Hız Tahmini (Regresyon Modeli)
├── arac_sinif_tahmini.ipynb  # Yoğunluk Sınıflandırması (Classification)
├── performans.ipynb          # Model Performans Analizleri
├── zaman.ipynb               # Zamansal Trafik Analizleri
├── requirements.txt          # Gerekli Kütüphaneler
└── README.md                 # Proje Dokümantasyonu
```

## 🤝 Katkıda Bulunma

Pull request'ler kabul edilir. Büyük değişiklikler için önce tartışma başlatınız.

## 👤 İletişim

Bu proje **Deniz BAYAT** tarafından geliştirilmiştir. *-Teşekkürler, Saygılar*

* LinkedIn: linkedin.com/in/denizbayat1/
* GitHub: github.com/1DenBay
* Medium: medium.com/@denizbyat
* Email: [denizbyat@gmail.com](mailto:denizbyat@gmail.com)
