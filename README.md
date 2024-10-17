# auto-release-trial

コミットによるリリースタグ作成のお試しリポジトリです。
詳しくは`package.json`, `.github/workflows/release.yml`を参照してください。
ここでは簡単な説明を記載します。

## リリースタグの作成方法

`release`ブランチへのコミットをトリガーにリリースタグが作成されます。
ここで言うコミットとは、直接のコミットはもちろんのこと、マージコミットも含みます。

## リリースタグの命名規則

リリースタグは`vX.Y.Z`の形式で作成されます。

値は前回のリリースから最新のコミットまでのすべてのコミットメッセージを取得し、それに基づいてバージョンアップを行います。

## コミットメッセージのフォーマット

コミットメッセージの内容によってバージョンが決まるので、コミットメッセージも一定のフォーマットに従う必要があります。

本リポジトリでは[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)に従っています。

例えば機能改修を行った場合は、`feat: 新機能の追加`のようにコミットメッセージを記述します。
例えばバグ修正を行った場合は、`fix: バグの修正`のようにコミットメッセージを記述します。

コミットメッセージの頭のキーワードによってバージョンアップが行われます。

| パターン          | バージョンアップ       |
| ----------------- | ---------------------- |
| `fix`             | Z を+1                 |
| `feat`            | Y を+1, Z を 0         |
| `BREAKING CHANGE` | X を+1, Y を 0, Z を 0 |
| `patch`           | Z を+1                 |
| `minor`           | Y を+1, Z を 0         |
| `major`           | X を+1, Y を 0, Z を 0 |

## 実際の例

### マイナーバージョンアップ

- https://github.com/sahksas/auto-release-trial/pull/20/commits

この PR では`minor: update`というコミットメッセージが含まれています。

- https://github.com/sahksas/auto-release-trial/actions/runs/11384025069

`dev`から`release`へのマージコミットによって GithubActions が実行され、

- https://github.com/sahksas/auto-release-trial/releases/tag/v0.2.0

リリースタグ v0.2.0 が作成されました。

### パッチバージョンアップ

- https://github.com/sahksas/auto-release-trial/pull/21/commits

この PR では`patch: update`というコミットメッセージが含まれています。

- https://github.com/sahksas/auto-release-trial/actions/runs/11384166803

`dev`から`release`へのマージコミットによって GithubActions が実行され、

- https://github.com/sahksas/auto-release-trial/releases/tag/v0.2.1

リリースタグ v0.2.1 が作成されました。
