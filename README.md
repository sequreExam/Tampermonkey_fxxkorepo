# Tampermonkey_fxxkrepo
ニコレポのいらない通知を消しました。

    // ==UserScript==
    // @name         fuckorepo
    // @namespace    http://tampermonkey.net/
    // @version      0.1
    // @description  try to take over the world!
    // @author       sequre
    // @match        http://www.nicovideo.jp/my/top
    // @grant        none
    // ==/UserScript==
    "use strict";

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

    (() =>
    {
        const startDeleteElement = () =>
        {
            const deleteElement = () =>
            {
                const elements = document.querySelectorAll('.NicorepoTimelineItem');
                for(let element of elements)
                {
                    for(let delItem of DELETE_CONTENT)
                    {
                        if(element.innerText.indexOf(delItem) > 0)
                        {
                            element.parentNode.removeChild(element);
                        }
                    }
                }
            }
            const target = document.querySelector('.NicorepoTimeline');
            const mo = new MutationObserver(deleteElement);
            mo.observe(target, {childList: true});

            deleteElement();
        }

        const target = document.querySelector('.nicorepo-page');
        const observer = new MutationObserver(startDeleteElement);
        const options = {childList: true};
        observer.observe(target, options);
    })();
