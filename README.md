# wordpress-ansible-sakura

は、さくらのレンタルサーバーに WordPress を設置するための Ansible Playbook です。

## Setup

Mac の場合、 Homebrew 経由でインストールするのが楽でしょう。

```bash
$ brew install ansible
```

## さくらのレンタルサーバ初期設定

### 公開鍵の設置

まず Ansible を使い、 SSH で入れるようにします。

```bash
$ ssh username@username.sakura.ne.jp
$ echo '公開鍵の内容' > ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys
```

### Ansible 疎通確認

```bash
$ ansible -i hosts username.sakura.ne.jp -m ping
```

### 管理画面にログインし DB 作成

DB を作成したらサーバーが割り当てられるため、管理画面から作成する。

https://secure.sakura.ad.jp/menu/top/

たとえば、

* (username)_wp_production
* (username)_wp_staging

という名前で DB を作成する。文字コードは UTF-8 で。十分に強い強度のパスワードを指定すること。

### 設定したパスワードを保存

設定したパスワードを host_vars に保存します。

### Play it!

```bash
$ ansible-playbook -i hosts sites.yml --extra-vars env=staging --ask-vault-pass
```

### ドメイン設定

最後にさくらの管理画面からドメインの設定をすれば完了
