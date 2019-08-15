---
description: >-
  Perform Image analysis of pictures attached to Tweets using the Watson Visual
  Recognition service
---

# Visual Recognition Dashboard Example

## About this Flow : 

This flow uses Watson Visual Recognition to analyze images from tweets. It also mesures the sentiment score of the tweets on a guage. 

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LhCRb6QNiVWF6s9FafQ%2F-Ljwuky9N2gyYS5dh-fm%2F-LjwvGFAJpPTLURtnETu%2FNode-RED-Twitter-TweetImageAnalyzer-Dashboard.png?alt=media&token=47ded435-2ac9-4eba-b08a-749942413042)

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LhCRb6QNiVWF6s9FafQ%2F-Ljwuky9N2gyYS5dh-fm%2F-LjwvBqCdnuW9GgxrEK0%2FScreen%20Shot%202019-07-16%20at%206.34.54%20PM.png?alt=media&token=c5e1e948-b239-4edb-92b6-01fa02801545)

#### Go to Catalog on IBM Cloud and create an instance of Visual Recognition Service. Use your API keys to authenticate to this flow  <a id="go-to-catalog-on-ibm-cloud-and-create-an-instance-of-visual-recognition-service-use-your-api-keys-to-authenticate-to-this-flow"></a>

## Flow can be imported : 

```text
[
   {
      "id":"e166925b.1b30f",
      "type":"tab",
      "label":"Twitter Image Analysis",
      "disabled":false,
      "info":""
   },
   {
      "id":"53328cd0.ccb6b4",
      "type":"ui_template",
      "z":"e166925b.1b30f",
      "group":"5a33565a.fc9bb",
      "name":"Photo",
      "order":3,
      "width":"9",
      "height":"7",
      "format":"{msg.payload}",
      "storeOutMessages":false,
      "fwdInMessages":true,
      "templateScope":"local",
      "x":570,
      "y":280,
      "wires":[
         [
            "4892db3e.cb4a74"
         ]
      ]
   },
   {
      "id":"3284724c.0349ee",
      "type":"comment",
      "z":"e166925b.1b30f",
      "name":"Reload picture into Node-RED Dashboard",
      "info":"<script>\n    window.location.reload(false); \n</script>",
      "x":1120,
      "y":280,
      "wires":[

      ]
   },
   {
      "id":"59539967.0c365",
      "type":"function",
      "z":"e166925b.1b30f",
      "name":"Extract Twitter Image URL",
      "func":"msg.payload = \"\";\nif (typeof msg.tweet.entities.media !== 'undefined') {\n  if (typeof msg.tweet.entities.media[0].media_url !== 'undefined') {\n    msg.payload = msg.tweet.entities.media[0].media_url;\n  }  \n}\n\nif (typeof msg.tweet.extended_tweet !== 'undefined') {\n    if (typeof msg.tweet.extended_tweet.entities !== 'undefined') {\n        if (typeof msg.tweet.extended_tweet.entities.media !== 'undefined') {\n            if (typeof msg.tweet.extended_tweet.entities.media[0].media_url !== 'undefined') {\n                msg.payload = msg.tweet.extended_tweet.entities.media[0].media_url_https;\n            }\n        }\n    }\n}\n\nif(typeof msg.tweet.retweeted_status !== 'undefined') {\n    if( typeof msg.tweet.retweeted_status.extended_tweet !== 'undefined') {\n        if( typeof msg.tweet.retweeted_status.extended_tweet.entities !== 'undefined') {\n            if( typeof msg.tweet.retweeted_status.extended_tweet.entities.media !== 'undefined') {\n                if( typeof msg.tweet.retweeted_status.extended_tweet.entities.media[0].media_url !== 'undefined') {\n                    msg.payload = msg.tweet.retweeted_status.extended_tweet.entities.media[0].media_url;\n                }\n            }\n        }\n    }\n}\n\n\nif( msg.payload.length ) {\n    msg.template = \"<img width=\\\"300\\\" height=\\\"300\\\" alt=\\\"Twitter Image\\\" src=\\\"\"+msg.payload+\"\\\">\";\n    return [ msg, null ];\n} else {\n    return [ null, msg ];\n}",
      "outputs":"2",
      "noerr":0,
      "x":270,
      "y":260,
      "wires":[
         [
            "8f249f5c.f901b8",
            "f85e365.acc8bc8",
            "15e1ed2a.233233",
            "46b5fdab.1e0234",
            "17a2322c.73c4f6",
            "53328cd0.ccb6b4"
         ],
         [

         ]
      ]
   },
   {
      "id":"8f249f5c.f901b8",
      "type":"debug",
      "z":"e166925b.1b30f",
      "name":"Image URL to analyze",
      "active":true,
      "tosidebar":true,
      "console":false,
      "tostatus":false,
      "complete":"payload",
      "targetType":"msg",
      "x":620,
      "y":240,
      "wires":[

      ]
   },
   {
      "id":"a19bdfc5.9a805",
      "type":"debug",
      "z":"e166925b.1b30f",
      "name":"",
      "active":true,
      "console":"false",
      "complete":"result",
      "x":820,
      "y":400,
      "wires":[

      ]
   },
   {
      "id":"3f2081d5.a17676",
      "type":"debug",
      "z":"e166925b.1b30f",
      "name":"",
      "active":true,
      "console":"false",
      "complete":"tweet",
      "x":590,
      "y":80,
      "wires":[

      ]
   },
   {
      "id":"bcca25bc.f6609",
      "type":"inject",
      "z":"e166925b.1b30f",
      "name":"Rhino",
      "topic":"",
      "payload":"{\"created_at\":\"Sat Sep 23 14:19:37 +0000 2017\",\"id\":911595915168899100,\"id_str\":\"911595915168899072\",\"text\":\"RT @IBM: Watch how a new solution is harnessing the power of #IBMIot to combat the poaching of endangered 🦏:… \",\"source\":\"<a href=\\\"http://twitter.com\\\" rel=\\\"nofollow\\\">Twitter Web Client</a>\",\"truncated\":false,\"in_reply_to_status_id\":null,\"in_reply_to_status_id_str\":null,\"in_reply_to_user_id\":null,\"in_reply_to_user_id_str\":null,\"in_reply_to_screen_name\":null,\"user\":{\"id\":2577403879,\"id_str\":\"2577403879\",\"name\":\"John Walicki\",\"screen_name\":\"johnwalicki\",\"location\":\"New Jersey, USA\",\"url\":null,\"description\":\"IBM Watson Internet of Things Developer Advocate, Über Geek, Family Guy. #IoT #OpenSource, #Linux, #AI My tweets are my own.\",\"translator_type\":\"none\",\"protected\":false,\"verified\":false,\"followers_count\":646,\"friends_count\":850,\"listed_count\":153,\"favourites_count\":1770,\"statuses_count\":1473,\"created_at\":\"Thu Jun 19 19:54:32 +0000 2014\",\"utc_offset\":null,\"time_zone\":null,\"geo_enabled\":false,\"lang\":\"en\",\"contributors_enabled\":false,\"is_translator\":false,\"profile_background_color\":\"C0DEED\",\"profile_background_image_url\":\"http://abs.twimg.com/images/themes/theme1/bg.png\",\"profile_background_image_url_https\":\"https://abs.twimg.com/images/themes/theme1/bg.png\",\"profile_background_tile\":false,\"profile_link_color\":\"1DA1F2\",\"profile_sidebar_border_color\":\"C0DEED\",\"profile_sidebar_fill_color\":\"DDEEF6\",\"profile_text_color\":\"333333\",\"profile_use_background_image\":true,\"profile_image_url\":\"http://pbs.twimg.com/profile_images/711615965721718784/7My0kbZI_normal.jpg\",\"profile_image_url_https\":\"https://pbs.twimg.com/profile_images/711615965721718784/7My0kbZI_normal.jpg\",\"profile_banner_url\":\"https://pbs.twimg.com/profile_banners/2577403879/1476478381\",\"default_profile\":true,\"default_profile_image\":false,\"following\":null,\"follow_request_sent\":null,\"notifications\":null},\"geo\":null,\"coordinates\":null,\"place\":null,\"contributors\":null,\"retweeted_status\":{\"created_at\":\"Fri Sep 22 13:15:04 +0000 2017\",\"id\":911217282067714000,\"id_str\":\"911217282067714048\",\"text\":\"Watch how a new solution is harnessing the power of #IBMIot to combat the poaching of endangered 🦏:… https://t.co/91BD2uZqFk\",\"display_text_range\":[0,140],\"source\":\"<a href=\\\"https://www.sprinklr.com\\\" rel=\\\"nofollow\\\">Sprinklr</a>\",\"truncated\":true,\"in_reply_to_status_id\":null,\"in_reply_to_status_id_str\":null,\"in_reply_to_user_id\":null,\"in_reply_to_user_id_str\":null,\"in_reply_to_screen_name\":null,\"user\":{\"id\":18994444,\"id_str\":\"18994444\",\"name\":\"IBM\",\"screen_name\":\"IBM\",\"location\":\"Armonk, New York\",\"url\":\"http://www.ibm.com\",\"description\":\"Official IBM Twitter account. Follows the IBM Social Computing Guidelines.\",\"translator_type\":\"none\",\"protected\":false,\"verified\":true,\"followers_count\":396044,\"friends_count\":6427,\"listed_count\":5154,\"favourites_count\":2637,\"statuses_count\":9814,\"created_at\":\"Wed Jan 14 20:41:57 +0000 2009\",\"utc_offset\":-14400,\"time_zone\":\"Eastern Time (US & Canada)\",\"geo_enabled\":false,\"lang\":\"en\",\"contributors_enabled\":false,\"is_translator\":false,\"profile_background_color\":\"FFFFFF\",\"profile_background_image_url\":\"http://pbs.twimg.com/profile_background_images/378800000152426467/Viwc1IvP.jpeg\",\"profile_background_image_url_https\":\"https://pbs.twimg.com/profile_background_images/378800000152426467/Viwc1IvP.jpeg\",\"profile_background_tile\":false,\"profile_link_color\":\"2FC2EF\",\"profile_sidebar_border_color\":\"000000\",\"profile_sidebar_fill_color\":\"252429\",\"profile_text_color\":\"666666\",\"profile_use_background_image\":false,\"profile_image_url\":\"http://pbs.twimg.com/profile_images/875111316821651456/AmZkYTWP_normal.jpg\",\"profile_image_url_https\":\"https://pbs.twimg.com/profile_images/875111316821651456/AmZkYTWP_normal.jpg\",\"profile_banner_url\":\"https://pbs.twimg.com/profile_banners/18994444/1495457811\",\"default_profile\":false,\"default_profile_image\":false,\"following\":null,\"follow_request_sent\":null,\"notifications\":null},\"geo\":null,\"coordinates\":null,\"place\":null,\"contributors\":null,\"is_quote_status\":false,\"extended_tweet\":{\"full_text\":\"Watch how a new solution is harnessing the power of #IBMIot to combat the poaching of endangered 🦏: https://t.co/zL55BXKLFq #WorldRhinoDay https://t.co/eBpZmbbnB7\",\"display_text_range\":[0,138],\"entities\":{\"hashtags\":[{\"text\":\"IBMIot\",\"indices\":[52,59]},{\"text\":\"WorldRhinoDay\",\"indices\":[124,138]}],\"urls\":[{\"url\":\"https://t.co/zL55BXKLFq\",\"expanded_url\":\"http://bitly.com/2hknTRt\",\"display_url\":\"bitly.com/2hknTRt\",\"indices\":[100,123]}],\"user_mentions\":[],\"symbols\":[],\"media\":[{\"id\":911217279353880600,\"id_str\":\"911217279353880576\",\"indices\":[139,162],\"media_url\":\"http://pbs.twimg.com/media/DKVLSakWAAAc3Fl.jpg\",\"media_url_https\":\"https://pbs.twimg.com/media/DKVLSakWAAAc3Fl.jpg\",\"url\":\"https://t.co/eBpZmbbnB7\",\"display_url\":\"pic.twitter.com/eBpZmbbnB7\",\"expanded_url\":\"https://twitter.com/IBM/status/911217282067714048/photo/1\",\"type\":\"photo\",\"sizes\":{\"small\":{\"w\":680,\"h\":453,\"resize\":\"fit\"},\"medium\":{\"w\":1024,\"h\":682,\"resize\":\"fit\"},\"thumb\":{\"w\":150,\"h\":150,\"resize\":\"crop\"},\"large\":{\"w\":1024,\"h\":682,\"resize\":\"fit\"}}}]},\"extended_entities\":{\"media\":[{\"id\":911217279353880600,\"id_str\":\"911217279353880576\",\"indices\":[139,162],\"media_url\":\"http://pbs.twimg.com/media/DKVLSakWAAAc3Fl.jpg\",\"media_url_https\":\"https://pbs.twimg.com/media/DKVLSakWAAAc3Fl.jpg\",\"url\":\"https://t.co/eBpZmbbnB7\",\"display_url\":\"pic.twitter.com/eBpZmbbnB7\",\"expanded_url\":\"https://twitter.com/IBM/status/911217282067714048/photo/1\",\"type\":\"photo\",\"sizes\":{\"small\":{\"w\":680,\"h\":453,\"resize\":\"fit\"},\"medium\":{\"w\":1024,\"h\":682,\"resize\":\"fit\"},\"thumb\":{\"w\":150,\"h\":150,\"resize\":\"crop\"},\"large\":{\"w\":1024,\"h\":682,\"resize\":\"fit\"}}}]}},\"quote_count\":2,\"reply_count\":0,\"retweet_count\":35,\"favorite_count\":46,\"entities\":{\"hashtags\":[{\"text\":\"IBMIot\",\"indices\":[52,59]}],\"urls\":[{\"url\":\"https://t.co/91BD2uZqFk\",\"expanded_url\":\"https://twitter.com/i/web/status/911217282067714048\",\"display_url\":\"twitter.com/i/web/status/9…\",\"indices\":[101,124]}],\"user_mentions\":[],\"symbols\":[]},\"favorited\":false,\"retweeted\":false,\"possibly_sensitive\":false,\"filter_level\":\"low\",\"lang\":\"en\"},\"is_quote_status\":false,\"quote_count\":0,\"reply_count\":0,\"retweet_count\":0,\"favorite_count\":0,\"entities\":{\"hashtags\":[{\"text\":\"IBMIot\",\"indices\":[61,68]}],\"urls\":[],\"user_mentions\":[{\"screen_name\":\"IBM\",\"name\":\"IBM\",\"id\":18994444,\"id_str\":\"18994444\",\"indices\":[3,7]}],\"symbols\":[]},\"favorited\":false,\"retweeted\":false,\"possibly_sensitive\":false,\"filter_level\":\"low\",\"lang\":\"en\",\"timestamp_ms\":\"1506176377466\"}",
      "payloadType":"json",
      "repeat":"",
      "crontab":"",
      "once":false,
      "x":150,
      "y":460,
      "wires":[
         [
            "a625aa99.53ef38"
         ]
      ]
   },
   {
      "id":"a625aa99.53ef38",
      "type":"change",
      "z":"e166925b.1b30f",
      "name":"",
      "rules":[
         {
            "t":"set",
            "p":"tweet",
            "pt":"msg",
            "to":"payload",
            "tot":"msg"
         }
      ],
      "action":"",
      "property":"",
      "from":"",
      "to":"",
      "reg":false,
      "x":320,
      "y":480,
      "wires":[
         [
            "64d22ec0.fe92d",
            "59539967.0c365"
         ]
      ]
   },
   {
      "id":"d43baa51.b9edb",
      "type":"comment",
      "z":"e166925b.1b30f",
      "name":"Sample Tweets with images",
      "info":"",
      "x":150,
      "y":380,
      "wires":[

      ]
   },
   {
      "id":"c86730cb.a23ff8",
      "type":"function",
      "z":"e166925b.1b30f",
      "name":"Process Results",
      "func":"if (typeof msg.result == 'undefined') {\n    return null;\n}\n\nif (typeof msg.result.error != 'undefined') {\n    //The Lite Plan allows users to make 7,500 API calls for free\n    // Daily limit is  (up to 250 calls per day) \n    // {\"status\":\"ERROR\",\"statusInfo\":\"Key is over transaction limit\"}\n    msg.template = msg.result.error.message;\n    return msg;\n}\n\n// Text Extraction\nif (typeof msg.result.images[0].text != 'undefined') {\n    var image_text = msg.result.images[0].text;\n    msg.payload = image_text;\n    msg.template = image_text;\n    if( image_text.length >0 ) {\n       msg.template= \"Watson found the words: \"+image_text;\n    }\n    return msg;\n}\n\nvar bestcolor = -1;\nvar colorscore = 0;\nvar c_id = 0;\nvar say = \"\";\nvar item;\n\nfor ( c_id=0; c_id < (msg.result.images[0].classifiers.length); c_id++ ){\n    // find the best color, if any\n    for( i =0; i<(msg.result.images[0].classifiers[c_id].classes.length); i++ ){\n      var object = msg.result.images[0].classifiers[c_id].classes[i].class;\n      if ( object.includes(\"color\") ) {\n        if( msg.result.images[0].classifiers[c_id].classes[i].score > colorscore){\n            bestcolor = i;\n            colorscore = msg.result.images[0].classifiers[c_id].classes[i].score;\n        }\n      }\n    }\n \n    var bestItem = 0;\n    var itemScore = 0;\n    for( i =0; i<(msg.result.images[0].classifiers[c_id].classes.length); i++ ){\n      var object = msg.result.images[0].classifiers[c_id].classes[i].class;\n      if ( !object.includes(\"color\") ) {\n        if( msg.result.images[0].classifiers[c_id].classes[i].score > itemScore){\n//            bestItem = i;\n            bestItem = 0;\n            itemScore =  msg.result.images[0].classifiers[c_id].classes[i].score;\n        }\n      }\n    }\n \n     if( bestcolor != \"-1\") {\n        // found a color\n        item = msg.result.images[0].classifiers[c_id].classes[bestcolor].class + \" \" + msg.result.images[0].classifiers[c_id].classes[bestItem].class;\n        bestcolor = -1;\n    } else {\n       item = msg.result.images[0].classifiers[c_id].classes[bestItem].class;\n    }\n//    say = say + \" Watson's \" + msg.result.images[0].classifiers[c_id].name + \" classifier thinks this picture contains a \" + item +\".\";\n    say = say + \" Watson thinks this picture contains a \" + item +\".\";\n}\nmsg.payload =  say;\n\nvar picInfo = msg.result.images[0].classifiers[0].classes;\nvar arrayLength = picInfo.length;\n\nmsg.template=\"<style>\";\nmsg.template=msg.template+\"table { width: 440px; margin-top: 10px; }\";\nmsg.template=msg.template+\"tr:nth-child(even){background-color: #f2f2f2;}\";\nmsg.template=msg.template+\"th, td { padding: 8px; text-align: left; border-bottom: 1px solid #ddd; width: 10%;}\";\nmsg.template=msg.template+\"</style>\";\n\nmsg.template=msg.template+\"<h2>\"+say+\"</h2><table span=100%><tr><th>Class</th><th>Confidence</th></tr>\";\nfor (var i = 0; i < arrayLength; i++) {\n  msg.template = msg.template + \"<tr><td>\" + picInfo[i].class + \"</td><td>\" + picInfo[i].score + \"</td></tr>\";\n}\nmsg.template = msg.template + \"</table>\";\n\nreturn msg;",
      "outputs":1,
      "noerr":0,
      "x":840,
      "y":360,
      "wires":[
         [
            "3cb0f472.80407c",
            "f669f8fa.c9242"
         ]
      ]
   },
   {
      "id":"3cb0f472.80407c",
      "type":"debug",
      "z":"e166925b.1b30f",
      "name":"What did Watson find?",
      "active":true,
      "console":"false",
      "complete":"payload",
      "x":1060,
      "y":380,
      "wires":[

      ]
   },
   {
      "id":"f85e365.acc8bc8",
      "type":"change",
      "z":"e166925b.1b30f",
      "name":"Tweet Text",
      "rules":[
         {
            "t":"set",
            "p":"payload",
            "pt":"msg",
            "to":"tweet.text",
            "tot":"msg"
         }
      ],
      "action":"",
      "property":"",
      "from":"",
      "to":"",
      "reg":false,
      "x":590,
      "y":200,
      "wires":[
         [
            "98cfc8d8.18aaa",
            "d49dedd8.ce8b28"
         ]
      ]
   },
   {
      "id":"98cfc8d8.18aaa",
      "type":"ui_text",
      "z":"e166925b.1b30f",
      "group":"5a33565a.fc9bb",
      "order":2,
      "width":"9",
      "height":"2",
      "name":"Tweet Text",
      "label":"",
      "format":"{{msg.payload}}",
      "layout":"row-left",
      "x":830,
      "y":200,
      "wires":[

      ]
   },
   {
      "id":"f669f8fa.c9242",
      "type":"ui_template",
      "z":"e166925b.1b30f",
      "group":"5402acbe.dcd3ec",
      "name":"Results Table",
      "order":1,
      "width":"9",
      "height":"10",
      "format":"",
      "storeOutMessages":true,
      "fwdInMessages":true,
      "templateScope":"local",
      "x":1040,
      "y":340,
      "wires":[
         [

         ]
      ]
   },
   {
      "id":"455e4f92.180cf",
      "type":"inject",
      "z":"e166925b.1b30f",
      "name":"Curtain",
      "topic":"",
      "payload":"{\"created_at\":\"Sat Sep 23 17:48:40 +0000 2017\",\"id\":911648524663709700,\"id_str\":\"911648524663709698\",\"text\":\"Breaking 2 @NikeRunning @NatGeo https://t.co/aAygp48EAq\",\"display_text_range\":[0,31],\"source\":\"<a href=\\\"http://twitter.com/download/iphone\\\" rel=\\\"nofollow\\\">Twitter for iPhone</a>\",\"truncated\":false,\"in_reply_to_status_id\":null,\"in_reply_to_status_id_str\":null,\"in_reply_to_user_id\":null,\"in_reply_to_user_id_str\":null,\"in_reply_to_screen_name\":null,\"user\":{\"id\":109308126,\"id_str\":\"109308126\",\"name\":\"Jrmi\",\"screen_name\":\"JeremieRoturier\",\"location\":\"London, England\",\"url\":\"http://jeremieroturier.com\",\"description\":\"Sportsaholic and writing junkie. Member of @JolieFoulee, founder of @EtoileFO. Take pics for quality football magazines. Work at @Apple x @beatsbydre. Ex @Nike.\",\"translator_type\":\"none\",\"protected\":false,\"verified\":false,\"followers_count\":472,\"friends_count\":665,\"listed_count\":24,\"favourites_count\":631,\"statuses_count\":4333,\"created_at\":\"Thu Jan 28 16:42:30 +0000 2010\",\"utc_offset\":7200,\"time_zone\":\"Paris\",\"geo_enabled\":true,\"lang\":\"en\",\"contributors_enabled\":false,\"is_translator\":false,\"profile_background_color\":\"8C12FF\",\"profile_background_image_url\":\"http://pbs.twimg.com/profile_background_images/106316656/chat_noir.jpg\",\"profile_background_image_url_https\":\"https://pbs.twimg.com/profile_background_images/106316656/chat_noir.jpg\",\"profile_background_tile\":true,\"profile_link_color\":\"85459E\",\"profile_sidebar_border_color\":\"8956B3\",\"profile_sidebar_fill_color\":\"030303\",\"profile_text_color\":\"17BEE8\",\"profile_use_background_image\":true,\"profile_image_url\":\"http://pbs.twimg.com/profile_images/730899031162036224/_8p6sEXu_normal.jpg\",\"profile_image_url_https\":\"https://pbs.twimg.com/profile_images/730899031162036224/_8p6sEXu_normal.jpg\",\"profile_banner_url\":\"https://pbs.twimg.com/profile_banners/109308126/1472307658\",\"default_profile\":false,\"default_profile_image\":false,\"following\":null,\"follow_request_sent\":null,\"notifications\":null},\"geo\":null,\"coordinates\":null,\"place\":{\"id\":\"3078869807f9dd36\",\"url\":\"https://api.twitter.com/1.1/geo/id/3078869807f9dd36.json\",\"place_type\":\"city\",\"name\":\"Berlin\",\"full_name\":\"Berlin, Germany\",\"country_code\":\"DE\",\"country\":\"Germany\",\"bounding_box\":{\"type\":\"Polygon\",\"coordinates\":[[[13.088304,52.338079],[13.088304,52.675323],[13.760909,52.675323],[13.760909,52.338079]]]},\"attributes\":{}},\"contributors\":null,\"is_quote_status\":false,\"quote_count\":0,\"reply_count\":0,\"retweet_count\":0,\"favorite_count\":0,\"entities\":{\"hashtags\":[],\"urls\":[],\"user_mentions\":[{\"screen_name\":\"NikeRunning\",\"name\":\"Nike+ Run Club\",\"id\":337726224,\"id_str\":\"337726224\",\"indices\":[11,23]},{\"screen_name\":\"NatGeo\",\"name\":\"National Geographic\",\"id\":17471979,\"id_str\":\"17471979\",\"indices\":[24,31]}],\"symbols\":[],\"media\":[{\"id\":911648512970051600,\"id_str\":\"911648512970051585\",\"indices\":[32,55],\"media_url\":\"http://pbs.twimg.com/media/DKbTfg-X0AEAI9P.jpg\",\"media_url_https\":\"https://pbs.twimg.com/media/DKbTfg-X0AEAI9P.jpg\",\"url\":\"https://t.co/aAygp48EAq\",\"display_url\":\"pic.twitter.com/aAygp48EAq\",\"expanded_url\":\"https://twitter.com/JeremieRoturier/status/911648524663709698/photo/1\",\"type\":\"photo\",\"sizes\":{\"thumb\":{\"w\":150,\"h\":150,\"resize\":\"crop\"},\"large\":{\"w\":1776,\"h\":1184,\"resize\":\"fit\"},\"medium\":{\"w\":1200,\"h\":800,\"resize\":\"fit\"},\"small\":{\"w\":680,\"h\":453,\"resize\":\"fit\"}}}]},\"extended_entities\":{\"media\":[{\"id\":911648512970051600,\"id_str\":\"911648512970051585\",\"indices\":[32,55],\"media_url\":\"http://pbs.twimg.com/media/DKbTfg-X0AEAI9P.jpg\",\"media_url_https\":\"https://pbs.twimg.com/media/DKbTfg-X0AEAI9P.jpg\",\"url\":\"https://t.co/aAygp48EAq\",\"display_url\":\"pic.twitter.com/aAygp48EAq\",\"expanded_url\":\"https://twitter.com/JeremieRoturier/status/911648524663709698/photo/1\",\"type\":\"photo\",\"sizes\":{\"thumb\":{\"w\":150,\"h\":150,\"resize\":\"crop\"},\"large\":{\"w\":1776,\"h\":1184,\"resize\":\"fit\"},\"medium\":{\"w\":1200,\"h\":800,\"resize\":\"fit\"},\"small\":{\"w\":680,\"h\":453,\"resize\":\"fit\"}}}]},\"favorited\":false,\"retweeted\":false,\"possibly_sensitive\":false,\"filter_level\":\"low\",\"lang\":\"en\",\"timestamp_ms\":\"1506188920547\"}",
      "payloadType":"json",
      "repeat":"",
      "crontab":"",
      "once":false,
      "x":150,
      "y":420,
      "wires":[
         [
            "a625aa99.53ef38"
         ]
      ]
   },
   {
      "id":"e34125f2.39cc3",
      "type":"comment",
      "z":"e166925b.1b30f",
      "name":"Paste API keys for Visual Recognition",
      "info":"1. Log into IBM Cloud\n2. Create an instance of the \nWatson Visual Recognition service.\n3. Visit the Service Credentials tab\n4. Click on View Credentials\n5. Copy/Paste the password and username into\nthis Node-RED node.",
      "x":580,
      "y":400,
      "wires":[

      ]
   },
   {
      "id":"64d22ec0.fe92d",
      "type":"debug",
      "z":"e166925b.1b30f",
      "name":"",
      "active":true,
      "console":"false",
      "complete":"false",
      "x":530,
      "y":480,
      "wires":[

      ]
   },
   {
      "id":"58a339ad.2a5d3",
      "type":"delay",
      "z":"e166925b.1b30f",
      "name":"",
      "pauseType":"rate",
      "timeout":"5",
      "timeoutUnits":"seconds",
      "rate":"1",
      "nbRateUnits":"10",
      "rateUnits":"second",
      "randomFirst":"1",
      "randomLast":"5",
      "randomUnits":"seconds",
      "drop":false,
      "x":280,
      "y":80,
      "wires":[
         [
            "59539967.0c365",
            "3f2081d5.a17676"
         ]
      ]
   },
   {
      "id":"d49dedd8.ce8b28",
      "type":"sentiment",
      "z":"e166925b.1b30f",
      "name":"",
      "property":"payload",
      "x":820,
      "y":160,
      "wires":[
         [
            "b2d62de.0fa61d"
         ]
      ]
   },
   {
      "id":"43f4eb9a.9e8f7c",
      "type":"ui_gauge",
      "z":"e166925b.1b30f",
      "name":"",
      "group":"caba2314.a97f3",
      "order":2,
      "width":0,
      "height":0,
      "gtype":"gage",
      "title":"Sentiment Score",
      "label":"",
      "format":"{{value}}",
      "min":"-10",
      "max":10,
      "colors":[
         "#ff0000",
         "#e6e600",
         "#008040"
      ],
      "seg1":"",
      "seg2":"",
      "x":1230,
      "y":160,
      "wires":[

      ]
   },
   {
      "id":"b2d62de.0fa61d",
      "type":"change",
      "z":"e166925b.1b30f",
      "name":"Sentiment Score",
      "rules":[
         {
            "t":"set",
            "p":"payload",
            "pt":"msg",
            "to":"sentiment.score",
            "tot":"msg"
         }
      ],
      "action":"",
      "property":"",
      "from":"",
      "to":"",
      "reg":false,
      "x":1010,
      "y":160,
      "wires":[
         [
            "43f4eb9a.9e8f7c"
         ]
      ]
   },
   {
      "id":"15e1ed2a.233233",
      "type":"change",
      "z":"e166925b.1b30f",
      "name":"Twitter Handle",
      "rules":[
         {
            "t":"set",
            "p":"payload",
            "pt":"msg",
            "to":"tweet.user.screen_name",
            "tot":"msg"
         }
      ],
      "action":"",
      "property":"",
      "from":"",
      "to":"",
      "reg":false,
      "x":600,
      "y":320,
      "wires":[
         [
            "b7bd8f8b.0391d"
         ]
      ]
   },
   {
      "id":"b7bd8f8b.0391d",
      "type":"ui_text",
      "z":"e166925b.1b30f",
      "group":"5a33565a.fc9bb",
      "order":1,
      "width":0,
      "height":0,
      "name":"",
      "label":"User: ",
      "format":"{{msg.payload}}",
      "layout":"row-left",
      "x":810,
      "y":320,
      "wires":[

      ]
   },
   {
      "id":"46b5fdab.1e0234",
      "type":"function",
      "z":"e166925b.1b30f",
      "name":"Tweet URL",
      "func":"msg.template = \"<a href=\\\"https://twitter.com/\"+msg.tweet.user.screen_name+\"/status/\"+msg.tweet.id_str+\"\\\">Open Tweet</a>\";\nif( typeof msg.payload.retweeted_status != 'undefined') {\n       msg.template = \"<a href=\\\"https://twitter.com/\"+msg.tweet.retweeted_status.user.screen_name+\"/status/\"+msg.tweet.retweeted_status.id_str+\"\\\">Open Tweet</a>\";\n}\n\n//msg.payload  = \"https://twitter.com/\"+msg.tweet.user.screen_name+\"/status/\"+msg.tweet.id_str;\n//if( typeof msg.payload.retweeted_status != 'undefined') {\n//    msg.payload  = \"https://twitter.com/\"+msg.tweet.retweeted_status.user.screen_name+\"/status/\"+msg.tweet.retweeted_status.id_str;\n//}\n\nreturn msg;",
      "outputs":1,
      "noerr":0,
      "x":590,
      "y":120,
      "wires":[
         [
            "751978db.6994f8",
            "f0877b6f.0403b"
         ]
      ]
   },
   {
      "id":"f0877b6f.0403b",
      "type":"ui_template",
      "z":"e166925b.1b30f",
      "group":"caba2314.a97f3",
      "name":"Open Tweet",
      "order":1,
      "width":0,
      "height":0,
      "format":"<a href={{msg.payload}}>Open Tweet</a>",
      "storeOutMessages":false,
      "fwdInMessages":false,
      "templateScope":"local",
      "x":830,
      "y":120,
      "wires":[
         [

         ]
      ]
   },
   {
      "id":"751978db.6994f8",
      "type":"debug",
      "z":"e166925b.1b30f",
      "name":"Open Tweet",
      "active":true,
      "tosidebar":true,
      "console":false,
      "tostatus":false,
      "complete":"template",
      "x":830,
      "y":80,
      "wires":[

      ]
   },
   {
      "id":"bfd5f2c8.c67fa",
      "type":"twitter in",
      "z":"e166925b.1b30f",
      "twitter":"",
      "tags":"IBM",
      "user":"false",
      "name":"",
      "inputs":1,
      "x":90,
      "y":80,
      "wires":[
         [
            "58a339ad.2a5d3"
         ]
      ]
   },
   {
      "id":"91669f98.1928d",
      "type":"inject",
      "z":"e166925b.1b30f",
      "name":"Best Ever",
      "topic":"",
      "payload":"{\"created_at\":\"Sat Apr 21 02:31:32 +0000 2018\",\"id\":987519171704520700,\"id_str\":\"987519171704520706\",\"text\":\"I love Sprite! Best soda ever made, I'll only buy that! #IoTCivicHack https://t.co/5pRSCGJGE2\",\"display_text_range\":[0,69],\"source\":\"<a href=\\\"http://twitter.com/download/iphone\\\" rel=\\\"nofollow\\\">Twitter for iPhone</a>\",\"truncated\":false,\"in_reply_to_status_id\":null,\"in_reply_to_status_id_str\":null,\"in_reply_to_user_id\":null,\"in_reply_to_user_id_str\":null,\"in_reply_to_screen_name\":null,\"user\":{\"id\":302215121,\"id_str\":\"302215121\",\"name\":\"Derek\",\"screen_name\":\"_viperboy_\",\"location\":\"Texas, USA\",\"url\":null,\"description\":\"Software Engineer/Developer Advocate @ IBM - Talk to me about IoT! Or food. Or cars. Views expressed here are my own and do not necessarily reflect my employer.\",\"translator_type\":\"none\",\"protected\":false,\"verified\":false,\"followers_count\":1060,\"friends_count\":256,\"listed_count\":46,\"favourites_count\":202,\"statuses_count\":4329,\"created_at\":\"Fri May 20 20:11:40 +0000 2011\",\"utc_offset\":null,\"time_zone\":null,\"geo_enabled\":false,\"lang\":\"en\",\"contributors_enabled\":false,\"is_translator\":false,\"profile_background_color\":\"000000\",\"profile_background_image_url\":\"http://abs.twimg.com/images/themes/theme14/bg.gif\",\"profile_background_image_url_https\":\"https://abs.twimg.com/images/themes/theme14/bg.gif\",\"profile_background_tile\":false,\"profile_link_color\":\"1B95E0\",\"profile_sidebar_border_color\":\"000000\",\"profile_sidebar_fill_color\":\"000000\",\"profile_text_color\":\"000000\",\"profile_use_background_image\":false,\"profile_image_url\":\"http://pbs.twimg.com/profile_images/983179574606467072/wIlJlD2P_normal.jpg\",\"profile_image_url_https\":\"https://pbs.twimg.com/profile_images/983179574606467072/wIlJlD2P_normal.jpg\",\"default_profile\":false,\"default_profile_image\":false,\"following\":null,\"follow_request_sent\":null,\"notifications\":null},\"geo\":null,\"coordinates\":null,\"place\":null,\"contributors\":null,\"is_quote_status\":false,\"quote_count\":0,\"reply_count\":0,\"retweet_count\":0,\"favorite_count\":0,\"entities\":{\"hashtags\":[{\"text\":\"IoTCivicHack\",\"indices\":[56,69]}],\"urls\":[],\"user_mentions\":[],\"symbols\":[],\"media\":[{\"id\":987519167132831700,\"id_str\":\"987519167132831744\",\"indices\":[70,93],\"media_url\":\"http://pbs.twimg.com/media/DbRfc03XkAATN3c.jpg\",\"media_url_https\":\"https://pbs.twimg.com/media/DbRfc03XkAATN3c.jpg\",\"url\":\"https://t.co/5pRSCGJGE2\",\"display_url\":\"pic.twitter.com/5pRSCGJGE2\",\"expanded_url\":\"https://twitter.com/_viperboy_/status/987519171704520706/photo/1\",\"type\":\"photo\",\"sizes\":{\"large\":{\"w\":1536,\"h\":2048,\"resize\":\"fit\"},\"thumb\":{\"w\":150,\"h\":150,\"resize\":\"crop\"},\"medium\":{\"w\":900,\"h\":1200,\"resize\":\"fit\"},\"small\":{\"w\":510,\"h\":680,\"resize\":\"fit\"}}}]},\"extended_entities\":{\"media\":[{\"id\":987519167132831700,\"id_str\":\"987519167132831744\",\"indices\":[70,93],\"media_url\":\"http://pbs.twimg.com/media/DbRfc03XkAATN3c.jpg\",\"media_url_https\":\"https://pbs.twimg.com/media/DbRfc03XkAATN3c.jpg\",\"url\":\"https://t.co/5pRSCGJGE2\",\"display_url\":\"pic.twitter.com/5pRSCGJGE2\",\"expanded_url\":\"https://twitter.com/_viperboy_/status/987519171704520706/photo/1\",\"type\":\"photo\",\"sizes\":{\"large\":{\"w\":1536,\"h\":2048,\"resize\":\"fit\"},\"thumb\":{\"w\":150,\"h\":150,\"resize\":\"crop\"},\"medium\":{\"w\":900,\"h\":1200,\"resize\":\"fit\"},\"small\":{\"w\":510,\"h\":680,\"resize\":\"fit\"}}}]},\"favorited\":false,\"retweeted\":false,\"possibly_sensitive\":false,\"filter_level\":\"low\",\"lang\":\"en\",\"timestamp_ms\":\"1524277892410\"}",
      "payloadType":"json",
      "repeat":"",
      "crontab":"",
      "once":false,
      "x":140,
      "y":500,
      "wires":[
         [
            "a625aa99.53ef38"
         ]
      ]
   },
   {
      "id":"4892db3e.cb4a74",
      "type":"debug",
      "z":"e166925b.1b30f",
      "name":"",
      "active":true,
      "tosidebar":true,
      "console":false,
      "tostatus":false,
      "complete":"template",
      "x":830,
      "y":280,
      "wires":[

      ]
   },
   {
      "id":"17a2322c.73c4f6",
      "type":"visual-recognition-v3",
      "z":"e166925b.1b30f",
      "name":"",
      "vr-service-endpoint":"https://gateway.watsonplatform.net/visual-recognition/api",
      "image-feature":"classifyImage",
      "lang":"en",
      "x":610,
      "y":360,
      "wires":[
         [
            "c86730cb.a23ff8",
            "a19bdfc5.9a805"
         ]
      ]
   },
   {
      "id":"48b26b2f.dbca5c",
      "type":"inject",
      "z":"e166925b.1b30f",
      "name":"callforcode tweet",
      "topic":"",
      "payload":"{\"created_at\":\"Wed Jun 20 12:42:35 +0000 2018\",\"id\":1009416219265466400,\"id_str\":\"1009416219265466368\",\"text\":\".@UNHumanRights, @RedCross, @LinuxFoundation et @IBM lancent une initiative globale : #CallForCode. Si vous êtes un… https://t.co/6a2FsNvpRb\",\"source\":\"<a href=\\\"http://twitter.com\\\" rel=\\\"nofollow\\\">Twitter Web Client</a>\",\"truncated\":true,\"in_reply_to_status_id\":null,\"in_reply_to_status_id_str\":null,\"in_reply_to_user_id\":null,\"in_reply_to_user_id_str\":null,\"in_reply_to_screen_name\":null,\"user\":{\"id\":1920701377,\"id_str\":\"1920701377\",\"name\":\"Stéphan SOULLIER\",\"screen_name\":\"SoullierS\",\"location\":\"Lille - France\",\"url\":\"http://fr.linkedin.com/in/StephanSoullier\",\"description\":\"Client Exec #IBM_France. Living in Lille, wonderful main town of North of France. #IBMWatson #Digital #IoT #Cloud #IBMGDPR #proud2beIBMer Opinions are my own\",\"translator_type\":\"none\",\"protected\":false,\"verified\":false,\"followers_count\":2136,\"friends_count\":1909,\"listed_count\":56,\"favourites_count\":3518,\"statuses_count\":4182,\"created_at\":\"Mon Sep 30 16:59:45 +0000 2013\",\"utc_offset\":null,\"time_zone\":null,\"geo_enabled\":true,\"lang\":\"fr\",\"contributors_enabled\":false,\"is_translator\":false,\"profile_background_color\":\"C0DEED\",\"profile_background_image_url\":\"http://abs.twimg.com/images/themes/theme1/bg.png\",\"profile_background_image_url_https\":\"https://abs.twimg.com/images/themes/theme1/bg.png\",\"profile_background_tile\":false,\"profile_link_color\":\"1DA1F2\",\"profile_sidebar_border_color\":\"C0DEED\",\"profile_sidebar_fill_color\":\"DDEEF6\",\"profile_text_color\":\"333333\",\"profile_use_background_image\":true,\"profile_image_url\":\"http://pbs.twimg.com/profile_images/439339981752897537/zFVlS2wf_normal.png\",\"profile_image_url_https\":\"https://pbs.twimg.com/profile_images/439339981752897537/zFVlS2wf_normal.png\",\"profile_banner_url\":\"https://pbs.twimg.com/profile_banners/1920701377/1393581744\",\"default_profile\":true,\"default_profile_image\":false,\"following\":null,\"follow_request_sent\":null,\"notifications\":null},\"geo\":null,\"coordinates\":null,\"place\":null,\"contributors\":null,\"is_quote_status\":false,\"extended_tweet\":{\"full_text\":\".@UNHumanRights, @RedCross, @LinuxFoundation et @IBM lancent une initiative globale : #CallForCode. Si vous êtes un.e https://t.co/uvvpUQsVgl qui veut voir de vrais changements dans le monde et aider à sauver des vies. https://t.co/mY0vYFUSg6 https://t.co/mD0C5QIWJ7\",\"display_text_range\":[0,266],\"entities\":{\"hashtags\":[{\"text\":\"CallForCode\",\"indices\":[86,98]}],\"urls\":[{\"url\":\"https://t.co/uvvpUQsVgl\",\"expanded_url\":\"http://xn--dveloppeur-b7a.se\",\"display_url\":\"développeur.se\",\"indices\":[118,141]},{\"url\":\"https://t.co/mY0vYFUSg6\",\"expanded_url\":\"http://ibm.biz/BdZtnj\",\"display_url\":\"ibm.biz/BdZtnj\",\"indices\":[219,242]}],\"user_mentions\":[{\"screen_name\":\"UNHumanRights\",\"name\":\"UN Human Rights\",\"id\":69231187,\"id_str\":\"69231187\",\"indices\":[1,15]},{\"screen_name\":\"RedCross\",\"name\":\"_meric_n Red Cr_ss\",\"id\":6519522,\"id_str\":\"6519522\",\"indices\":[17,26]},{\"screen_name\":\"linuxfoundation\",\"name\":\"The Linux Foundation\",\"id\":14706299,\"id_str\":\"14706299\",\"indices\":[28,44]},{\"screen_name\":\"IBM\",\"name\":\"IBM\",\"id\":18994444,\"id_str\":\"18994444\",\"indices\":[48,52]}],\"symbols\":[],\"media\":[{\"id\":1002218356982808600,\"id_str\":\"1002218356982808576\",\"indices\":[243,266],\"media_url\":\"https//pbs.twimg.com/media/DgE3CxhX0AAjLS_.jpg\",\"media_url_https\":\"https://pbs.twimg.com/media/DgE3CxhX0AAjLS_.jpg\",\"url\":\"https://t.co/mD0C5QIWJ7\",\"display_url\":\"pic.twitter.com/mD0C5QIWJ7\",\"expanded_url\":\"https://twitter.com/IBM_France/status/1002218358601846784/photo/1\",\"type\":\"photo\",\"sizes\":{\"thumb\":{\"w\":150,\"h\":150,\"resize\":\"crop\"},\"large\":{\"w\":800,\"h\":418,\"resize\":\"fit\"},\"small\":{\"w\":680,\"h\":355,\"resize\":\"fit\"},\"medium\":{\"w\":800,\"h\":418,\"resize\":\"fit\"}},\"source_status_id\":1002218358601846800,\"source_status_id_str\":\"1002218358601846784\",\"source_user_id\":29704444,\"source_user_id_str\":\"29704444\"}]},\"extended_entities\":{\"media\":[{\"id\":1002218356982808600,\"id_str\":\"1002218356982808576\",\"indices\":[243,266],\"media_url\":\"http://pbs.twimg.com/media/DeiYSSNWAAAI_zJ.jpg\",\"media_url_https\":\"https://pbs.twimg.com/media/DeiYSSNWAAAI_zJ.jpg\",\"url\":\"https://t.co/mD0C5QIWJ7\",\"display_url\":\"pic.twitter.com/mD0C5QIWJ7\",\"expanded_url\":\"https://twitter.com/IBM_France/status/1002218358601846784/photo/1\",\"type\":\"photo\",\"sizes\":{\"thumb\":{\"w\":150,\"h\":150,\"resize\":\"crop\"},\"large\":{\"w\":800,\"h\":418,\"resize\":\"fit\"},\"small\":{\"w\":680,\"h\":355,\"resize\":\"fit\"},\"medium\":{\"w\":800,\"h\":418,\"resize\":\"fit\"}},\"source_status_id\":1002218358601846800,\"source_status_id_str\":\"1002218358601846784\",\"source_user_id\":29704444,\"source_user_id_str\":\"29704444\"}]}},\"quote_count\":0,\"reply_count\":0,\"retweet_count\":0,\"favorite_count\":0,\"entities\":{\"hashtags\":[{\"text\":\"CallForCode\",\"indices\":[86,98]}],\"urls\":[{\"url\":\"https://t.co/6a2FsNvpRb\",\"expanded_url\":\"https://twitter.com/i/web/status/1009416219265466368\",\"display_url\":\"twitter.com/i/web/status/1…\",\"indices\":[117,140]}],\"user_mentions\":[{\"screen_name\":\"UNHumanRights\",\"name\":\"UN Human Rights\",\"id\":69231187,\"id_str\":\"69231187\",\"indices\":[1,15]},{\"screen_name\":\"RedCross\",\"name\":\"_meric_n Red Cr_ss\",\"id\":6519522,\"id_str\":\"6519522\",\"indices\":[17,26]},{\"screen_name\":\"linuxfoundation\",\"name\":\"The Linux Foundation\",\"id\":14706299,\"id_str\":\"14706299\",\"indices\":[28,44]},{\"screen_name\":\"IBM\",\"name\":\"IBM\",\"id\":18994444,\"id_str\":\"18994444\",\"indices\":[48,52]}],\"symbols\":[]},\"favorited\":false,\"retweeted\":false,\"possibly_sensitive\":false,\"filter_level\":\"low\",\"lang\":\"fr\",\"timestamp_ms\":\"1529498555376\"}",
      "payloadType":"json",
      "repeat":"",
      "crontab":"",
      "once":false,
      "onceDelay":0.1,
      "x":120,
      "y":540,
      "wires":[
         [
            "a625aa99.53ef38"
         ]
      ]
   },
   {
      "id":"bfdd1c14.f484d8",
      "type":"ui_ui_control",
      "z":"e166925b.1b30f",
      "name":"",
      "x":1020,
      "y":240,
      "wires":[
         [

         ]
      ]
   },
   {
      "id":"5a33565a.fc9bb",
      "type":"ui_group",
      "z":"e166925b.1b30f",
      "name":"Tweet",
      "tab":"32fe664e.e812a2",
      "order":1,
      "disp":true,
      "width":"9"
   },
   {
      "id":"5402acbe.dcd3ec",
      "type":"ui_group",
      "z":"",
      "name":"Results",
      "tab":"32fe664e.e812a2",
      "order":2,
      "disp":true,
      "width":"9"
   },
   {
      "id":"caba2314.a97f3",
      "type":"ui_group",
      "z":"",
      "name":"Sentiment",
      "tab":"32fe664e.e812a2",
      "order":3,
      "disp":false,
      "width":"8"
   },
   {
      "id":"32fe664e.e812a2",
      "type":"ui_tab",
      "z":"e166925b.1b30f",
      "name":"Twitter Image Analysis",
      "icon":"dashboard",
      "order":2
   }
]
```

