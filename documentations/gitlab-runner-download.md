
## GitLab Runner

### GitLab Runner Nedir?

Özünde, gitlab-ci ile oluşturduğumuz jobları çalıştırmak ve çıktılarını gitlabe geri göndermek için kullanılan açık kaynak bir projedir.

### GitLab Runner Kurulumu Nasıl Yapılır?

1. İlk önce orjinal GitLab Repository'sini sistemimize ekliyoruz.
```sh
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
``` 

2. GitLab Runner projesini serverimize indiriyoruz.
```sh
sudo apt-get install gitlab-runner
```
3. Sıradaki komut ile GitLab Runner versiyonunu kontrol edebiliriz.
```sh
sudo gitlab-runner -version
```

### GitLab Runner Nası Kayıt Edilir?

1. İlk olarak serverimiz üzerine yüklediğimiz GitLab' ın **"Settings"** kısmından **"CI/CD"** kısmına tıklıyoruz.

2. Burada **"Runners"** kısmını Expand ettikten sonra **"Set up a specific runner for a project"** kısmından **"Show runner installation instructions"** kısmına tıklayarak server terminalimiz üzerinden gösterilen adımları tamamlıyoruz.

3. Adımları tamamlarken son adıma geldiğimizde runner'ın konfigürasyon ayarları doğru şekilde seçilmeli. Kullanılacak olan teknolojiye göre executor seçilmeli. Biz burada ssh executor olacak seçeceğiz ve gerekli bilgileri gireceğiz. Server üzerinde bulunan SSH ile buradaki SSH'ın eşlenmesi gerektiğini unutmayalım.

4. Bütün adımları doğru bir şekilde tanımlayınca default ayarlarıyla runner'ımız aktif oluyor.

5. Runner' ın üzerinde bulunan küçük kaleme tıklayarak runner ayarlarını açıyoruz.

6. Bu ekranda ilk olarak işaretleyeceğimiz ayar herhangi bir pipeline dosyasının tagi olmasa dahi runner'ın bu dosyaya otomatik bağlanmasına izin verecek olan **"Indicates whether this runner can pick jobs without tags"** ayarını tiklemek. İsterseniz runner'ınız için description ayarlayabilir, tag ekleyerek spesifik bir pipeline için çalışabilir hale getirebilirsiniz.

7. Eğer herhangi bir runner register etmezseniz yüksek ihtimalle pipeline ekranında **"Stuck"** hatasıyla karşılaşacaksınız çünkü pipeline kendisini koşturacak bir runner bulamayacaktır.

