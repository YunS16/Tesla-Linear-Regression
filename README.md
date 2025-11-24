<p align="center">
  <img src="img/tesla.jpg" width="500" height="500">
</p>

# 🏎️ Tesla Üretim & Teslimat Analizi (2015–2025)

Bu proje, Tesla’nın 2015–2025 yılları arasındaki Quarterly Production ve Estimated Deliveries verilerini kullanarak
“Üretim → Teslimat” ilişkisini analiz eden basit ama öğretici bir lineer regresyon çalışmasıdır.


## 📦 Proje Yapısı
 Tesla-Linear-Regression

├── tesla_lineer.ipynb                    → Tüm analiz ve görselleme adımlarını içeren Jupyter Notebook  
├── tesla_deliveries_dataset_2015_2025.csv → Tesla üretim & teslimat veri seti  
├── README.md                              
└── img(görseller)
    
---
## 📦 Veri Seti Özeti

| Bilgi                  | Değer                                                        |
|------------------------|--------------------------------------------------------------|
| Veri Tipi              | **CSV (Comma-Separated Values)**                             |
| Zaman Aralığı          | **2015 – 2025**                                              |
| Toplam Satır           | **2640**                                                     |
| Toplam Sütun           | **12**                                                       |
| Eksik Veri             | **0**                                                        |
| Kullanılan Değişkenler | `Production_Units` (X), `Estimated_Deliveries` (Y)           |
| Hedef Değişken (Target)| **Estimated_Deliveries**                                     |
| Bağımsız Değişken (Feature)| **Production_Units**                                     |
| Filtre / Temizlik      | Veri seti temiz; ek doldurma veya silme işlemi yapılmadı.   |

---

## 🎯 Projenin Amacı

Bu projede hedef değişken (y) şudur:

Estimated_Deliveries

Bağımsız değişken (X) ise:

Production_Units

Modelin amacı:
"Belirli bir üretim miktarına göre kaç araç teslim edileceğini tahmin etmek."


## 🧼 Veri Temizleme & Hazırlık Adımları

Notebook içinde yapılan veri hazırlığı şunları içerir:

Dataset’in okunması

Sütun isimlerinin kontrol edilmesi

Eksik değer kontrolü

Üretim ve teslimat verilerinin sayısal formatta doğrulanması

Basit EDA (İlk 5 satır / info / describe)

Scatter plot ile doğrusal ilişkinin görselleştirilmesi

Veri seti zaten temiz olduğundan ek bir doldurma veya filtreleme işlemine ihtiyaç duyulmamıştır.


## Korelasyon Matrisi Örneği


![Korelasyon Matrisi](img/korelasyon_matris.png)
```
# Korelasyon matrisi analizinde kullanılacak değişkenlerin seçilmesi
corr = df[['Estimated_Deliveries',
           'Production_Units',
           'Avg_Price_USD',
           'Range_km',
           'Charging_Stations']].corr()

# Korelasyon matrisinin görselleştirmek için
plt.imshow(corr, cmap="coolwarm")
plt.colorbar()
plt.title("Correlation Heatmap")
plt.show()

```
Buradaki kodlar ile korelasyon tablomuzu oluşturduk  
Korelasyon tablosu, üretim ve teslimat sütunları arasında çok yüksek bir doğrusal ilişki bulunduğunu doğrular.
Bu nedenle lineer regresyon modeli için uygun bir veri setidir.

---


## Lineer Regresyon Modeli
![Lineer Regresyon](img/Lineer_regresyon.png)
```
plt.scatter(X_test, y_test)
plt.plot(X_test, y_pred, linewidth=3)
plt.xlabel("Production Units")
plt.ylabel("Estimated Deliveries")
plt.title("Linear Regression Fit")
plt.show()

```
Buradaki kodlar sayesinde lineer regresyon modelimizi oluşturduk  
Model tarafından oluşturulan çizgi, tahmin edilen teslimat değerlerini temsil eder.
Gerçek test verileriyle yakın hizalanması modelin yüksek doğruluğunu gösterir.


## Sonuç

Bu proje kapsamında, Tesla’nın 2015–2025 yılları arasında kaydettiği üretim ve teslimat verileri incelenmiş ve iki değişken arasındaki ilişki lineer regresyon modeli kullanılarak detaylı şekilde analiz edilmiştir. Verilerin hem sayısal yapısı hem de doğrusal dağılımı, doğrusal bir modelin bu probleme uygun olduğunu güçlü biçimde göstermiştir.   
Sonuç olarak bu çalışma, Tesla’nın üretim hacmindeki artışın teslimat sayıları üzerinde doğrusal ve güçlü bir etkisi olduğunu açıkça ortaya koymaktadır. Kullanılan model, hem öğretici hem de pratik bir makine öğrenimi uygulaması olarak proje amacını başarıyla karşılamış ve anlamlı tahminler üretmiştir.

Bu proje, gerçek dünya verilerinin analizinde temel ML yöntemlerinin ne kadar etkili olabileceğini gösteren yalın ama etkili bir örnek niteliği taşımaktadır.

<p align="center">
  <img src="img/tesla_car.png" width="500" height="500">
</p>

