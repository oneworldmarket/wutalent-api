Javascript API
===
yu:talent also supports a JS API. This is the API which you can use in all your front-end work.

To use this API you have to include the latest jQuery library in the header.  

Then you need to include at the bottom the following code:

```
<script>
    window.wuAfterInit = function(wu) {
        //here is the user code to work with
    }

    var wuDomain = 'yutalent.co.uk';

    window.wuAsyncInit = function () {
        WU.init({
            domain: wuDomain,
            signed_request: '<?php echo $_REQUEST['signed_request'] ?>',
            height: '100%',
            'afterInit': function(wu){
                if( typeof window.wuAfterInit == 'function' ) {
                    window.wuAfterInit(wu);
                }
            }
        });
    };

    // Load the SDK's source Asynchronously
    (function (d, s, id) {
        var js, wjs = d.getElementsByTagName(s)[0];
        if (d.getElementById(id)) {
            return;
        }
        js = d.createElement(s);
        js.id = id;
        js.src = "//" + wuDomain + "/static/scripts/api/WU.js";
        wjs.parentNode.insertBefore(js, wjs);
    }(document, 'script', 'wutalent-jssdk'));
</script>
```

Full example:

```
<!doctype html>
<head>
    <script src="/static/scripts/lib/jquery-1.7.2.min.js"></script>
</head>

<script>
    window.wuAfterInit = function(wu) {        
            wu.Messenger.sendMessageToWU('user/profile', {}, function(response){
                alert( response.user );
            });            
    }
        
    var wuDomain = 'yutalent.co.uk';

    window.wuAsyncInit = function () {
        WU.init({
            domain: wuDomain,
            signed_request: '<?php echo $_REQUEST['signed_request'] ?>',
            height: '100%',
            'afterInit': function(wu){
                if( typeof window.wuAfterInit == 'function' ) {
                    window.wuAfterInit(wu);
                }
            }
        });
    };

    // Load the SDK's source Asynchronously
    (function (d, s, id) {
        var js, wjs = d.getElementsByTagName(s)[0];
        if (d.getElementById(id)) {
            return;
        }
        js = d.createElement(s);
        js.id = id;
        js.src = "//" + wuDomain + "/static/scripts/api/WU.js";
        wjs.parentNode.insertBefore(js, wjs);
    }(document, 'script', 'wutalent-jssdk'));
</script>
```
