# Intel Image Classification Projesi

## 📌 Projenin Amacı
Bu projede, **Intel Image Classification** veri seti kullanılarak 6 farklı sahnenin
(*buildings, forest, glacier, mountain, sea, street*) sınıflandırılması amaçlanmıştır.  

Geliştirilen model, **derin öğrenme tabanlı evrişimsel sinir ağı (CNN)** mimarisi
olan **MobileNetV2** ile transfer learning yaklaşımıyla eğitilmiştir.  
Sonuçların değerlendirilmesi için:  
- Accuracy/Loss grafiklerinin incelenmesi  
- Classification Report ve Confusion Matrix çıktıları  
- Grad-CAM görselleştirmeleri  

eklenmiştir.

---

## 📂 Veri Seti
- Kaynak: [Intel Image Classification (Kaggle)](https://www.kaggle.com/datasets/puneet6060/intel-image-classification)  
- Eğitim: 14.034 görsel  
- Test: 3.000 görsel  
- Görseller 224×224 piksel boyutuna ölçeklenmiştir.  
- Train/Validation/Test ayrımı yapılmıştır (Validation oranı %15).  
- **Veri artırma (Data Augmentation)** teknikleri:  
  - RandomFlip (yansıtma)  
  - RandomRotation (döndürme)  
  - RandomZoom (yakınlaştırma/uzaklaştırma)  

### Veri Görselleştirme
- 3×3 örnek görsel grid  
- Sınıf dağılımı bar grafiği  

---

## 🧠 Model Mimarisi
- Taban model: **MobileNetV2** (ImageNet ön-eğitimli)  
- **Stage-1**: Base katmanlar dondurularak üst katmanlar eğitildi  
- **Stage-2**: Son 30 katman açılarak düşük öğrenme oranı ile fine-tuning yapıldı  
- Katmanlar:  
  - GlobalAveragePooling2D  
  - Dropout  
  - Dense (softmax çıkış)  

### Eğitim Parametreleri
- Optimizer: Adam  
- Loss: SparseCategoricalCrossentropy  
- Callback’ler: EarlyStopping, ReduceLROnPlateau, ModelCheckpoint  
- Epoch: Stage-1 → 8, Stage-2 → 4  

---

## 📊 Değerlendirme
- **Classification Report**: Precision, Recall ve F1-score her sınıf için ayrı ayrı hesaplanmıştır.  
- **Confusion Matrix**: Doğru/yanlış tahminlerin sınıf bazında dağılımı görselleştirilmiştir.  

📌 **Sonuçlar:**
- Test doğruluğu: **%91**  
- En çok karışıklık *glacier* ↔ *mountain* sınıflarında gözlemlenmiştir.  

---

## 🔎 Açıklanabilirlik (Grad-CAM)
- Grad-CAM yöntemi kullanılarak modelin hangi görsel bölgelerden etkilendiği incelenmiştir.  
- Son konvolüsyon katmanından üretilen ısı haritası, orijinal görsellerin üzerine bindirilmiştir.  
- Böylece modelin tahmin yaparken **ilgili bölgelere odaklandığı** gözlemlenmiştir.  

---

## ⚙️ Hiperparametre Denemeleri
Proje kapsamında farklı öğrenme oranları test edilmiştir:  
- Stage-1: 1e-3 (hızlı öğrenme)  
- Stage-2: 1e-5 (düşük LR ile fine-tuning)  

Ayrıca unfreeze depth (son 30 katman) parametresi değiştirilerek validasyon başarımı karşılaştırılmıştır.  

---

## ✅ Sonuç
Bu projede **Intel Image Classification** veri seti üzerinde MobileNetV2 tabanlı
bir derin öğrenme modeli eğitilmiş ve test seti üzerinde %91 doğruluk elde edilmiştir.  

- Modelin başarımı, confusion matrix ve classification report ile detaylı olarak incelenmiştir.  
- Grad-CAM görselleştirmeleri modelin karar mekanizmasını açıklanabilir hale getirmiştir.  

📌 Sonuç olarak, sahne sınıflandırma problemlerinde transfer learning tabanlı CNN
mimarilerinin etkili bir çözüm sunduğu gösterilmiştir.

---

## 🚀 Gelecek Çalışmalar
- Farklı transfer learning modellerinin denenmesi (EfficientNet, ResNet vb.)  
- Daha kapsamlı hiperparametre optimizasyonu (Grid Search, Optuna vb.)  
- Modelin gerçek zamanlı uygulamalara entegrasyonu (ör. mobil cihazlar için TensorFlow Lite)  

---

## 📎 Bağlantılar
- Kaggle Notebook: https://www.kaggle.com/code/bengusucoban/intel-image-classification 
- Kaggle Dataset (ağırlık dosyaları): https://www.kaggle.com/datasets/bengusucoban/bengusucobanintel-mnv2-weights
- GitHub Notebook: [intel_image_classification.ipynb](intel_image_classification.ipynb)
