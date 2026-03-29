# Feedback Model

## 建议事件字段

- `event_time`
- `item_id`
- `event_type`
- `source`
- `topic_tags`
- `value_signal`
- `notes`

## 事件类型建议

- `opened_not_finished`
- `finished_not_saved`
- `worth_deep_read`
- `worth_long_term_store`
- `influenced_output`
- `negative_feedback`

## 画像更新规则

- 连续多次出现的主题偏好，才进入长期画像。
- 单次异常行为，只记为观察信号。
- 来源偏好必须结合长期价值结果，而不是只看曝光次数。

## 弱排序建议

- 上调：长期高价值主题、稳定优质来源、被多次沉淀的内容类型。
- 下调：重复低价值格式、长期负反馈类型。
- 保留探索：每轮前排预留少量非偏好但公共重要性高的内容。

