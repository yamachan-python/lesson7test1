# QRコード生成ツール（Flask）

入力した文字から QR コードの画像を作って表示する Web アプリです。
使うライブラリは Flask・qrcode・Pillow と、公開用のサーバーの gunicorn です。

## 手元で動かす

```
python -m venv env
```

仮想環境を有効にします。

- Windows：`env\Scripts\activate`
- Mac：`source env/bin/activate`（Mac は最初の行も `python3 -m venv env`）
- Windows の PowerShell で「スクリプトの実行が無効」と出たら：`Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` を1回打つか、コマンドプロンプトに切り替えて打ちます。

```
pip install -r requirements.txt
python app.py
```

ブラウザで `http://localhost:8000` を開きます。

## Render で公開する

- Runtime：Python
- Build Command：`pip install -r requirements.txt`
- Start Command：`gunicorn app:app`（`python app.py` でも動きますが、公開には gunicorn を使います。gunicorn は Windows では動かないので、手元は `python app.py` です）
- Python の版を決めておきたい時は、環境変数 `PYTHON_VERSION` に `3.14.10` のように最後の数字まで入れます（2026年11月に新しく作るサービスの既定と同じ版です）。

この requirements.txt の版は、Python 3.12〜3.15 で入ることを確かめています（2026年11月）。

## うまく動かない時

- `pip install` が止まる：古い requirements.txt を使っていないか確かめます（`Pillow==10.4.0` は Python 3.14 では入りません）。
- `ModuleNotFoundError`：requirements.txt を GitHub に push し忘れていないか確かめます。
- 余白は 1〜20 の範囲だけを受け付けます。
