# Generate Direct Method Cash Flow Statement from Trial Balance
# 残高試算表から直接法キャッシュフロー計算書(簡易)を自動生成

## 概要 (Overview)
このプログラムは、ExcelまたはCSV形式の「残高試算表（Trial Balance）」を読み込み、**直接法によるキャッシュフロー計算書（Cash Flow Statement by Direct Method）**を自動で算出してExcel形式で出力するPythonスクリプトです。

間接法ではなく、売上や仕入、人件費など営業活動の実際のキャッシュフローを、各勘定科目の増減高と発生額から推計します。

## 必須要件 (Requirements)
- Python 3.8 以上
- 必要なライブラリ：
  - `pandas`
  - `openpyxl`

## インストール方法 (Installation)

```bash
# リポジトリをクローンまたはダウンロード後、ディレクトリに移動
cd path/to/cashflow_generator

# 必要なパッケージをインストール
pip install -r requirements.txt
```

## 使い方 (Usage)

残高試算表のファイル（ExcelまたはCSV）を用意し、コマンドラインから実行します。

```bash
python cashflow_direct.py <入力ファイル名> [-o <出力ファイル名>]
```

### 実行例
```bash
python cashflow_direct.py data.csv -o output_CF.xlsx
```

## 入力データの形式 (Input Data Format)
本プログラムは、以下のような一般的な「残高試算表」の列構造を自動で検知して読み込みます。
- 勘定科目コード
- **勘定科目名** (必須)
- **前月残高** または **期首残高** (必須)
- 借方
- 貸方
- **当月残高** または **期末残高** (必須)

※ 列名が見つからない場合は、一般的な配列（B列が科目名、C列が前月残高…）を想定して処理を継続します。

## 注意事項 (Notes)
当プログラムの直接法キャッシュフローの算出ロジックは、科目名に含まれるキーワード（「売掛金」「買掛金」「給与」など）を用いて概算する仕組みです。会社独自の特殊な勘定科目名を使用している場合は、ソースコードの `get_account(["キーワード"])` 部分を修正してご活用ください。

## Webでの公開方法 (Deploying to the Web)

本アプリケーションは **Streamlit** で作成されているため、無料で Web 上に公開することができます。一番簡単でおすすめなのは「[Streamlit Community Cloud](https://share.streamlit.io/)」を利用する方法です。

### 手順（Streamlit Community Cloud を使う場合）

1. **GitHub にアップロードする**
   このフォルダ一式（`app.py`、`cashflow_direct.py`、`requirements.txt`など）を、ご自身の GitHub アカウントにアップロード（プッシュ）します。
   > **【重要】** 残高試算表などの Excel/CSV データや PDF ファイルは個人情報や機密データが含まれるため、絶対に一緒にアップロードしないでください。すでに本フォルダには、機密ファイルがアップロードされないよう `.gitignore` を設定済みです。

2. **Streamlit Community Cloud にログインする**
   [Streamlit Community Cloud](https://share.streamlit.io/) にアクセスし、GitHub アカウントでサインインします。

3. **アプリをデプロイする**
   - 「**New app**」ボタンをクリックします。
   - 作成した GitHub リポジトリ（Repository）を選択します。
   - ブランチ（Branch）は通常 `main` を選びます。
   - `Main file path` には `app.py` を入力します。
   - 「**Deploy**」ボタンを押すと、数分でアプリが Web 上で公開されます。

公開された URL は他の人と共有でき、ブラウザ上から Excel/CSV ファイルをアップロードしてキャッシュフローを計算できるようになります。
