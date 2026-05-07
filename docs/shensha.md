# 神煞まとめ | 神煞总览 | Shensha Summary

本ドキュメントは、Bazi MCP の `getBaziDetail` ツールが返す `神煞` フィールドに関する要約です。
This document summarizes the `神煞` (Shensha) field returned by the `getBaziDetail` tool.

## 神煞とは | What is Shensha

**神煞 (しんさつ / shénshà)** とは、八字命理学において干支の組み合わせから導かれる「吉凶星」の総称です。日主や年支・日支などを基準に算出され、各柱（年・月・日・時）に配置されることで、その人の運命・性格・人間関係に対する象意を補足的に示します。

- **神 (吉星 / auspicious stars)**: 福徳・才能・援助などの良い暗示。
- **煞 (凶星 / inauspicious stars)**: 災い・障害・トラブルなどの悪い暗示。

神煞は十神（比肩・正官・正財など）や五行のような根幹的な要素ではなく、あくまで補助的な情報として参照されます。

## 出力構造 | Output Structure

`getBaziDetail` は四柱（年柱・月柱・日柱・時柱）ごとに該当する神煞を配列で返します。

```json
{
  "神煞": {
    "年柱": ["国印", "亡神"],
    "月柱": ["天德合", "月德合", "天乙贵人", "太极贵人", "福星贵人", "金舆", "血刃", "华盖", "天喜", "元辰"],
    "日柱": ["天德合", "月德合", "桃花", "九丑", "童子煞"],
    "时柱": ["天乙贵人", "太极贵人", "福星贵人", "金舆", "血刃", "华盖", "天喜", "元辰", "童子煞"]
  }
}
```

実装は `src/lib/bazi.ts` の `buildGodsObject` 関数で、`cantian-tymext` パッケージの `getShen()` を呼び出しています。
The implementation lives in `src/lib/bazi.ts:62` (`buildGodsObject`), which calls `getShen()` from `cantian-tymext`.

## 主な神煞一覧 | Common Shensha

以下は出力例に登場する主要な神煞の意味早見表です。

### 吉星 | Auspicious

| 神煞 | 読み | 主な意味 (日本語) | Meaning (English) |
| --- | --- | --- | --- |
| 天乙贵人 | てんいつきじん | 最上級の貴人星。困難時に助けを得やすい。 | The highest "noble person" star; brings help in adversity. |
| 太极贵人 | たいきょくきじん | 学術・宗教・神秘学への適性。研究熱心。 | Affinity for scholarship, philosophy, and metaphysics. |
| 福星贵人 | ふくせいきじん | 衣食住に困らず、福徳を享受しやすい。 | Brings blessings, comfort, and material ease. |
| 国印 | こくいん | 権威・名誉・公職を象徴。リーダーシップ。 | Symbolizes authority, official rank, and leadership. |
| 天德合 | てんとくごう | 災いを和らげ、徳を増す吉星。 | Mitigates disasters and enhances virtue. |
| 月德合 | げっとくごう | 慈悲・善行に恵まれる。天德合と並ぶ吉星。 | Brings compassion and goodwill; pairs with 天德合. |
| 金舆 | きんよ | 財運・配偶縁。とくに「車（金の輿）」の象徴。 | Wealth and spouse luck; literally "golden carriage". |
| 天喜 | てんき | 慶事・婚姻・出産などの喜び事。 | Joyful events such as marriage and childbirth. |
| 红鸾 | こうらん | 婚姻・恋愛運の代表的な吉星。 | Romance and marriage luck. |
| 文昌贵人 | ぶんしょうきじん | 学業・試験・文才に有利。 | Favorable for study, exams, and literary talent. |
| 学堂 | がくどう | 学問・教養に縁がある。 | Affinity for learning and academia. |
| 驿马 | えきば | 移動・旅行・転職など変化を促す。 | Travel, relocation, and career changes. |

### 凶星 | Inauspicious

| 神煞 | 読み | 主な意味 (日本語) | Meaning (English) |
| --- | --- | --- | --- |
| 亡神 | もうしん | 喪失・隠匿・心労。慎重さが必要。 | Loss, concealment, and mental strain. |
| 血刃 | けつじん | 血光の災い・怪我・手術など。 | Risk of injury, surgery, or bloodshed. |
| 华盖 | かがい | 孤独・芸術・宗教性。孤高の星。 | Solitude, artistic and religious inclinations. |
| 元辰 | げんしん | 不和・障害・困難。とくに対人関係。 | Discord, obstacles, and interpersonal trouble. |
| 桃花 | とうか | 恋愛運。多すぎると色情の煩いに。 | Romance; in excess, indicates affairs and complications. |
| 九丑 | きゅうしゅう | 容姿・人間関係の煩い。慎重を要する。 | Troubles in appearance or relationships. |
| 童子煞 | どうじさつ | 幼少時の身体虚弱や信仰縁を示す。 | Frailty in youth; karmic ties to spirituality. |
| 劫煞 | ごうさつ | 突然の損失・盗難・トラブル。 | Sudden loss, theft, or accidents. |
| 灾煞 | さいさつ | 災難・事故。 | Calamity and accidents. |
| 孤辰 | こしん | 男性の孤独。配偶縁が薄い。 | Loneliness for men; weak spouse luck. |
| 寡宿 | かしゅく | 女性の孤独。配偶縁が薄い。 | Loneliness for women; weak spouse luck. |

> **注意 | Note**: 同じ神煞でも他の干支との組み合わせで作用が変化します。一つの神煞だけで吉凶を断定せず、八字全体・大運・流年と合わせて総合的に解釈してください。
> The effect of a single Shensha varies with surrounding stems and branches. Always interpret it together with the full chart, decade luck (大运), and annual luck (流年).

## 算出の基準柱 | Reference Pillars

神煞は柱ごとに算出基準が異なります（流派により差はありますが、`cantian-tymext` の実装に準拠）。

- **年柱・日柱を基準とするもの**: 天乙贵人、文昌贵人、桃花、驿马 など。
- **月支を基準とするもの**: 天德、月德、天德合、月德合 など。
- **日干を基準とするもの**: 金舆、福星贵人、太极贵人 など。
- **年支または日支を基準とするもの**: 华盖、将星、亡神、劫煞 など。

このため、同じ干支でも「日柱」「月柱」「時柱」のどこに現れるかで意味合いが変わります。

## 利用上の指針 | Usage Guidelines

1. **吉凶を単独で判断しない | Don't judge in isolation**
   神煞は十神・五行・刑冲合会に比べると影響度が小さいため、補助情報として扱う。
2. **柱の位置に注目 | Mind the pillar**
   年柱＝祖先・幼年、月柱＝両親・青年期、日柱＝配偶・本人、時柱＝子女・晩年。
   Year = ancestry/childhood, Month = parents/youth, Day = spouse/self, Hour = children/old age.
3. **大運・流年と組み合わせる | Combine with luck cycles**
   神煞が大運や流年で「冲」「合」されると、その年に作用が顕在化しやすい。
4. **流派差に留意 | Be aware of school differences**
   神煞の算出基準・解釈は流派によって異なる。本MCPは `cantian-tymext` の定義に従う。

## 参考 | References

- 実装: [`src/lib/bazi.ts`](../src/lib/bazi.ts) (`buildGodsObject`)
- 依存ライブラリ: [`cantian-tymext`](https://www.npmjs.com/package/cantian-tymext)
- 出力例: [README.md](../README.md) の `getBaziDetail` 結果例を参照。
