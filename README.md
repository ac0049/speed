# CSS preload used in theme(impluse)
```
<link rel="preload" as="style" href="{{ 'theme.css' | asset_url }}">
or
{{ 'theme.css' | asset_url | stylesheet_tag: preload: true }}
<script src="{{ 'theme.js' | asset_url }}" defer="defer"></script>
```
# CSS preload 1
```

<link rel="preload" href="{{ 'theme.css' | asset_url }}" as="style">
<script>
function onLoadStylesheet() {
    var url = "{{ 'theme.css' | asset_url }}";
    var link = document.querySelector('link[href="' + url + '"]');
    link.loaded = true;
    link.dispatchEvent(new Event('load'));
}
</script>

<link rel="stylesheet" href="{{ 'theme.css' | asset_url }}" type="text/css" media="print" onload="this.media='all';onLoadStylesheet()">
```
# JS preload
```
<link rel="preload" href="{{ 'theme.css' | asset_url }}" as="style">
<link rel="preload" href="{{ 'modernizr-2.8.2.min.js' | asset_url  }}" as="script">
```
# CLS issue - set image width and height
```
<script>
  const images = document.querySelectorAll('.rte--indented-images img')
    images.forEach((image) => {
     image.width = image.clientWidth;
     image.height = image.clientHeight
  });
</script>
```

# speed 1

## theme.liquid
```
<!-- JS minifed file extension should be *.js not min.js -->
{% comment %}
    {{ content_for_header }}
  {% endcomment %}
  {{ content_for_header | replace : "addEventListener('load'", "addEventListener('wnw_load'" | replace : "previewBarInjector.init();", "" | replace : 'DOMContentLoaded', 'wnw_load' | replace : 'defer="defer" src=', 'type="lazyload2" defer="defer" data-src=' }}
  <script>var trekkie=[];trekkie.integrations=!0;</script>
  
  <link rel="stylesheet" data-href="{{ 'theme.css' | asset_url }}" type="text/css">
  <script type="lazyload2" data-src="{{ 'custom.js' | asset_url }}" defer></script>
<script type="lazyload2">
....
</script>
  
  ...
  {% render 'optimize-code' %}
  
  
```

## optimize-code.liquid
```
 <script type="text/javascript">
  var windowWidth,lazyLink,lazyImages,lazySource,lazyBackground,lazyIframe,lazyScripts,navigator_platform,lazyLoadedJS,src,style,datasrc,urls,analytics,s,x,i,j,flag;
  function init(){flag&&(flag=0,lazyLoadImg(),lazyLoadBackground(),lazyLoadIframe(),lazyLoadSource(),load_all_js())}
  function isElementInViewport(t){
    var a=t.getBoundingClientRect();
    return a.top>=0&&a.left>=0&&a.bottom<=(window.innerHeight||document.documentElement.clientHeight)&&a.right<=(window.innerWidth||document.documentElement.clientWidth)
  }
  function insertAfter(newNode, referenceNode) {
    referenceNode.parentNode.insertBefore(newNode, referenceNode.nextSibling);
  }
  function isElementInView(t){
    var a=t.getBoundingClientRect();
    return a.top<(window.innerHeight/2||document.documentElement.clientHeight/2) && a.bottom>(window.innerHeight/2||document.documentElement.clientHeight/2)
  }
  function lazyLoadLink(){
    lazyLink.forEach(function(t){
      if(t.href=='') t.href=null==t.dataset.href?t.href:t.dataset.href
    })
  }
  function lazyLoadImg(){
    lazyImages.forEach(function(t){
      null!=(src=windowWidth<600?null==t.dataset.mobsrc?t.dataset.src:t.dataset.mobsrc:t.dataset.src)&&(t.src=src),t.classList.remove("lazy2")
    })
  }
  function lazyLoadImg2(){
    lazyImages.forEach(function(t){
      isElementInViewport(t)&&(null!=(src=windowWidth<600?null==t.dataset.mobsrc?t.dataset.src:t.dataset.mobsrc:t.dataset.src)&&(t.src=src),t.classList.remove("lazy"))
    })
  }
  function lazyLoadSource(){
    lazySource.forEach(function(t){
      t.srcset=null==t.dataset.srcset?t.srcset:t.dataset.srcset
    })
  }
  function lazyLoadBackground(){
    lazyBackground.forEach(function(t){
      lazybg=windowWidth<768?null==t.dataset.mobstyle?t.dataset.style:t.dataset.mobstyle:t.dataset.style,null!=lazybg&&(t.style=lazybg),t.classList.remove("lazybg")
    })
  }
  function lazyLoadIframe(){
    lazyIframe.forEach(function(t){
      t.src=null==t.dataset.src?t.src:t.dataset.src
    })
  }
  function lazyLoadScripts(){
    j!=lazyScripts.length&&("lazyload2"==lazyScripts[j].getAttribute("type")?(lazyScripts[j].setAttribute("type","lazyloaded"),void 0!==lazyScripts[j].dataset.src?((s=document.createElement("script")).src=lazyScripts[j].dataset.src,document.body.appendChild(s),s.onload=function(){j++,lazyLoadScripts()}):((s=document.createElement("script")).innerHTML=lazyScripts[j].innerHTML,document.body.appendChild(s),j++,lazyLoadScripts())):(j++,lazyLoadScripts()))
  }
  function lazyLoadCss(t){
    (s=document.createElement("link")).rel="stylesheet",s.href=t,document.getElementsByTagName("head")[0].appendChild(s)
  }
  function lazyLoadJS(t){
    if(lazyLoadedJS)return setTimeout(function(){lazyLoadJS(t)},200),!1;lazyLoadedJS=1,(s=document.createElement("script")).src=t,s.onload=function(){lazyLoadedJS=0},document.body.appendChild(s)
  }
  function wnwAnalytics() {
    var script2 = document.querySelectorAll(".analytics");
    script2.forEach(function(analyticsScript) {
      trekkie.integrations=false;
      s = document.createElement("script");
      s.innerHTML = analyticsScript.innerHTML;
      insertAfter(s, analyticsScript);
      analyticsScript.parentNode.removeChild(analyticsScript);
    });
  }
  document.addEventListener("DOMContentLoaded",function(){windowWidth=screen.width,lazyLink=document.querySelectorAll("link[data-href]"),lazyImages=document.querySelectorAll("img.lazy2"),nolazyImages=document.querySelectorAll("img.lazy"),lazyBackground=document.querySelectorAll(".lazybg"),lazyIframe=document.querySelectorAll("iframe"),lazySource=document.querySelectorAll("source"),lazyScripts=document.querySelectorAll("script[type=lazyload2]"),navigator_platform=navigator.platform,i=0,j=0,flag=1,window.addEventListener("scroll",function(){init()}),window.addEventListener("mousemove",function(){init()}),window.addEventListener("touchstart",function(){init()}),"Linux x86_64"!=navigator_platform&&init(),setTimeout(function(){init()},6000)});

  function load_all_js() {

    console.log("Yes-optimization");
    lazyLink=document.querySelectorAll("link[data-href]");
    lazyLoadLink();
    
    lazyLoadJS("//cdn.shopify.com/s/files/1/0560/6827/6386/t/23/assets/vendor.min.js?v=91934266268907694051666105069");
    lazyLoadJS("//cdn.shopify.com/s/files/1/0560/6827/6386/t/23/assets/theme.js?v=86204165267415173161666105069");
    setTimeout(function() {
      const wnw_load = new Event('wnw_load');
      window.dispatchEvent(wnw_load);
    }, 100);
    setTimeout(function() {
      var DOMContentLoaded2_event = document.createEvent("Event");
      DOMContentLoaded2_event.initEvent("DOMContentLoaded2", true, true);
      window.document.dispatchEvent(DOMContentLoaded2_event);
    }, 10000);
    setTimeout(function() {
      wnwAnalytics();                
    },100);
    

    j=0;
    lazyScripts = document.querySelectorAll("script[type=lazyload2]");
    lazyLoadScripts();
    
    lazySource = document.querySelectorAll("source");
    lazyLoadSource();
            
    setInterval(function() {
      lazyImages = document.querySelectorAll('img.lazy2');
      lazyBackground = document.querySelectorAll('.lazybg');
      lazyLoadImg();
      lazyLoadBackground();
    }, 2000);
  }

</script>
```

# Speed2
```
{{ content_for_header | replace : "addEventListener('load'", "addEventListener('wnw_load'" | replace : "previewBarInjector.init();", "" | replace : 'DOMContentLoaded', 'wnw_load' | replace : 'defer="defer" src=', 'type="lazyload2" defer="defer" data-src=' }}

<script type="text/javascript">
  var windowWidth,lazyLink,lazyImages,lazySource,lazyBackground,lazyIframe,lazyScripts,navigator_platform,lazyLoadedJS,src,style,datasrc,urls,analytics,s,x,i,j,flag;
  function init(){flag&&(flag=0,lazyLoadImg(),lazyLoadBackground(),lazyLoadIframe(),lazyLoadSource(),load_all_js())}
  function isElementInViewport(t){
    var a=t.getBoundingClientRect();
    return a.top>=0&&a.left>=0&&a.bottom<=(window.innerHeight||document.documentElement.clientHeight)&&a.right<=(window.innerWidth||document.documentElement.clientWidth)
  }
  function isElementInView(t){
    var a=t.getBoundingClientRect();
    return a.top<(window.innerHeight/2||document.documentElement.clientHeight/2) && a.bottom>(window.innerHeight/2||document.documentElement.clientHeight/2)
  }
  function lazyLoadLink(){
    lazyLink.forEach(function(t){
      t.href=null==t.dataset.href?t.href:t.dataset.href
    })
  }
  function lazyLoadImg(){
    lazyImages.forEach(function(t){
      null!=(src=windowWidth<600?null==t.dataset.mobsrc?t.dataset.src:t.dataset.mobsrc:t.dataset.src)&&(t.src=src),t.classList.remove("lazy2")
    })
  }
  function lazyLoadImg2(){
    lazyImages.forEach(function(t){
      isElementInViewport(t)&&(null!=(src=windowWidth<600?null==t.dataset.mobsrc?t.dataset.src:t.dataset.mobsrc:t.dataset.src)&&(t.src=src),t.classList.remove("lazy"))
    })
  }
  function lazyLoadSource(){
    lazySource.forEach(function(t){
      t.srcset=null==t.dataset.srcset?t.srcset:t.dataset.srcset
    })
  }
  function lazyLoadBackground(){
    lazyBackground.forEach(function(t){
      lazybg=windowWidth<768?null==t.dataset.mobstyle?t.dataset.style:t.dataset.mobstyle:t.dataset.style,null!=lazybg&&(t.style=lazybg),t.classList.remove("lazybg")
    })
  }
  function lazyLoadIframe(){
    lazyIframe.forEach(function(t){
      t.src=null==t.dataset.src?t.src:t.dataset.src
    })
  }
  function lazyLoadScripts(){
    j!=lazyScripts.length&&("lazyload2"==lazyScripts[j].getAttribute("type")?(lazyScripts[j].setAttribute("type","lazyloaded"),void 0!==lazyScripts[j].dataset.src?((s=document.createElement("script")).src=lazyScripts[j].dataset.src,document.body.appendChild(s),s.onload=function(){j++,lazyLoadScripts()}):((s=document.createElement("script")).innerHTML=lazyScripts[j].innerHTML,document.body.appendChild(s),j++,lazyLoadScripts())):(j++,lazyLoadScripts()))
  }
  function lazyLoadCss(t){
    (s=document.createElement("link")).rel="stylesheet",s.href=t,document.getElementsByTagName("head")[0].appendChild(s)
  }
  function lazyLoadJS(t){
    if(lazyLoadedJS)return setTimeout(function(){lazyLoadJS(t)},200),!1;lazyLoadedJS=1,(s=document.createElement("script")).src=t,s.onload=function(){lazyLoadedJS=0},document.body.appendChild(s)
  }
  document.addEventListener("DOMContentLoaded",function(){windowWidth=screen.width,lazyLink=document.querySelectorAll("link"),lazyImages=document.querySelectorAll("img.lazy2"),nolazyImages=document.querySelectorAll("img.lazy"),lazyBackground=document.querySelectorAll(".lazybg"),lazyIframe=document.querySelectorAll("iframe"),lazySource=document.querySelectorAll("source"),lazyScripts=document.getElementsByTagName("script"),navigator_platform=navigator.platform,i=0,j=0,flag=1,window.addEventListener("scroll",function(){init()}),window.addEventListener("mousemove",function(){init()}),window.addEventListener("touchstart",function(){init()}),"Linux x86_64"!=navigator_platform&&init(),setTimeout(function(){init()},60000)});

  function load_all_js() {

    console.log("Yes-optimization");
    setTimeout(function() {
      const wnw_load = new Event('wnw_load');
      window.dispatchEvent(wnw_load);
    }, 100);
    lazyLink=document.querySelectorAll("link");
    lazyLoadLink();

    j=0;
    lazyScripts = document.querySelectorAll("script[type=lazyload2]");
    lazyLoadScripts();
    
    lazySource = document.querySelectorAll("source");
    lazyLoadSource();
	
    var previewbar = 0;
    
    setInterval(function() {
      lazyImages = document.querySelectorAll('img.lazy2');
      lazyBackground = document.querySelectorAll('.lazybg');
      lazyLoadImg();
      lazyLoadBackground();
      
      if(typeof(Shopify.PreviewBarInjector) == 'function' && previewbar == 0 ){
        let domain = new URL(location.href);
        
        var previewBar = new Shopify.PreviewBarInjector({
          targetNode: document.body,
          iframeRoot: 'https://'+domain.hostname,
          iframeSrc: 'https://'+domain.hostname+'/preview_bar',
          previewToken: '',
          themeStoreId: '836',
          permanentDomain: 'shifted-strong.myshopify.com',
        });
        previewBar.init();
        previewbar = 1;
        console.log('preview bar');
      }
    }, 2000);
  }

</script>
```
