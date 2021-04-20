# jQuery10
## 一次レビューの修正内容
----------
#### 1. 「前へ」「次へ」ボタンの変更
 - e.preventDefault();を先頭にしました。
 - if文でのelseを消去しました。
 - currentPage = $('.counter-current').text(); を消去しました。

 ```Javascript
  // 変更前　「前へ」ボタン
  $(document).on('click', '[data-js="page-prev"]', function (e) {
    currentPage = $('.counter-current').text();
    currentPage--
    e.preventDefault();
    if ($('[data-js="page-prev"]').hasClass('disabled')) {
      return false;
    }
    resetPage();
    getBookData();
  })
  // 変更後
  $(document).on('click', '[data-js="page-prev"]', function (e) {
    e.preventDefault();
    if ($('[data-js="page-prev"]').hasClass('disabled')) {
      return false;
    }

    currentPage--
    resetPage();
    getBookData();
  })
```

#### 2. function名の変更
- Ajax() → getBookData() に変更しました。

#### 3. エラーメッセージ表示の関数化
- Ajax通信のfail時処理内に書いていた処理を関数化しました。
 ```Javascript
  function alertError(data) {
    switch(data.status) {
      case 0:
        showMessage('<p class="error_message">通信に失敗しました。インターネットの接続をご確認ください。</p>')
        break;
      case 400:
        showMessage('<p class="error_message">検索文字が入力されていません。</p>')
        break;
      case 429:
        showMessage('<p class="error_message">リクエスト過多です。しばらく時間を置いてからお試しください。</p>')
        break;
      default:
        showMessage('<p class="error_message">予期せぬエラーが発生しました。</p>')
    }
  }
```

#### 4. 0件の時の処理の記載箇所を移動
- function showBookList内に書いていた以下の処理を.done内に移動しました。
 ```Javascript
  if (data.count === 0) {
    resetPage();
    showMessage('検索結果が見つかりませんでした。<br>別のキーワードで検索して下さい。');
    return false;
  }
```






