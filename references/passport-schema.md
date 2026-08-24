# 人生母题通行证数据规范

生成或更新人生母题HTML时使用本规范。HTML中的 `life-motif-passport` JSON是后续更新的机器可读基线；可见页面与JSON必须表达同一版本的结论。

## JSON结构

```json
{
  "schema_version": "1.0",
  "project": {
    "name": "人生母题 Life Motif",
    "product_version": "2.0"
  },
  "passport": {
    "id": "lm-YYYYMMDD-local-id",
    "created_at": "YYYY-MM-DD",
    "updated_at": "YYYY-MM-DD",
    "revision": 0,
    "display_version": "V2.0",
    "source_mode": "full_interview | full_migration | summary_migration | lightweight_rebuild",
    "confidence": "high | medium | low",
    "language": "zh-CN"
  },
  "person": {
    "preferred_name": ""
  },
  "source": {
    "coverage": "",
    "limitations": []
  },
  "narrative": {
    "current": "",
    "previous": []
  },
  "sections": [
    {
      "id": "S01",
      "name": "出生",
      "summary": "",
      "evidence": [],
      "confidence": "high | medium | low",
      "updated_at": "YYYY-MM-DD"
    }
  ],
  "timeline": [
    {
      "id": "T01",
      "period": "",
      "title": "",
      "event": "",
      "belief_formed": "",
      "source_section_ids": []
    }
  ],
  "motifs": [
    {
      "id": "M01",
      "title": "",
      "summary": "",
      "status": "pending | recurring | loosening | changed",
      "confidence": "high | medium | low",
      "formed_from": [],
      "evidence_for": [],
      "evidence_against": [],
      "triggers": [],
      "feelings": [],
      "automatic_beliefs": [],
      "old_responses": [],
      "short_term_benefits": [],
      "long_term_costs": [],
      "new_choices": [],
      "observation_questions": [],
      "updated_at": "YYYY-MM-DD"
    }
  ],
  "current_state": {
    "as_of": "YYYY-MM-DD",
    "work": "",
    "relationships": "",
    "health": "",
    "money": "",
    "learning": "",
    "inner_state": ""
  },
  "next_observations": {
    "period": "",
    "core_statement": "",
    "items": []
  },
  "open_questions": [],
  "history": [
    {
      "revision": 1,
      "display_version": "V2.1",
      "date": "YYYY-MM-DD",
      "mode": "single_event | recent_changes | monthly | quarterly | migration",
      "summary": "",
      "changes": [
        {
          "target_type": "narrative | section | timeline | motif | current_state | observation",
          "target_id": "M01",
          "change_type": "added | reinforced | weakened | revised | closed",
          "before": "",
          "after": "",
          "evidence": []
        }
      ],
      "confirmed_by_user": true
    }
  ]
}
```

## 数据规则

- 首次生成使用 `revision: 0`、`display_version: V2.0`、空 `history`；以后每次确认更新，revision加1，显示版本依次为V2.1、V2.2……。
- `sections`保留实际获得的35板块信息；资料不足的板块允许低可信度或空摘要，不得编造。
- 母题编号一旦建立便保持稳定。母题变化时更新状态并写入history，不复用旧编号表达新的母题。
- 新证据追加到原数组；旧证据不删除。发现原判断错误时，将修改前后内容写入history，并更新当前字段。
- `history`只追加，不改写或删除旧记录。每次更新必须记录证据与用户确认状态。
- 不把AI推测写成事实。无法确认的内容进入 `open_questions` 或低可信度字段。
- JSON必须是严格合法的UTF-8 JSON，不写注释，不保留Markdown代码围栏或模板占位符。
- 嵌入HTML前，将字符串中的 `</script>` 转义为 `<\/script>`，并转义U+2028、U+2029，防止提前结束script标签。
- HTML包含完整私人档案。不要把完整HTML当作公开分享文件；公开传播仅导出经过隐私处理的分享卡。

## 一致性检查

生成文件前核对：用户称呼、版本、更新时间、一句话叙事、母题编号与状态、当前状态、未来观察重点，必须在可见HTML和JSON中一致。JSON解析失败、仍含 `{{...}}` 占位符或可见页面版本与JSON不一致时，不得宣称交付完成。
