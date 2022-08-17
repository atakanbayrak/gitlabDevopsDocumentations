## Pipeline Nedir?

GitLab Pipeline kısaca CI/CD süreçlerini otomatikleştiren bir konfigürasyon dosyasıdır. Tabii ki bu tanım çok yüzeysel bir tanımdır ancak temel olarak kafamızda ne olduğunu oluşturabilmek için yeterli olacaktır.

### Pipeline Nasıl Kullanılır?

1. İlk olarak projemizin merkez klasöründe **".gitlab-ci.yml"** uzantılı ve isimli dosyamızı oluşturmak. İsim ve uzantı aynı olmalı!

2. YML dosyalarının kendine ait bir syntax'ı bulunmakta bu yüzden biz de belirli kurallara uymalıyız.

3. Aşağıda göreceğiniz şekilde basit bir demo oluşturabiliriz.

```sh
stages:
  - build
  - test
build:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    - echo "Kod buil ediliyor"
    - dotnet build
    - echo "Build işlemi tamamlandı"

test:   # This job runs in the test stage.
  stage: test    # It only starts when the job in the build stage completes successfully.
  script:
      - dotnet test 
```

4. Bu kod bloğu basit bir şekilde dotnet projemizi build edip ardından eğer varsa proje dosyaları içerisindeki test dosyasını çağırıp çalıştıracak.

5. Bu şekilde dosyamızı kaydedip commit yaptıktan sonra hemen sayfanın üstünde göreceğiniz üzere pipeline'ımız otomatik olarak çalışmaya başlayacak.

6. Şuan yazılan kurallara göre ne zaman master dosyamıza bir commit yaparsak pipeline dosyamız çalışacak.

7. Eğer **"CI/CD"** ekranından **"Pipelines"** sekmesine tıklarsanız burada bulunduğunuz proje için bu zamana kadar oluşturulan pipeline'ları görebilir ayrıca ayrıntılarına bakıp hataları veya logları inceleyebilirsiniz. 
