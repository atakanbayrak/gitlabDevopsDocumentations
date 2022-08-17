## Unit Test Nedir?

Unit Test, bir yazılımın en küçük test edilebilir bölümlerinin, tek tek ve bağımsız olarak doğru çalışması için incelendiği bir yazılım geliştirme sürecidir. Unit Test yazılım testinin ilk seviyesidir ve entegrasyon testinden önce gelir. Unit Testleri geliştiriciler kendileri yazar ve yürütürler.

### Nasıl Unit Test Yazılır?

1. İlk olarak unit test yazmak istediğimiz projeninin temel solution dosyasına **"xUnitTest Projesi"** ekliyoruz. 

2. Eklediğimiz proje dosyasının bağımlılık kısmına kontrol etmek istediğimiz metodların bulunduğu sınıfın bağımlılığını ekliyoruz. Böylece içerisindeki methodları kontrol etmemiz çok daha kolaylaşacak.

3. Unit testler 3 kısımdan oluşmakta. Bunlar Arrange,Act,Assert kısımlarıdır. Arrange kısmında testimiz için gerekli sınıfımızı oluşturup kodlarımızı hazır hale getiririz. Act kısmında oluşturduğumuz kodları çalıştırıp verileri test içerisine yolladığımız kısımdır. Assert kısmı ise bu gönderdiğimiz veriler ve beklediğimiz değerlerin kıyaslandığı kısımdır.

4. Gerekli testlerimizi yazdıktan sonra Visual Studio üzerinde bulunan **"Test"** sekmesinden **"Testleri Çalıştır"** seçeneğine tıklayarak testimizi ilk önce Visual Studio üzerinde deniyoruz. 

5. Bu adımdan sonra proje dosyalarımızı git aracılığıyla server içerisinde bulunan GitLab üzerine yüklüyoruz. 

6. Pipeline ayarlarımızı aşşağıdaki gibi yapıyoruz.

```sh
stages:          # List of stages for jobs, and their order of execution
  - build
  - test

build-job:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    - dotnet build

unit-test-job:   # This job runs in the test stage.
  stage: test    # It only starts when the job in the build stage completes successfully.
  before_script:
      - echo "Test için dizin aranacak!"
  script:
      - dotnet test 
  after_script:
      - echo "Test işlemi tamamlandı."
```
7. Bu pipeline devreye girdiği andan itibaren ilk önce projemizi build edecek ardından **"dotnet test"** komutu çalıştığında proje klasörümüzün içerisinde test projeslerini aramaya başlayacak. Zaten bu arama işlemlerinin yapıldığının takibini pipeline ekranında görebiliriz. Ardından bulduğu test projelerini çalıştırıp kodumuzu otomatik bir şekilde test etmemize olanak sağlamış olacak.

8. Bu adımdan sonra **"YML"** dosyasının içerisinde yapılacak her değişiklik tamamen projenin isteklerine göre ayarlanabilir.
