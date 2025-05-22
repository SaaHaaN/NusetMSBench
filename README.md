
# 🧠 Medical Image Segmentation with ResNet18-UNet (MedSegBench)

Bu proje, **tıbbi görüntü segmentasyonu** için PyTorch kullanılarak oluşturulmuş bir derin öğrenme modelini içerir. Kullanılan model, ResNet18 temelli encoder ile UNet yapısını birleştirerek **MedSegBench** veri kümesi üzerinde segmentasyon görevi yapmaktadır.

---

## 📁 İçerik

- [Tanıtım](#-tanıtım)
- [Kullanılan Teknolojiler](#-kullanılan-teknolojiler)
- [Kurulum](#-kurulum)
- [Veri Kümesi](#-veri-kümesi)
- [Model Mimarisi](#-model-mimarisi)
- [Eğitim Detayları](#-eğitim-detayları)
- [TensorBoard Takibi](#-tensorboard-takibi)
- [Sonuçlar](#-sonuçlar)
- [Kaynakça](#-kaynakça)

---

## 📌 Tanıtım

Bu projede MedSegBench veri kümesinde segmentasyon yapılmıştır. Model, ResNet18 encoder ve UNet decoder yapısıyla tasarlanmıştır. Amaç, segmentasyon çıktısını mask olarak elde etmek ve doğruluğu çeşitli metriklerle değerlendirmektir.

---

## ⚙️ Kullanılan Teknolojiler

- Python 3.x
- PyTorch
- torchvision
- numpy
- matplotlib
- scikit-learn
- TensorBoard
- MedSegBench (veri kümesi)

---

## 🚀 Kurulum

- Gerekli bağımlılıkları yükleyin:
   ```bash
   pip install -r requirements.txt
   ```

> `requirements.txt` içeriği:
```txt
torch
torchvision
numpy
matplotlib
scikit-learn
tqdm
tensorboard
```

---

## 📂 Veri Kümesi

Bu projede [MedSegBench - NuSet](https://medsegbench.github.io/) bulunan 'NusetMSBench' veri kümesi kullanılmaktadır. `NusetMSBench` sınıfı ile veri otomatik olarak indirilmektedir. Görseller 256x256 olarak ölçeklendirilmiş ve her biri tek-kanal (grayscale) formatındadır.

---

## 🧩 Model Mimarisi

Model, ResNet18 encoder ve UNet tarzı bir decoder'dan oluşmaktadır. Skip-connection yapıları kullanılarak detay bilgileri korunmaktadır.

```python
class ResNet18_UNet(nn.Module):
    ...
```

---

## 📊 Eğitim Detayları

- Kayıp Fonksiyonu: `DiceLoss`
- Optimizasyon: `Adam`, öğrenme oranı `1e-4`
- Epoch sayısı: `150`
- Batch size: `8`
- Değerlendirme: Doğruluk (Accuracy), F1, IOU, Precision, Recall

---

## 📉 TensorBoard Takibi

TensorBoard üzerinden loss, accuracy ve görsel karşılaştırmalar izlenebilir:

```bash
tensorboard --logdir=./logs/NusetMSBenchDiceLoss
```

TensorBoard'da hem giriş hem de segmentasyon çıktıları her 5 epoch'ta bir görselleştirilmiştir.

---

## ✅ Sonuçlar

- Model performansı hem eğitim hem de validasyon için kaydedilmektedir.
- En iyi validasyon kaybına sahip model, `./checkpoints` klasörüne kaydedilir.
- Epoch sonuçları `Odev2_BCE.txt` dosyasına yazılır.

---

## 📚 Kaynakça

- [MedSegBench - NuSet](https://medsegbench.github.io/)
- [U-Net Paper](https://arxiv.org/abs/1505.04597)
- [ResNet Paper](https://arxiv.org/abs/1512.03385)
- [PyTorch Documentation](https://pytorch.org/)
