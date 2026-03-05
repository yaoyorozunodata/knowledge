---
description: GitHubでメールアドレス流出を防ぐための設定
version: 1.1
date: 2026-03-05
tags: github, email, privacy, security, git
---

# GitHubでメールアドレス流出を防ぐための設定

## 公開プロフィールでメールを出さない運用

### 公開プロフィールの設定

1. GitHub 右上アイコンから `Settings` を開く
2. 左メニュー `Public profile` を開く
3. `Public email` を未設定にする（公開しない）
4. `Bio / URL / Social accounts` にメールアドレスを書かない

### 公開プロフィールに関する注意点

- `Settings > Public profile` の `Public email` は未設定（公開しない）
- プロフィール本文（Bio / URL / Social accounts）にメールを書かない
- 既に公開済みコミットのメールは、後から設定変更しても自動では消えない

## user.emailで実メールを使う場合

### Emailsに関する設定

1. GitHub 右上アイコンから `Settings` を開く
2. 左メニュー `Emails` を開く
3. `Keep my email addresses private` を **ON** にする
4. `Block command line pushes that expose my email` を **OFF** にする

### 実メール運用の注意

- Publicリポジトリに実メールで誤pushする事故が起き得る可能性がある
- Privateリポジトリでは実メールが表示されるため、完全な隠蔽はできない
- コミット履歴に実メールが残るため、過去のコミットも注意が必要

## 実メールアドレスを完全に隠蔽する

### 完全に隠蔽するためのEmailsに関する設定

1. GitHub 右上アイコンから `Settings` を開く
2. 左メニュー `Emails` を開く
3. `Keep my email addresses private` を `ON` にする
4. `Block command line pushes that expose my email` を `ON` にする

### Git設定

- `user.email` は常に `ID+USERNAME@users.noreply.github.com` を使う
- グローバル設定を `noreply` に固定し、リポジトリごとの実メール上書きを禁止する

```bash
git config --global user.email "ID+USERNAME@users.noreply.github.com"
```

確認:

```bash
git config --global --get user.email
git log --format='%h %ae %an'
```

### 完全に隠蔽する運用での関する注意点

- Public/Private問わず、コミットメールが完全に隠蔽される
- コミットメールが完全に隠蔽されるため、メールアドレス流出のリスクが大幅に減る
- コミット履歴に実メールが記載されることがないため
- コミットメールが `noreply` になるため、他のユーザーがメールアドレスを知ることができなくなる
- ただし、既存のコミットは `noreply` メールに置き換えることはできないため、既存のコミット履歴には注意が必要
