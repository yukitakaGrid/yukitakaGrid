<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/banner-light.svg">
  <img alt="Boids の軌跡を描いたバナー画像" src="assets/banner-dark.svg" width="100%">
</picture>

# yukitakaGrid

インタラクション、ジェネラティブアート、CG（シェーダー）を作っています。本業は土木技術者です。  
<sub>I build interactive and generative work and real-time graphics. Civil engineer by day.</sub>

<p>
  <img alt="Unity" src="https://img.shields.io/badge/Unity-000000?style=flat-square&logo=unity&logoColor=white">
  <img alt="TouchDesigner" src="https://img.shields.io/badge/TouchDesigner-000000?style=flat-square">
  <img alt="Processing" src="https://img.shields.io/badge/Processing-006699?style=flat-square&logo=processingfoundation&logoColor=white">
  <img alt="GLSL" src="https://img.shields.io/badge/GLSL-5586A4?style=flat-square&logo=opengl&logoColor=white">
  <img alt="Three.js" src="https://img.shields.io/badge/Three.js-000000?style=flat-square&logo=threedotjs&logoColor=white">
  <img alt="Python" src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white">
  <img alt="C#" src="https://img.shields.io/badge/C%23-512BD4?style=flat-square&logo=dotnet&logoColor=white">
  <img alt="Node.js" src="https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white">
  <img alt="Arduino / ESP32" src="https://img.shields.io/badge/Arduino%20%2F%20ESP32-00878F?style=flat-square&logo=arduino&logoColor=white">
</p>

## 作品

<table>
  <tr>
    <td width="50%"><img alt="水面の上に、白い鳥の群れが光りながら飛んでいる" src="assets/tsukinokame-s4-birds.jpg"></td>
    <td width="50%"><img alt="灰色の夜空に満月。その下に小さな鳥の群れが輪になって舞う" src="assets/tsukinokame-s7-moon.jpg"></td>
  </tr>
  <tr>
    <td align="center"><sub>ツキノカメ（静止画）</sub></td>
    <td align="center"><sub>ツキノカメ（静止画）</sub></td>
  </tr>
</table>

| 年 | 作品 | 内容 |
|---|---|---|
| 2026 | ツキノカメ（制作中） | Web インタラクション／VJ／映像。Boids による鳥の群れを、水・月・結晶などの場面で見せる。 |
| 2026 | [tiny-hide-and-seek](https://github.com/yukitakaGrid/tiny-hide-and-seek) | 3D スキャンした空間で遊ぶ、小人サイズのオンラインかくれんぼ。依存なしの Node.js WebSocket サーバーと Three.js クライアント（BVH 物理、PWA プッシュ、Redis 永続化）。 |
| 2025 | [MorphCubes](#morphcubes) | 遠隔地の人の身体性を表現する、複数の環境ロボット型テレプレゼンス。形状が変わる家具型ロボットを使う。 |
| 2023 | [Tree of Souls](https://github.com/yukitakaGrid/TreeOfSouls) | Boids とフラクタルによるジェネラティブアート（JavaScript、p5.js）。Processing Community Day Tokyo 2023 で展示。 |
| 2023 | [KitAI](https://github.com/yukitakaGrid/KitAI) | ハッカソンで制作した、ChatGPT がコマンドを実装する Discord bot（Python）。 |

### MorphCubes

> [!NOTE]
> 論文 *MorphCubes: Adaptive Modular Robots for Dynamic Remote Human Embodiment*（Shima & Takashima）が **ACM CHI '25 Late-Breaking Work** に採択され、**INTERACTION 2025 インタラクティブ発表賞（PC 推薦）** を受賞しました。

```mermaid
flowchart LR
    A([遠隔地のユーザー]) -- 接続 --> B[Furniture Mode<br>机の高さの箱]
    B -- 変形 --> C[Embody Mode<br>人の背丈まで伸び、姿と手を投影]
    C -- 終了 --> B
```

<img alt="論文の図1。(a) 遠隔地のユーザー、(b) Furniture Mode、(c・d) 変形の途中、(e) Embody Mode" src="assets/morphcubes-fig1.jpg" width="100%">
<sub>図1：Shima & Takashima, CHI EA '25, ACM</sub>

普段は家具として置かれたモジュールが、通話時に人の背丈まで変形し、遠隔地のユーザーの姿と手を映します。

## Boids

ツキノカメと Tree of Souls は、どちらも Boids（各個体が近傍の個体だけを参照して動くモデル）を使っています。Tree of Souls では、個体の軌跡からデジタル彫刻を生成しています。

```js
// 近傍の個体だけを参照して、次の速度を決める
for (const b of birds) {
  const near = birds.filter(o => o !== b && dist(o, b) < RADIUS);
  b.vel.add(separation(b, near).mult(0.05)); // 分離
  b.vel.add(alignment(b, near).mult(0.04));  // 整列
  b.vel.add(cohesion(b, near).mult(0.004));  // 結合
  b.pos.add(b.vel.limit(MAX_SPEED));
  b.trail.push(b.pos.copy());                // 軌跡を保存
}
```

## そのほかのリポジトリ

<table>
  <tr>
    <td width="50%" valign="top">
      <a href="https://github.com/yukitakaGrid/pcx_test">
        <picture>
          <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api/pin/?username=yukitakaGrid&repo=pcx_test&theme=github_dark&hide_border=true">
          <img alt="pcx_test — 点群から kd-tree のデータ構造を作った（C# / Unity）" src="https://github-readme-stats.vercel.app/api/pin/?username=yukitakaGrid&repo=pcx_test&theme=default&hide_border=true">
        </picture>
      </a>
    </td>
    <td width="50%" valign="top">
      <a href="https://github.com/yukitakaGrid/Nebula">
        <picture>
          <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api/pin/?username=yukitakaGrid&repo=Nebula&theme=github_dark&hide_border=true">
          <img alt="Nebula — 16ms #0 GLSL Graphics Compo の提出作品（GLSL）" src="https://github-readme-stats.vercel.app/api/pin/?username=yukitakaGrid&repo=Nebula&theme=default&hide_border=true">
        </picture>
      </a>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <a href="https://github.com/yukitakaGrid/LightEffects">
        <picture>
          <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api/pin/?username=yukitakaGrid&repo=LightEffects&theme=github_dark&hide_border=true">
          <img alt="LightEffects — LED キューブのアニメーションを作る Unity 製 GUI ツール（C#）" src="https://github-readme-stats.vercel.app/api/pin/?username=yukitakaGrid&repo=LightEffects&theme=default&hide_border=true">
        </picture>
      </a>
    </td>
    <td width="50%" valign="top">
      <a href="https://github.com/yukitakaGrid/LightAnimationController">
        <picture>
          <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api/pin/?username=yukitakaGrid&repo=LightAnimationController&theme=github_dark&hide_border=true">
          <img alt="LightAnimationController — 物理演算やライフゲームなどで動かすアニメーション制御ソフト（Processing）" src="https://github-readme-stats.vercel.app/api/pin/?username=yukitakaGrid&repo=LightAnimationController&theme=default&hide_border=true">
        </picture>
      </a>
    </td>
  </tr>
</table>

<details>
<summary><b>経歴・受賞</b></summary>

| 時期 | こと |
|---|---|
| 2025.11 | Generative VJ：BSP によるビル群のサイズ・高さの動的変容を用いた演出 |
| 2025.4〜 | 土木技術者 |
| 2025.3 | 芝浦工業大学 電子情報システム学科 卒業。卒業論文は MorphCubes |
| 2025.3 | INTERACTION 2025 インタラクティブ発表賞（PC 推薦） |
| 2025.2 | ACM CHI '25 Late-Breaking Work 採択 |
| 2023.10 | 16ms #0（GLSL Graphics Compo）：fBm ノイズによる星雲シミュレーションを提出 → [Nebula](https://github.com/yukitakaGrid/Nebula) |
| 2023.6 | Processing Community Day Tokyo 2023：Boids の軌跡によるデジタル彫刻 |

</details>

<details>
<summary><b>技術領域</b></summary>

HCI／メディアアート／CG（GPGPU・シェーダー）／VR・AR・MR／プロジェクションマッピング／自然シミュレーション／ジェネラティブデザイン

</details>

<details>
<summary><b>English (short)</b></summary>

Interactive and generative work. **Tsukinokame** (web / VJ / moving image, in progress), **MorphCubes** (modular shape-changing robots for remote human embodiment; CHI '25 Late-Breaking Work, INTERACTION 2025 Interactive Presentation Award), **Tree of Souls** (Boids and fractals; Processing Community Day Tokyo 2023). Civil engineer by day.

</details>

## GitHub 統計

<p>
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=yukitakaGrid&theme=github_dark">
    <img alt="GitHub プロフィールの集計カード（読み込めないときは、このカードは出ません）" src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=yukitakaGrid&theme=github" height="150px">
  </picture>
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api/top-langs/?username=yukitakaGrid&layout=compact&count_private=true&theme=github_dark&hide_border=true">
    <img alt="よく使う言語（読み込めないときは、このカードは出ません）" src="https://github-readme-stats.vercel.app/api/top-langs/?username=yukitakaGrid&layout=compact&count_private=true&theme=default&hide_border=true" height="150px">
  </picture>
</p>

