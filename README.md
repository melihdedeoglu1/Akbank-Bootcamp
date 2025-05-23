# Akbank-Bootcamp
URL dataseti (benign url, defacement url, phishing url, malware url) üzerinde KNN ve Random Forest gözetimli öğrenme algoritmaları kullanarak makine öğrenmesi yapıldı.


#Giriş
Veri seti olarak https://www.kaggle.com/datasets/sid321axn/malicious-urls-dataset linkindeki url veri setini kullandık. 
Veri seti url ve type olarak 2 sütuna sahip olup 641119 satırdan oluşuyor.

Aldığımız url verilerini extract_features fonksiyonu ile 'url_length', 'domain_length', 'path_length', 'num_dots', 'num_slashes', 'is_https', 'num_params' özelliklerine ayırdık ve bu özellikler için yeni sütunlar oluşturduk. 

Eklediğimiz özelliklerin verisini daha rahat görmek ve yorumlayabilmek için de grafik analizleri yaptık.

LabelEncoder ile veri setimizdeki type türlerini sayısal veriye dönüştürdük.

X verisine url ve type sütununu drop ederek tablomuzu yükledik Y verisine de type sütununu yükledik. Bu verileri %80 eğitim ve %20 test olacak şekilde ayırdık.

---İlk olarak KNN gözetimli öğrenme algoritmasını kullandık.

'url_length', 'domain_length', 'path_length', 'num_dots', 'num_slashes', 'is_https', 'num_params' özelliklerimizin KNN algoritması için önemini belirledik ve görselleştirdik. Bunun sonucunda en önemli özelliğimizin 'domain_length' ve en önemsiz özelliğimizin 'is_https' olduğunu gördük. (!!!Etiketleme hataları nedeniyle is_https özelliği istatistiksel olarak düşük önemde görünse de, gerçek dünyadaki güvenlik önemi nedeniyle veri setinde tutulmuştur. Hatalar giderildiğinde model performansına katkısı artacaktır.)

GridSearch kullanarak KNN algoritmasının bizim verimiz için en iyi doğruluk oranını veren hiperparametrelerini öğrendik ve bu hiperparametreler ile KNN algoritmamızı gerçekledik.

KNN algoritması için Confusion Matrix görselleştirmesi yaptık. 

---İkinci olarak Random Forest gözetimli öğrenme algoritmasını kullandık.

'url_length', 'domain_length', 'path_length', 'num_dots', 'num_slashes', 'is_https', 'num_params' özelliklerimizin Random Forest/ algoritması için önemini belirledik ve görselleştirdik. KNN algoritmasında olduğu gibi bunun sonucunda da en önemli özelliğimizin 'domain_length' ve en önemsiz özelliğimizin 'is_https' olduğunu gördük. (!!!Etiketleme hataları nedeniyle is_https özelliği istatistiksel olarak düşük önemde görünse de, gerçek dünyadaki güvenlik önemi nedeniyle veri setinde tutulmuştur. Hatalar giderildiğinde model performansına katkısı artacaktır.)

RandomSearch kullanarak Random Forest algoritmasının bizim verimiz için en iyi doğruluk oranını veren hiperparametrelerini öğrendik ve bu hiperparametreler ile Random Forest algoritmamızı gerçekledik.

Random Forest algoritması için Confusion Matrix görselleştirmesi yaptık.

#Metrikler
...

#Sonuç ve Gelecek Çalışmalar
...

#Linkler
...

