# Dear ImGui for Visual Studio 6.0 (VC++6.0)

このプロジェクトは、Visual Studio 6.0 (VC++6.0) でのDear ImGuiをOpenGL（GLFWを使わない）とDirectX9に対応させたものです。

## 概要

Dear ImGuiは通常、近代的なC++コンパイラでのビルドを前提としていますが、このプロジェクトではVC++6.0でもビルドできるように修正を加えています。さらに、DirectX9でのドッキングビュー（Docking）機能にも対応しています。

## 特徴

- **Visual Studio 6.0 (VC++6.0) 対応**: 古いコンパイラでもImGuiを使用可能
- **OpenGL2 サポート**: GLFWを使わない軽量なOpenGL実装
- **DirectX9 サポート**: DirectX9による描画
- **ドッキング機能**: ウィンドウのドッキング・アンドッキングに対応
- **マルチビューポート**: 複数のウィンドウ表示機能

## ビルド対象

このプロジェクトには2つのサンプルアプリケーションが含まれています：

1. **vs6_dx9** - DirectX9を使用したサンプル
2. **vs6_opengl** - OpenGL2を使用したサンプル

## オリジナルImGuiからの主な変更点

### 1. VC++6.0 互換性のための修正

#### C++11機能の対応
- `constexpr` キーワードの無効化
  ```cpp
  #if _MSC_VER <= 1200
  #define constexpr
  #endif
  ```

- `nullptr` の定義
  ```cpp
  #ifndef _INTPTR_T_DEFINED
  #define _INTPTR_T_DEFINED
  typedef int intptr_t;
  typedef unsigned int uintptr_t;
  #define nullptr 0
  #endif
  ```

#### コンパイラ固有の修正
- `imgui_widgets.cpp` でVC++6.0用の条件分岐を追加
- `main_opengl.cpp` でVC++6.0用のWinMain関数を使用

### 2. プラットフォーム対応

#### DirectX9対応
- `imgui_impl_dx9.cpp/h` - DirectX9レンダラー実装
- DirectX9 SDKのインクルードとライブラリ
- 独自のDirectX9描画パイプライン

#### OpenGL2対応
- `imgui_impl_opengl2.cpp/h` - OpenGL2レンダラー実装
- GLFWを使わない軽量な実装
- Win32 APIを直接使用

#### Win32プラットフォーム
- `imgui_impl_win32.cpp/h` - Win32ウィンドウシステム対応

### 3. ドッキング機能の有効化

両方のサンプルでドッキング機能を有効にしています：
```cpp
io.ConfigFlags |= ImGuiConfigFlags_DockingEnable;         // ドッキング有効
io.ConfigFlags |= ImGuiConfigFlags_ViewportsEnable;       // マルチビューポート有効
```

## ファイル構成

### コアファイル
- `imgui.h/cpp` - ImGuiメインライブラリ
- `imgui_internal.h` - 内部API定義
- `imgui_demo.cpp` - デモウィンドウ
- `imgui_draw.cpp` - 描画機能
- `imgui_tables.cpp` - テーブル機能
- `imgui_widgets.cpp` - UI部品

### プラットフォーム実装
- `imgui_impl_dx9.h/cpp` - DirectX9バックエンド
- `imgui_impl_opengl2.h/cpp` - OpenGL2バックエンド
- `imgui_impl_win32.h/cpp` - Win32プラットフォーム

### サンプルアプリケーション
- `main_dx9.cpp` - DirectX9サンプル
- `main_opengl.cpp` - OpenGL2サンプル

### プロジェクトファイル
- `vs6_dx9.dsp/dsw` - DirectX9プロジェクト
- `vs6_opengl.dsp/dsw` - OpenGLプロジェクト

### 設定ファイル
- `imconfig.h` - コンパイル時設定
- `imgui.ini` - 実行時設定（自動生成）

### STBライブラリ
- `imstb_rectpack.h` - 矩形パッキング
- `imstb_textedit.h` - テキスト編集
- `imstb_truetype.h` - TrueTypeフォント
- `stb_image.h` - 画像読み込み

## ビルド方法

### 前提条件
- Visual Studio 6.0 (Visual C++ 6.0)
- DirectX9 SDK（DirectX9版をビルドする場合）

### DirectX9版のビルド
1. `vs6_dx9.dsw` を開く
2. プロジェクトをビルド
3. `Debug/vs6_dx9.exe` が生成される

### OpenGL版のビルド
1. `vs6_opengl.dsw` を開く
2. プロジェクトをビルド
3. `Debug/vs6_opengl.exe` が生成される

## 動作確認済み環境

- Windows XP/Vista/7/8/10/11
- Visual Studio 6.0 with Service Pack 6
- DirectX9 SDK (June 2010)

## ライセンス

このプロジェクトは、オリジナルのDear ImGuiと同じMITライセンスに従います。

## 参考リンク

- [Dear ImGui 公式](https://github.com/ocornut/imgui)
- [Dear ImGui Documentation](https://github.com/ocornut/imgui/wiki)
- [DirectX9 SDK](https://www.microsoft.com/en-us/download/details.aspx?id=6812)