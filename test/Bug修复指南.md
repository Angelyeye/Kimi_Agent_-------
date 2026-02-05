# 《春节模拟器》Bug修复指南

## 快速修复清单

### 1. 修复游戏结束逻辑 (BUG-001)

**文件:** `src/game.js`  
**位置:** `GameState.isGameOver()` 方法 (约第154行)

**问题:** 游戏在第10天早晨才结束，而不是第9天晚上

**修复方案:**

```javascript
// 原代码 (第154-158行)
isGameOver() {
    return this.progress.currentDay > GAME_CONFIG.TOTAL_DAYS ||
           (this.progress.currentDay === GAME_CONFIG.TOTAL_DAYS && 
            this.progress.currentPeriod >= GAME_CONFIG.PERIODS_PER_DAY);
}

// 修复后
isGameOver() {
    return this.progress.currentDay > GAME_CONFIG.TOTAL_DAYS;
}
```

**说明:** 原逻辑在第9天晚上(period=2)时不会触发结束，因为2 < 3。只有当推进到第10天早晨时才会触发。

---

### 2. 修复结局数据字段不匹配 (BUG-002)

**选择方案A - 修改代码 (推荐):**

**文件:** `src/game.js`  
**位置:** `EndingManager.checkEndingConditions()` 方法 (约第1143行)

```javascript
// 原代码 (第1144行)
if (!ending.unlockConditions || ending.unlockConditions.length === 0) {

// 修复后 - 同时支持两种字段名
if ((!ending.unlockConditions && !ending.trigger_conditions) || 
    (ending.unlockConditions && ending.unlockConditions.length === 0)) {
    return true;
}

// 同时修改第1149行
for (const conditionGroup of (ending.unlockConditions || ending.trigger_conditions || [])) {
```

**选择方案B - 修改数据文件:**

**文件:** `data/endings.json`

将所有 `trigger_conditions` 改为 `unlockConditions`

---

### 3. 添加事件数据加载 (WARN-001)

**文件:** `src/game.js`  
**位置:** `Game.loadGameData()` 方法 (约第1448行)

**修复方案:**

```javascript
async loadGameData() {
    try {
        // 加载角色数据
        const charResponse = await fetch('data/characters.json');
        if (charResponse.ok) {
            const charData = await charResponse.json();
            this.characters = charData.characters || [];
        }
    } catch (e) {
        console.warn('加载角色数据失败，使用默认数据:', e);
        this.loadDefaultCharacters();
    }

    // 加载事件数据 (新增)
    try {
        const eventResponse = await fetch('data/common_events.json');
        if (eventResponse.ok) {
            const eventData = await eventResponse.json();
            this.eventData = eventData.events || [];
        } else {
            this.loadDefaultEvents();
        }
    } catch (e) {
        console.warn('加载事件数据失败，使用默认数据:', e);
        this.loadDefaultEvents();
    }

    // 加载角色专属事件 (新增)
    try {
        const charEventResponse = await fetch('data/character_events.json');
        if (charEventResponse.ok) {
            const charEventData = await charEventResponse.json();
            // 合并通用事件和角色专属事件
            this.eventData = this.eventData.concat(charEventData.events || []);
        }
    } catch (e) {
        console.warn('加载角色专属事件失败:', e);
    }

    // 加载结局数据 (新增)
    try {
        const endingResponse = await fetch('data/endings.json');
        if (endingResponse.ok) {
            const endingData = await endingResponse.json();
            this.endingData = endingData.endings || [];
        } else {
            this.loadDefaultEndings();
        }
    } catch (e) {
        console.warn('加载结局数据失败，使用默认数据:', e);
        this.loadDefaultEndings();
    }

    // 设置到管理器
    this.events.loadEvents(this.eventData);
    this.endings.loadEndings(this.endingData);
}
```

---

### 4. 处理未定义属性 (BUG-003)

**方案A - 添加属性支持 (推荐):**

**文件:** `src/game.js`  
**位置:** 在 `ATTRIBUTE_BOUNDS` 后添加 (约第38行后)

```javascript
const ATTRIBUTE_BOUNDS = {
    deposit: { min: -50000, max: 10000000, default: 0 },
    weight: { min: 30, max: 200, default: 65 },
    face: { min: -100, max: 100, default: 50 },
    mood: { min: 0, max: 100, default: 50 },
    health: { min: 0, max: 100, default: 50 },
    luck: { min: 0, max: 100, default: 50 },
    // 新增属性
    elder_favor: { min: -100, max: 100, default: 0 },
    uncle_favor: { min: -100, max: 100, default: 0 },
    aunt_favor: { min: -100, max: 100, default: 0 },
    relative_favor: { min: -100, max: 100, default: 0 },
    eq: { min: 0, max: 100, default: 50 },
    prestige: { min: -100, max: 100, default: 0 },
    reputation: { min: -100, max: 100, default: 0 }
};

const ATTRIBUTE_NAMES = {
    deposit: '存款',
    weight: '体重',
    face: '面子',
    mood: '心情',
    health: '健康',
    luck: '运气',
    // 新增属性名
    elder_favor: '长辈好感',
    uncle_favor: '舅舅好感',
    aunt_favor: '阿姨好感',
    relative_favor: '亲戚好感',
    eq: '情商',
    prestige: '声望',
    reputation: '名誉'
};
```

**方案B - 过滤无效属性:**

**文件:** `src/game.js`  
**位置:** `AttributeManager.applyEffects()` 方法 (约第374行)

```javascript
applyEffects(effects) {
    if (!Array.isArray(effects)) return;

    const results = [];
    for (const effect of effects) {
        if (effect.type === 'attribute' || effect.attribute) {
            const attr = effect.attribute;

            // 跳过未定义的属性
            if (!ATTRIBUTE_BOUNDS[attr]) {
                console.warn(`未知属性: ${attr}`);
                continue;
            }

            // ... 原有代码
        }
    }
    return results;
}
```

---

### 5. 添加角色头像 (BUG-004)

**方案A - 创建头像目录:**

```bash
mkdir -p /mnt/okcomputer/output/data/avatars/
```

然后为每个角色创建头像图片，或使用emoji图片。

**方案B - 修改角色数据使用emoji:**

**文件:** `data/characters.json`

将所有 `"avatar": "avatars/xxx.png"` 改为 `"avatar": "👤"` (对应角色的emoji)

---

## 测试验证

修复后，请进行以下测试：

1. **游戏结束测试:** 玩到第9天晚上，确认结束后正确显示结局
2. **结局触发测试:** 验证不同属性组合能触发不同结局
3. **事件加载测试:** 确认数据文件中的事件能被正确加载和触发
4. **属性变化测试:** 验证所有属性变化都正确生效

---

*修复指南版本: 1.0*
