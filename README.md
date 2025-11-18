# Tesla Üretim & Teslimat Analizi (2015–2025)

Bu proje, Tesla'nın 2015–2025 yılları arasındaki üretim ve teslimat verilerini kullanarak
**Production_Units → Estimated_Deliveries** ilişkisini inceleyen basit bir lineer regresyon çalışmasıdır.

Veri seti temizdir, eksik veri içermez ve sayısal olarak güçlü bir doğrusal ilişki barındırır.

---

## 📌 Proje İçeriği

Aşağıdaki işlem adımları uygulanmıştır:

- Veri setinin okunması  
- İlk inceleme (EDA)  
- Scatter plot ile ilişki kontrolü  
- Eğitim/Test ayrımı  
- Lineer regresyon modeli kurulumu  
- Modelden elde edilen metriklerin hesaplanması  
- Sonuçların yorumlanması  

---

## 📦 Veri Seti Özeti

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

## 📊 Scatter Plot (X → Y İlişkisi)

Tesla üretim ve teslimat arasındaki ilişki aşağıdaki grafikte gösterilmektedir:

<p align="center">
  <img src="analysis_result_1.png" width="600px">
</p>

### **Grafik Yorumu**
- Noktalar neredeyse düz bir çizgi üzerinde  
- Üretim arttıkça teslimat da artıyor  
- Bu, **çok güçlü bir doğrusal ilişki** olduğuna işaret ediyor  

---

## 🧪 Uygulanan Veri İşleme Adımları

### ✔ Veri Okuma

```python
df = pd.read_csv("tesla_deliveries_dataset_2015_2025.csv")
