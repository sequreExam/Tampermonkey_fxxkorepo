# fxxkrepo
    // ==UserScript==
    // @name         fuckorepo
    // @namespace    http://tampermonkey.net/
    // @version      0.1
    // @description  try to take over the world!
    // @author       sequre
    // @match        http://www.nicovideo.jp/my/top
    // @grant        none
    // ==/UserScript==

    // ここに削除したい文字列を書く
    const DELETE_CONTENT =
        [
          "生放送を開始しました。",
          "生放送を予約しました。",
          "記事を投稿しました。",
          "生放送が開始されました。",
          "達成しました。",
          "動画を登録しました。",
          "宣伝しました。",
          "紹介されました。",
          "クリップしました。",
          "マンガをお気に入りしました。",
          "ニコニ広告しました。",
          "立体をお気に入り登録しました。"
        ];

    (function()
    {
      'use strict';
      function startDeleteElement()
      {
        function deleteElement()
        {
          var elements = document.querySelectorAll('.NicorepoTimelineItem');
          for (let element of elements)
          {
            for (let delItem of DELETE_CONTENT)
            {
              if(element.innerText.indexOf(delItem) > 0)
              {
                element.parentNode.removeChild(element);
              }
            }
          }
        }
        var target = document.querySelector('.NicorepoTimeline');
        var mo = new MutationObserver(deleteElement);
        mo.observe(target, {childList: true});

        deleteElement();
      }

      var target = document.querySelector('.nicorepo-page');
      var observer = new MutationObserver(startDeleteElement);
      var options = {childList: true};
      observer.observe(target, options);
    })();
