# 定制化修改

## 1. manage_blueprint工具blueprintType参数描述错误，导致AI误用
问题描述：AI创建蓝图时使用blueprintType参数传入父类路径，而非正确的parentClass参数，导致蓝图无法正确继承父类。

解决方案：修改`src/tools/consolidated-tool-definitions.ts`第200行，将blueprintType描述改为"Blueprint type (e.g., Actor, Character, Pawn)."，使其与parentClass区分。

时间：2026-04-17 15:50

---

## 2. set_scs_property的property_value参数被错误序列化，导致数组属性设置失败
问题描述：设置ComponentTags等数组属性时报错"Expected array for array property"，原因是JSON.stringify将数组包装成字符串传递。

解决方案：修改`src/tools/handlers/blueprint-handlers.ts`第371行，移除JSON.stringify包装，直接传递值以保留JSON数组/对象类型。

时间：2026-04-17 17:46

---

## 3. set_scs_property只读取propertyValue参数，不接受工具描述中的value参数
问题描述：AI按工具描述传入value参数，但代码只读取propertyValue，导致报错"Property value is invalid"。

解决方案：修改`src/tools/handlers/blueprint-handlers.ts`set_scs_property分支，同时支持value和propertyValue参数名（与set_default行为一致）。

时间：2026-04-17 17:46