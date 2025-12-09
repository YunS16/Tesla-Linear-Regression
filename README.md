<p align="center">
  <img src="img/tesla.jpg" width="500" height="500">
</p>


# 🏎️ Tesla Üretim & Teslimat Analizi (2015–2025)

Bu proje, Tesla’nın 2015–2025 yılları arasında yayımladığı *Production_Units* ve *Estimated Deliveries* verilerini kullanarak  
**üretim hacminin teslimat sayıları üzerindeki etkisini inceleyen bir lineer regresyon çalışmasıdır.**

Amaç, belirli bir çeyrekte üretilen araç sayısına bakarak Tesla’nın tahmini teslimat performansını matematiksel olarak modellemektir.  
 
Bu çalışma; veri analizi, görselleştirme ve makine öğrenimi temellerini bir araya getirerek  
Tesla’nın üretim–teslimat dinamiklerini istatistiksel olarak ortaya koymayı hedeflemektedir.  


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

---


### b) “Kullanılan Kütüphaneler”


## 📦 Kullanılan Kütüphaneler

- `pandas` – Veri okuma ve veri çerçevesi işlemleri
- `numpy` – Sayısal hesaplamalar
- `matplotlib` / `seaborn` – Veri görselleştirme
- `scikit-learn` – Regresyon modelleri ve metrikler


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



## 📋 Korelasyon Matrisi


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

---


## 📈 Lineer Regresyon Modeli
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

## 📌 Model Seçimi

Tesla’nın 2015–2025 yılları arasındaki üretim (Production Units) ve tahmini teslimat (Estimated Deliveries) verileri incelendiğinde iki değişken arasında **yüksek pozitif doğrusal ilişki** bulundu.

Bu nedenle ilk olarak:

- **Lineer Regresyon** modeli temel bir yaklaşım olarak seçildi.

Ancak modelin doğrusal olmayan ilişkileri yakalayıp yakalayamadığını görmek için ek olarak şu modeller de denendi:

- **Polinomsal Regresyon (degree=2)**
- **Random Forest Regresyon**

Amaç; farklı modellerin performanslarını karşılaştırarak **hangi modelin Tesla verisini en iyi açıkladığını belirlemekti.

## 🧠 Model Karşılaştırması (Lineer – Polinomsal – Random Forest)

Tesla’nın üretim verilerinden teslimat tahmini yapılırken toplam **3 farklı makine öğrenimi modeli** test edilmiştir:

- **Lineer Regresyon**
- **Polinomsal Regresyon (degree = 2)**
- **Random Forest Regresyon**

Amaç, bu modellerin performanslarını karşılaştırarak **hangi modelin en doğru sonucu verdiğini belirlemektir.**

---

### 📘 1. Modellerin Eğitim Kodları

#### 🔹 Lineer Regresyon
```python
lr_model = LinearRegression()
lr_model.fit(X_train, y_train)
lr_pred = lr_model.predict(X_test)
```
```
poly = PolynomialFeatures(degree=2)
X_train_poly = poly.fit_transform(X_train)
X_test_poly = poly.transform(X_test)
```
### Polinomsal Regresyon (degree = 2)
```
poly_model = LinearRegression()
poly_model.fit(X_train_poly, y_train)
poly_pred = poly_model.predict(X_test_poly)
```
### Random Forest Regresyon
```
rf_model = RandomForestRegressor(
    n_estimators=200,
    random_state=42
)
rf_model.fit(X_train, y_train)
rf_pred = rf_model.predict(X_test)
```
## 2. Model Performans Sonuçları
![model_sonuc](img/sonuc.png)

## 3. Model Yorumları
## 📌 Model Seçimi

Tesla’nın 2015–2025 yılları arasındaki üretim (Production Units) ve tahmini teslimat (Estimated Deliveries) verileri incelendiğinde iki değişken arasında **yüksek pozitif doğrusal ilişki** bulundu.

Bu nedenle ilk olarak:

- **Lineer Regresyon** modeli temel bir yaklaşım olarak seçildi.

Ancak modelin doğrusal olmayan ilişkileri yakalayıp yakalayamadığını görmek için ek olarak şu modeller de denendi:

- **Polinomsal Regresyon (degree=2)**
- **Random Forest Regresyon**

Amaç; farklı modellerin performanslarını karşılaştırarak **hangi modelin Tesla verisini en iyi açıkladığını belirlemekti.

## 🧠 Model Karşılaştırması (Lineer – Polinomsal – Random Forest)

Tesla’nın üretim verilerinden teslimat tahmini yapılırken toplam **3 farklı makine öğrenimi modeli** test edilmiştir:

- **Lineer Regresyon**
- **Polinomsal Regresyon (degree = 2)**
- **Random Forest Regresyon**

Amaç, bu modellerin performanslarını karşılaştırarak **hangi modelin en doğru sonucu verdiğini belirlemektir.**

---

### 📘 1. Modellerin Eğitim Kodları

#### 🔹 Lineer Regresyon
```python
lr_model = LinearRegression()
lr_model.fit(X_train, y_train)
lr_pred = lr_model.predict(X_test)
```
```
poly = PolynomialFeatures(degree=2)
X_train_poly = poly.fit_transform(X_train)
X_test_poly = poly.transform(X_test)
```
### Polinomsal Regresyon (degree = 2)
```
poly_model = LinearRegression()
poly_model.fit(X_train_poly, y_train)
poly_pred = poly_model.predict(X_test_poly)
```
### Random Forest Regresyon
```
rf_model = RandomForestRegressor(
    n_estimators=200,
    random_state=42
)
rf_model.fit(X_train, y_train)
rf_pred = rf_model.predict(X_test)
```
## 2. Model Performans Sonuçları
![model_sonuc](img/sonuc.png)

## 3. Model Yorumları
✔️ Lineer Regresyon

Basit ve hızlıdır

Güçlü doğrusal ilişkiyi iyi yakalar

Karmaşık yapıyı modellemek sınırlıdır

✔️ Polinomsal Regresyon (d=2)

Doğrusal olmayan ilişkileri daha iyi modeller

Lineer modele göre daha düşük hata verdi

Bu projede en yüksek doğruluğa sahip model olmuştur

✔️ Random Forest Regresyon

Karmaşık ilişkileri öğrenebilir

Aykırı değerlerden daha az etkilenir

Ancak bu veri setinde Polinomsal Regresyon kadar iyi performans göstermemiştir

## Model Sonuç
Veri analizine göre değişkenler arasında güçlü bir doğrusal ilişki bulunduğu için ilk model olarak Lineer Regresyon denenmiştir.
Daha sonra doğruluğu artırmak amacıyla Polinomsal Regresyon ve Random Forest modelleri test edilmiştir.

Karşılaştırma sonuçlarına göre en iyi performans, en düşük hata ve en yüksek R² değeri Polinomsal Regresyon (degree=2) modeline aittir.

Bu nedenle proje sonucunda en başarılı model Polinomsal Regresyon olarak seçilmiştir.

## Model Sonuç

Veri analizine göre değişkenler arasında güçlü bir doğrusal ilişki bulunduğu için ilk model olarak Lineer Regresyon kullanıldı.
Daha sonra model performansını artırmak amacıyla Polinomsal Regresyon ve Random Forest modelleri de denenmiş, bu karşılaştırma sonucunda en düşük hata değerini Random Forest modelinin verdiği görülmüştür

## 💯Genel Sonuç

Bu proje kapsamında, Tesla’nın 2015–2025 yılları arasında kaydettiği üretim ve teslimat verileri incelenmiş ve iki değişken arasındaki ilişki lineer regresyon modeli kullanılarak detaylı şekilde analiz edilmiştir. Verilerin hem sayısal yapısı hem de doğrusal dağılımı, doğrusal bir modelin bu probleme uygun olduğunu güçlü biçimde göstermiştir.   

Sonuç olarak bu çalışma, Tesla’nın üretim hacmindeki artışın teslimat sayıları üzerinde doğrusal ve güçlü bir etkisi olduğunu açıkça ortaya koymaktadır. Kullanılan model, hem öğretici hem de pratik bir makine öğrenimi uygulaması olarak proje amacını başarıyla karşılamış ve anlamlı tahminler üretmiştir.

Bu proje, gerçek dünya verilerinin analizinde temel ML yöntemlerinin ne kadar etkili olabileceğini gösteren yalın ama etkili bir örnek niteliği taşımaktadır.

<p align="center">
  <img src="img/tesla_car.png" width="500" height="500">
</p>

