<p align="center">
  <img src="tesla.jpg" width="500" height="500">
</p>

# 🏎️ Tesla Üretim & Teslimat Analizi (2015–2025)

Bu proje, Tesla'nın 2015–2025 yılları arasındaki üretim ve teslimat verilerini kullanarak  
**Estimated_Deliveries** değişkenini birden fazla girdi (özellik) yardımıyla tahmin eden  
basit ama güçlü bir **lineer regresyon** çalışmasıdır.

Veri seti temizdir, eksik veri içermez ve sayısal olarak güçlü bir doğrusal ilişki barındırır.

## 📦 Proje Yapısı
 Tesla-Linear-Regression

├── tesla_lineer.ipynb                    → Tüm analiz ve görselleme adımlarını içeren Jupyter Notebook  
├── tesla_deliveries_dataset_2015_2025.csv → Tesla üretim & teslimat veri seti  
├── README.md                             → Bu doküman  
└── (opsiyonel) görseller
    ├── korelasyon_matris.png             → Korelasyon matrisi heatmap ekran görüntüsü  
    └── scatter_regresyon.png             → Gerçek vs Tahmin scatter grafiği  


---


##  Veri Seti Özeti

| Bilgi | Değer |
|-------|-------|
| Toplam Satır | **2640** |
| Toplam Sütun | **12** |
| Eksik Veri | **0** |
| Kullanılan Değişkenler | Production_Units (X), Estimated_Deliveries (Y) |

### Kullanılan temel kolonlar:

| Sütun | Açıklama |
|-------|----------|
| Production_Units | Tesla üretim adedi (X) |
| Estimated_Deliveries | Tahmini teslimatlar (Y) |

---


## Korelasyon Matrisi Örneği


![Korelasyon Matrisi](korelasyon_matris.png)



---

## 🧪 Uygulanan Veri İşleme Adımları

### 📘 Veri Okuma

```python
df = pd.read_csv("tesla_deliveries_dataset_2015_2025.csv")
```

## 🧠 Veri İnceleme (EDA)

Veri yüklendikten sonra temel inceleme adımları uygulanmıştır:


```python
df.head()
df.info()
df.describe()
```
Bu işlemler ile:
- Veri türleri görüldü
- Eksik veri olmadığı doğrulandı
- Sayısal kolonların dağılımı incelendi
- Modelde kullanacağımız kolonların uygunluğu kontrol edildi

## 🖊️ Eğitim / Test Ayrımı

Modeli daha gerçekçi değerlendirmek için veri eğitim/test olarak ayrıldı:
```
from sklearn.model_selection import train_test_split

X = df[["Production_Units"]]
y = df["Estimated_Deliveries"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```
## Lineer Regresyon Modeli
![Lineer Regresyon](lineer_regresyon.png)





- Veri seti temiz, dengeli ve analiz için idealdir.

- Üretim miktarı, teslimat miktarını yüksek doğrulukta tahmin edebilmektedir.

