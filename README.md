![diode_logo](https://github.com/user-attachments/assets/15666d10-1cf9-4a4a-82ee-e838088f6016)

Bu rehber, Diode düğümünüzün (Node) kritik verilerini korumak ve beklenmedik arızalar, sunucu taşımaları veya format işlemleri sonrasında hızlı bir şekilde geri dönebilmeniz için yedek (snapshot) alma ve geri yükleme adımlarını detaylı bir şekilde anlatmaya yardımcı olmak için hazırlandı. Düzenli yedek alarak; veri kaybı riskini en aza indirebilir, bakım ve yükseltme süreçlerini kesintisiz tamamlayabilir ve oluşabilecek aksaklıklardan etkilenmeden düğümünüzü çalışır tutabilirsiniz.

------

1- Geçici verileri temizleyip düğümün yedek dosyasını alın. Yedek dosyasını aldıktan sonra çıktıda ```1 diode-node  5.31s  v1.6.5   278  33.9MB``` gibi bilgiler çıkacak. Burada önemli olan kısım  ```Set``` seçeneğini altında yer alan, yedek dosyasının en başında ki rakamdır. Bu kurulum için önemlidir çünkü orada ki rakama göre kurulum yapılıyor.  

```Mask
diode-node.flush && sudo snap stop diode-node && sudo snap save diode-node
```

![image](https://github.com/user-attachments/assets/d11f073f-341a-4cb4-958e-91af1f94cd22)


2- Düğümü kullanmaya devam etmek istiyorsanız o zaman düğümü yeniden başlatın. Eğer kullanmayacaksanız ya da düğümü farklı bir sunucuya taşayacaksanız o zaman bu adımı geçebilirsiniz.

```Mask
sudo snap start diode-node
```

3- Düğümünüzün sadece yedeğini alıyorsanız ```/var/lib/snapd/snapshots/``` dosya yoluna gidin. Snapshots klasörüne gidip, yedek dosyasını Pc'nize yedekleyin.


## Geri Yükleme İşlemi

Düğümünüzün yedeğini alıp, yeni bir sunucuya hemen kuracaksanız o zaman aşağıda ki adımları takip edebilirsiniz.

1- Taşıma yapacağınız yeni sunucuda ki ```Snapshots``` klasörünü kontrol edin. Eğer ```/var/lib/snapd/snapshots/``` dizini mevcut değilse aşağıda ki komutu ile oluşturun. Ya da FTP/SFTP Termius, WinSCP vb. uygulamaları ile yeni sunucuya bağlanıp ```/var/lib/snapd/``` dosya yoluna giderek ```Snapshots``` klasörünü manuel olarak oluşturabilirsiniz.

```Processing
sudo mkdir -p /var/lib/snapd/snapshots
```

2- Yedek dosyasını yeni sunucuya taşımak için 2 seçeneğiz var. Sizin için hangisi kolaysa onu kullanabilirsiniz. Yeni sunucuda ki ```/var/lib/snapd/snapshots/``` dosya yolunu oluşturduktan aşağıda ki adımları takip edin.

<b>Birinci seçenek:</b> Düğümün kurulu olduğu eski sunucunun terminalinde aşağıda ki komutu çalıştırarak yedeği yeni sunucuya aktarabilirsiniz.

```AMPL
scp /var/lib/snapd/snapshots/1_diode-node*.zip root@IpAdresiniz:/var/lib/snapd/snapshots/
```

> [!CAUTION]
> - ```1_diode-node``` yedek dosyasının başında ki rakam yedek alırken ```Set``` kısmının alınta yazan rakamdır sizde farklılık gösterebilir, sizde ne yazdıysa o rakamı kullanın.
> - Yukarıda ki komutta ```root@IpAdresiniz``` kısmına kendi ip adresinizi yazın.
> - Sunucuya ilk kez bağlanıyorsanız ```Are you sure you want to continue connecting (yes/no)?``` diye soracaktır; ```yes``` yazıp Enter’a basın.
> - Yedek dosyasının aktarılacağı sunucusunun root şifresi isteyecek; doğru şifreyi girdikten sonra aktarım başlar.

<b>İkinci seçenek:</b> FTP/SFTP Termius, WinSCP vb. uygulamaları ile yeni sunucuya bağlanın. Pc'nizde bulunan yedek dosyasını ```/var/lib/snapd/snapshots/``` dosya yoluna giderek ```snapshots``` klasörünün içerisine kopyalayabilirsiniz.

3- Yedek dosyası yeni sunucuya taşıdıktan sonra Diode düğümünü kurun.

```AL
sudo snap install diode-node
```

4- Yedek dosyasını yüklemeden önce düğümü durdurun.

```ABAP
sudo snap stop diode-node
```

5- Yedek dosyasını yükleyin. Yedek dosyasının önüne ekleyeceğiz rakam yedek dosyası alırken ```Set``` kısmının alınta yazan rakamdır. Yani sizin aldığınız yedek dosyasının en başında yazan rakama göre aşağıda ki komutu kendizine göre düzenlemeniz gerekiyor.

```Mask
sudo snap restore 1 diode-node
```

![image](https://github.com/user-attachments/assets/e283eaaf-9cd9-4eab-983d-deaa29c18a49)


6- Düğümünüzü yeniden başlatın

```Mask
sudo snap start diode-node
```











