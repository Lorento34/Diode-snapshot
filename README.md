# Diode-snapshot


1- Geçici verileri temizleyip düğümün yedek dosyasını alın. Yedek dosyasını aldıktan sonra çıktıda ```1_diode-node_v1.6.5_278``` gibi dosyanın adı yazar. Burada önemli olan kısım yedek dosyasının en başında ki rakamdır. Bu kurulum için önemlidir çünkü orada ki rakama göre kurulum yapılıyor.  

```Mask
diode-node.flush && sudo snap stop diode-node && sudo snap save diode-node
```

2- Düğümünüzün sadece yedeğini alıyorsanız ```/var/lib/snapd/snapshots/``` dosya yoluna gidin. Snapshots klasörüne gidip, yedek dosyasını Pc'nize yedekleyin.

3- Düğümünüzün yedeğini alıp yeni bir sunucuya hemen düğüm kuracaksanız o zaman aşağıda ki adımları takip edebilirsiniz.

> [!CAUTION]
> - Taşımaa yapacağınız yeni sunucuda ki ```Snapshots``` klasörünü kontrol edin eğer ```/var/lib/snapd/snapshots/``` dizini mevcut değilse aşağıda kikomutu ile oluşturun. Ya da FTP/SFTP Termius, WinSCP vb. uygulamaları ile yeni sunucuya bağlanıp ```Snapshots``` klasörünü manuel olarak oluşturabilirsiniz.

```Processing
sudo mkdir -p /var/lib/snapd/snapshots
``` 
> - Yeni sunucuda ki ```/var/lib/snapd/snapshots/``` dosya yolunu oluşturduktan sonra yedek dosyasını yeni sunucuya aktarabilirsiniz.

```AMPL
scp /var/lib/snapd/snapshots/1_diode-node*.zip root@IpAdresiniz:/var/lib/snapd/snapshots/
```
> [!CAUTION]
> 
> Yukarıda ki komutta ki ```root@IpAdresiniz``` kısmına kendi ip adresinizi yazın.
> 
> Sunucuya ilk kez bağlanıyorsanız ```Are you sure you want to continue connecting (yes/no)?``` diye soracaktır; ```yes``` yazıp Enter’a basın.
> 
> Yedek dosyasının aktarılacağı sunucusunun root şifresi isteyecek; doğru şifreyi girdikten sonra aktarım başlar.

4- Düğümü kullanmaya devam etmek istiyorsanız o zaman düğümü yeniden başlatın. Eğer düğümünü kullanmayacaksanız ya da farklı bir sunucuya taşayacaksanız o zaman bu adımı geçebilirsiniz.

```Mask
sudo snap start diode-node
```





























