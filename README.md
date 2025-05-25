# Akbank-Bootcamp
URL dataseti (benign url, defacement url, phishing url, malware url) üzerinde KNN ve Random Forest gözetimli öğrenme algoritmaları kullanarak makine öğrenmesi yapıldı.


# Giriş
Veri seti olarak https://www.kaggle.com/datasets/sid321axn/malicious-urls-dataset linkindeki url veri setini kullandık. 
Veri seti url ve type olarak 2 sütuna sahip olup 641119 satırdan oluşuyor.

Aldığımız url verilerini extract_features fonksiyonu ile 'url_length', 'domain_length', 'path_length', 'num_dots', 'num_slashes', 'is_https', 'num_params' özelliklerine ayırdık ve bu özellikler için yeni sütunlar oluşturduk. 

Eklediğimiz özelliklerin verisini daha rahat görmek ve yorumlayabilmek için de grafik analizleri yaptık.

LabelEncoder ile veri setimizdeki type türlerini sayısal veriye dönüştürdük.

0-benign tipi, 1-defacement tipi, 2-malware tipi ve 3-phishing tipi ifade ediyor.

X verisine url ve type sütununu drop ederek tablomuzu yükledik Y verisine de type sütununu yükledik. Bu verileri %80 eğitim ve %20 test olacak şekilde ayırdık.

**İlk olarak KNN gözetimli öğrenme algoritmasını kullandık.**

'url_length', 'domain_length', 'path_length', 'num_dots', 'num_slashes', 'is_https', 'num_params' özelliklerimizin KNN algoritması için önemini belirledik ve görselleştirdik. Bunun sonucunda en önemli özelliğimizin 'domain_length' ve en önemsiz özelliğimizin 'is_https' olduğunu gördük. (!!!Etiketleme hataları nedeniyle is_https özelliği istatistiksel olarak düşük önemde görünse de, gerçek dünyadaki güvenlik önemi nedeniyle veri setinde tutulmuştur. Hatalar giderildiğinde model performansına katkısı artacaktır.)

GridSearch kullanarak KNN algoritmasının bizim verimiz için en iyi doğruluk oranını veren hiperparametrelerini öğrendik ve bu hiperparametreler ile KNN algoritmamızı gerçekledik.

KNN algoritması için Confusion Matrix görselleştirmesi yaptık. 

**İkinci olarak Random Forest gözetimli öğrenme algoritmasını kullandık.**

'url_length', 'domain_length', 'path_length', 'num_dots', 'num_slashes', 'is_https', 'num_params' özelliklerimizin Random Forest/ algoritması için önemini belirledik ve görselleştirdik. KNN algoritmasında olduğu gibi bunun sonucunda da en önemli özelliğimizin 'domain_length' ve en önemsiz özelliğimizin 'is_https' olduğunu gördük. (!!!Etiketleme hataları nedeniyle is_https özelliği istatistiksel olarak düşük önemde görünse de, gerçek dünyadaki güvenlik önemi nedeniyle veri setinde tutulmuştur. Hatalar giderildiğinde model performansına katkısı artacaktır.)

RandomSearch kullanarak Random Forest algoritmasının bizim verimiz için en iyi doğruluk oranını veren hiperparametrelerini öğrendik ve bu hiperparametreler ile Random Forest algoritmamızı gerçekledik.

Random Forest algoritması için Confusion Matrix görselleştirmesi yaptık.

# Metrikler

**KNN sonuçları**

Öncelikle özelliklerimiz için önem grafiği oluşturduk. Çıktısı aşağıdaki resimde olup etiketleme hatalarından dolayı en önemsiz özellik is_https gibi gözükse de teknik olarak böyle olmaması gerekiyor.
![KNNOnemGrafigi](https://github.com/melihdedeoglu1/Akbank-Bootcamp/blob/main/images/knn_onem.png?raw=true)

GridSearch ile verilerimiz için en iyi hiperparametreleri ve en iyi doğruluğu elde ettik.
![KNNEnIyiGrafigi](https://github.com/melihdedeoglu1/Akbank-Bootcamp/blob/main/images/knn_eniyi.png?raw=true)

Elde ettiğimiz en iyi hiperparametreleri modeli eğitirken kullandık ve model için sınıflandırma raporu elde ettik.
![KNNSonuclarGrafigi](https://github.com/melihdedeoglu1/Akbank-Bootcamp/blob/main/images/knn_sonuclar.png?raw=true)

Elde edilen bu verilerde de görüldüğü gibi toplam 130.239 test örneğinde %91.35 doğruluk elde ettik. özellikle Benign sınıfında yüksek başarı sağlandı (F1-skoru: 0.95). En düşük olan Phishing sınıfı ise model tarafından diğer sınıflara göre daha düşük doğrulukla sınıflandırılmış (F1-skoru: 0.70, recall: 0.62). Modelimiz bu sınıfa ait örneklerin örüntü benzerliklerinden dolayı bazı Phishing sınıfına ait özellikleri gözden kaçırdığı anlamına geliyor.


Modelimizin Confiuson Matrix'ini görselleştirdik.

![KNNConfusionGrafigi](https://github.com/melihdedeoglu1/Akbank-Bootcamp/blob/main/images/knn_confusion.png)

Sınıflandırma raporundaki Phishing sınıfına ait F1-skorunun neden az çıktığı bu grafikte belli oluyor. Modelimiz Phishing sınıfını Benign olarak sınıflandırmış ve bu da Phishing doğruluğunu düşürüyor. Bu duruma çözüm önerisi olarak Phishing örnekleri eklemenin model doğruluğuna katkıda bulunabileceğini düşünüyoruz.



**Random Forest Sonuçları**

Öncelikle özelliklerimiz için önem grafiği oluşturduk. Çıktısı aşağıdaki resimde olup etiketleme hatalarından dolayı en önemsiz özellik is_https gibi gözükse de teknik olarak böyle olmaması gerekiyor.
![RandomForestOnemGrafigi](https://github.com/melihdedeoglu1/Akbank-Bootcamp/blob/main/images/rf_onem.png?raw=true)

RandomSearch ile verilerimiz için en iyi hiperparametreleri ve en iyi doğruluğu elde ettik.
![RandomForestEnIyiGrafigi](https://github.com/melihdedeoglu1/Akbank-Bootcamp/blob/main/images/rf_eniyi.png?raw=true)

Elde ettiğimiz en iyi hiperparametreleri modeli eğitirken kullandık ve model için sınıflandırma raporu elde ettik.
![RandomForestSonuclarGrafigi](https://github.com/melihdedeoglu1/Akbank-Bootcamp/blob/main/images/rf_sonuclar.png?raw=true)

Elde edilen bu verilerde de görüldüğü gibi toplam 130.239 test örneğinde %92.3 doğruluk elde ettik. Benign ve Defacement sınıflarında yüksek başarı sağlandı (F1-skoru: 0.95). En düşük olan Phishing sınıfı ise model tarafından diğer sınıflara göre daha düşük doğrulukla sınıflandırılmış (F1-skoru: 0.74, recall: 0.69). Modelimiz bu sınıfa ait örneklerin örüntü benzerliklerinden dolayı bazı Phishing sınıfına ait özellikleri gözden kaçırdığı anlamına geliyor.


Modelimizin Confiuson Matrix'ini görselleştirdik.

![RandomForestConfusionGrafigi](https://github.com/melihdedeoglu1/Akbank-Bootcamp/blob/main/images/rf_confusion.png)

Sınıflandırma raporundaki Phishing sınıfına ait F1-skorunun neden az çıktığı bu grafikte belli oluyor. Modelimiz Phishing sınıfını Benign olarak sınıflandırmış ve bu da Phishing doğruluğunu düşürüyor. Bu duruma çözüm önerisi olarak Phishing örnekleri eklemenin model doğruluğuna katkıda bulunabileceğini düşünüyoruz.


# Sonuç ve Gelecek Çalışmalar
*    Projemizde de belirtttiğimiz gibi mevcut veri setimizde, bazı URL'ler aslında HTTPS olmasına rağmen bu durum göz ardı edilerek yanlış şekilde etiketlenmiş. Yani, verideki HTTPS olup olmadığı bilgisinin doğru şekilde yansıtılmadığı örnekler mevcut. Bu nedenle, modelin öğrenme sürecinde is_https özelliğinin önemi istatistiksel olarak düşük görünmektedir.HTTPS'in güvenlik açısından kritik bir faktör olduğunu ve URL'nin güvenli olup olmadığını belirlemede önemli bir rol oynadığını düşünüyoruz.Modeli yeniden eğitmeden önce, yanlış etiketlenmiş HTTPS verilerini düzelmek için manuel etiketleme veya veri temizliği işlemleri yapılabilir. Sonrasında, is_https özelliğini daha doğru bir şekilde modelin öğrenme sürecine dahil etmek, modelin performansını artırabilir.
*    modelimiz günlük hayatta kullanılabilmesi için bir web arayüzü geliştirilebilir.
*    modelimiz için daha farklı algoritmalar denenebilir
# Linkler
* **Umut Kuzyaka** [https://www.kaggle.com/code/umutkuzyaka/akbankproject](https://www.kaggle.com/code/umutkuzyaka/akbank-project)

* **Melih Dedeoğlu**  https://www.kaggle.com/code/melihdedeolu/akbankproject
* googlecollab https://colab.research.google.com/drive/1bIpJRqvGnbfGHDvIYNA7sqB7Hsyh0bLD#scrollTo=M4rRoc4Ek1mg

