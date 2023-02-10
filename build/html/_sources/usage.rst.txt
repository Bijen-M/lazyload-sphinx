Usage
=====

.. _code:

Code
------------

For this lazy loading technique, we can use the following code snippet on the view page:

.. code-block:: javascript

    const loadedUrl=[];
       function loadScript(urls){
          
           for(const url of urls){
               if(loadedUrl.includes(url)){
                   return;
               }
               let isLoaded=false;
               var scripts = document.getElementsByTagName("script");
               console.log(" Script length: "+scripts.length);
               
              
               let script = document.createElement('script');
               script.type = "text/javascript";
               script.src = url;
               script.className = 'dynamic-script';
               document.body.appendChild(script);
               loadedUrl.push(url);
           }
       }
       function isInViewport(el) {
           const rect = el.getBoundingClientRect();
           return (
               rect.top >= 0 &&
               rect.left >= 0 &&
               rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
               rect.right <= (window.innerWidth || document.documentElement.clientWidth)
   
           );
       }
   
       const box = document.querySelector('.emi_input_block');
   
   
   document.addEventListener('scroll', function () {
          if(isInViewport(box)){
           const urls = [
               'newfrontend/homepage/js/emicalculator.js',
               'newfrontend/homepage/js/chart.js'
           ]
           loadScript(urls);
          }
       }, {
           passive: true
       });


This code essentially loads the script when the user scrolls to it and is visibile in the viewport.