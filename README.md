# Spor Salonu Yoğunluk Analizi ve Tahmini 

Bu proje, çeşitli zamansal ve çevresel faktörlere dayanarak bir spor salonundaki kişi sayısını analiz eden ve tahmin eden bir Makine Öğrenmesi projesidir. Bu projenin amacı, spor salonu kullanım alışkanlıklarındaki eğilimleri anlamak ve herhangi bir saatte spor salonunda bulunacak kişi sayısını tahmin edebilecek bir regresyon modeli oluşturmaktır. Proje; Keşifçi Veri Analizi (EDA), Veri Ön İşleme, Model Eğitimi ve Hiperparametre Optimizasyonu adımlarını içeren bir veri bilimi sürecini kapsamaktadır.

## Veri Seti Bilgileri
Veri seti (`gym_crowdedness.csv`), spor salonunun geçmiş doluluk verilerini içerir. Veri setindeki temel özellikler (features) şunlardır:
* **Hedef Değişken (Target):** `number_people` (Spor salonundaki kişi sayısı)
* **Zamansal Özellikler:** `date` (tarih), `day_of_week` (haftanın günü), `month` (ay), `hour` (saat), `is_weekend` (hafta sonu mu?), `is_holiday` (tatil mi?)
* **Hava Durumu Özelliği:** `temperature` (sıcaklık)
* **Akademik Takvim:** `is_start_of_semester` (dönem başı mı?), `is_during_semester` (dönem içi mi?)

## Proje İş Akışı

### 1. Veri Ön İşleme (Data Preprocessing)
* Tarih/Zaman verileri işlendi: `date` sütunu UTC Datetime nesnelerine dönüştürüldü ve `year` (yıl) bilgisi yeni bir sütun olarak çıkarıldı.
* Veri sızıntısını (data leakage) ve gereksiz karmaşıklığı önlemek için modele katkısı olmayan `date` ve `timestamp` sütunları düşürüldü.
* Makine öğrenmesi modellerinin performansını artırmak amacıyla özellikler `StandardScaler` kullanılarak ölçeklendirildi.

### 2. Keşifçi Veri Analizi (EDA)
Verilerdeki eğilimleri ve ilişkileri bulmak için `Seaborn` ve `Matplotlib` kullanılarak çeşitli görselleştirmeler yapıldı:
* **Çizgi Grafikleri:** Saatlere göre ortalama kişi sayısındaki değişim.
* **Çubuk ve Kutu Grafikleri:** Haftanın günlerine, tatillere ve üniversite dönemi takvimine göre yoğunluk analizi.
* **Regresyon Grafiği:** Sıcaklık ile spor salonu doluluğu arasındaki ilişki.
* **Isı Haritası (Heatmap):** Tüm sayısal özelliklerin birbiriyle olan korelasyon matrisi.

### 3. Makine Öğrenmesi Modelleri
Aşağıdaki çeşitli regresyon algoritmaları eğitilmiş ve performansları test edilmiştir:
* Linear Regression (Doğrusal Regresyon)
* Lasso Regression
* Ridge Regression
* K-Neighbors Regressor (KNN)
* Decision Tree Regressor (Karar Ağaçları)
* Random Forest Regressor (Rastgele Orman)

**Kullanılan Değerlendirme Metrikleri:** Root Mean Squared Error (RMSE), Mean Absolute Error (MAE) ve R² Score.

### 4. Hiperparametre Optimizasyonu
En iyi performans gösteren modeller (KNN ve Random Forest) için optimum parametreleri bulmak amacıyla `RandomizedSearchCV` kullanılmıştır.

**En İyi Model Performansı:**
**Random Forest Regressor** modeli (`n_estimators=500` ve `max_features=7` parametreleri ile) veri setinde en başarılı sonuçları elde etmiştir:
* **Test R² Skoru:** ~0.92
* **Test RMSE:** ~6.42
* **Test MAE:** ~4.29
