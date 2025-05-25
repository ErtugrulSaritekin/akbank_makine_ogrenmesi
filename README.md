# Akbank Makine Öğrenmesi Bootcamp - Proje: Iowa Konut Fiyatı Tahmini

**Öğrenci:** Ertuğrul Sarıtekin
NOT: DEĞERLİ OKUYUCU, GITHUB ANLAM VEREMEDİĞİM ŞEKİLDE HATA VERİYOR BİRKAÇ FARKLI ŞEKİLDE  DEĞİŞTİREREK YÜKLEDİM OLMADI BU YÜZDEN SİZİNLE COLAB LİNKİNİ BURADA PAYLAŞIYORUM AYRICA COLAB LİNKİYLE  BURADAKİ ÖDEVİN AYNI OLDUĞUNU BİLGİSAYARINIZA İNDİREREK ANLAYABİLİRSİNİZ SAYGILARIMLA https://colab.research.google.com/drive/1PcZcarcsVbJxn3zQ_l_agCDx0qteRAY4?usp=sharing

## Projeye Genel Bakış

Bu proje, Iowa Konut veri setini kullanarak Ames, Iowa'daki ev fiyatlarını tahmin etmeyi amaçlamaktadır. Bu, çeşitli ev özelliklerine dayanarak `SalePrice` değerini tahmin etmeye çalıştığımız bir regresyon görevidir.



## Metodoloji

1.  **Veri Yükleme ve Keşifsel Veri Analizi (EDA):** Iowa Konut veri seti Kaggle'dan yüklendi. Verinin yapısını, özellik türlerini ve eksik değerleri anlamak için temel keşifsel veri analizi yapıldı.
2.  **Ön İşleme:**
    *   Sayısal özellikler: Eksik değerler medyan stratejisi ile dolduruldu ve ardından `StandardScaler` ile ölçeklendi.
    *   Kategorik özellikler: Eksik değerler en sık kullanılan değer stratejisi ile dolduruldu ve ardından `OneHotEncoder` ile kodlandı.
    *   Bu adımlar bir `ColumnTransformer` içinde birleştirildi.
3.  **Model Seçimi:** Gücü ve karmaşık ilişkileri ele alma yeteneği nedeniyle regresyon modeli olarak `XGBRegressor` seçildi.
4.  **İleri Düzey XGBoost Özellikleri:**
    *   Aşırı öğrenmeyi önlemek ve model karmaşıklığını kontrol etmek amacıyla XGBoost modeline L1 Regülarizasyonu (`reg_alpha=0.1`) ve L2 Regülarizasyonu (`reg_lambda=1.0`) uygulandı.
5.  **Pipeline:** Tüm ön işleme adımları ve XGBoost modeli bir scikit-learn `Pipeline` içinde kapsüllendi.
6.  **Model Eğitimi:** Pipeline, veri setinin eğitim bölümü üzerinde eğitildi.
7.  **Değerlendirme:** Modelin performansı, ayrılmış bir test seti üzerinde Ortalama Mutlak Hata (MAE), Kök Ortalama Kare Hata (RMSE) ve R-kare (R2) metrikleri kullanılarak değerlendirildi.
    *   **Test MAE:** 15245.35
    *   **Test RMSE:** 25113.75
    *   **Test R2 Skoru:** 0.92
8.  **Model Yorumlama:**
    *   **Özellik Önem Düzeyleri:** Modelin tahminlerini en çok etkileyen özellikler belirlendi (örneğin, `num__OverallQual`, `cat__BsmtQual_Ex`, `num__GarageCars`).
    *   **Kısmi Bağımlılık Grafiği (PDP):** Önemli bir özellik olan `OverallQual` ile tahmin edilen satış fiyatı arasındaki ilişki görselleştirildi ve analiz edildi.

## Sonuçlar ve Tartışma

Uygulanan L1 ve L2 regülarizasyonuna sahip XGBoost modeli, test seti üzerinde **0.92 R-kare skoru** elde ederek ev fiyatlarındaki varyansın önemli bir kısmını açıklamıştır. Ortalama Mutlak Hata (MAE) **15245.35** olarak bulunmuştur. Özellik önem düzeyi analizine göre, evin genel kalitesi (`OverallQual`), bodrum kalitesi (`BsmtQual_Ex`) ve garaj kapasitesi (`GarageCars`) fiyatı belirlemede en etkili faktörler olarak öne çıkmıştır. `OverallQual` için çizilen Kısmi Bağımlılık Grafiği, kalite arttıkça ev fiyatının da, özellikle yüksek kalite seviyelerinde daha belirgin olmak üzere, pozitif ve bir miktar doğrusal olmayan bir şekilde arttığını göstermiştir.

Bu proje, gerçek dünya verileri üzerinde uçtan uca bir makine öğrenmesi projesinin nasıl geliştirilebileceğini, XGBoost gibi güçlü bir algoritmanın ileri düzey özelliklerinin nasıl kullanılabileceğini ve model sonuçlarının nasıl yorumlanabileceğini göstermiştir. Daha fazla hiperparametre optimizasyonu veya özellik mühendisliği ile model performansı potansiyel olarak daha da artırılabilir.

## Kullanılan Teknolojiler
*   Python
*   Pandas, NumPy
*   Scikit-learn (Pipeline, ColumnTransformer, SimpleImputer, StandardScaler, OneHotEncoder, metrics)
*   XGBoost (XGBRegressor)
*   Matplotlib, Seaborn (görselleştirme için)
*   Kaggle, GitHub
