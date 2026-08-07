# 北交所/IPO项目——董监高访谈笔录Word定稿与核查

## 适用场景

新三板挂牌公司转北交所（或直接IPO）项目中，需要将工作底稿里扫描件PDF格式的董监高访谈笔录，转换为可编辑的Word定稿，完成板块适用性改造，与招股说明书交叉核验，并对接券商修订意见最终定稿。

---

## 一、确认人员范围（第一步必做）

1. 找到工作底稿中的《董监高名单》官方文件，按其确认本次需处理的董事+高管名单
2. 排除：已离任的董监高、已撤销的监事会成员、只有调查表无访谈笔录PDF的人员
3. 注意区分：访谈笔录（问答式）vs 调查表（填空式）——是两种不同文件，勿混淆

---

## 二、扫描件PDF→Word定稿（7步流程）

### 步骤1：OCR提取PDF内容

- PDF通常为扫描件，工具链：pdfplumber转图片(resolution=300) → tesseract(chi_sim+eng)
- ⚠️ 防幻觉红线：OCR有错字，关键信息（企业名/金额/数字）必须逐字对照原文，不轻信子代理的二次归纳

### 步骤2：建立Word模板

- 以项目中律师已手工制作的1份Word为模板（通常独立董事先做好）
- 用python-docx读取段落结构，建立"问题段→回答段"的索引映射
- 模板复制法：复制模板→替换姓名和回答，100%保留格式

### 步骤3：逐人生成Word

- 第1题（基本信息）：严格按PDF原文"详见本人签署的调查表"，不自行填学历/出生年月
- 出生年月如需核验：从调查表首页OCR身份证号，第7-14位精确推算
- 文件命名：序号-项目名访谈提纲-姓名-职务.docx
- 输出格式：.docx（不用.doc）

---

## 三、板块适用性改造（核心工作！）

### 必改项（核准制→注册制）

| 位置 | 原表述（新三板/核准制） | 改为（北交所/注册制） |
|------|------------------------|---------------------|
| 鉴于段 | "公开转让并在全国中小企业股份转让系统挂牌及后续...北交所上市" | "系全国中小企业股份转让系统挂牌公司，现为申请向不特定合格投资者公开发行股票并在北京证券交易所上市" |
| 第七章第1题 | "未经法定机关核准" | "未经法定机关依法注册或核准" |
| 第七章第2题 | "干扰中国证监会及其发行审核委员会审核工作" | "干扰北京证券交易所及中国证监会发行上市审核注册工作" |
| 第七章第2题 | "骗取发行核准" | "骗取发行注册" |
| 第三章第2题 | "全国股转公司或者证券交易所" | "全国股转公司、北京证券交易所或者证券交易所" |
| 全文 | "公开转让说明书" | "招股说明书" |

### 需判断项

- "挂牌公司"：指公司现状→保留；"申请挂牌/挂牌及公开转让"→改
- "全国股转公司"在《监管规则适用指引——发行类第2号》原文中→保留（是法规原文列举）

### 已准确无需改

- 《公司法》条文号：核对是否为2024年新法条文号（第178条，旧法第146条）
- "发行上市""上市公司"：北交所也适用，保留

### 排查方法（可复用）

扫描全文关键词：全国中小企业股份转让系统/新三板/股转/挂牌及公开转让/发行审核委员会/发审委/核准/非上市公众公司/公开转让说明书，逐一判断。

---

## 四、与招股说明书交叉核验（9个核查点）

提取招股说明书全文（通常为可提取文本的PDF），对比访谈笔录：

| 核查点 | 重点 | 常见问题 |
|--------|------|---------|
| 1.海外资产 | 境外子公司清单 | 一般一致 |
| 2.资产抵押/质押 | ⚠️重点！ | 访谈常遗漏质押（应收账款质押、存单质押等） |
| 3.对外担保 | 区分：公司为子公司担保≠对外担保 | 技术合规但建议补充说明 |
| 4.重大合同招投标 | — | 一般一致 |
| 5.行政处罚 | — | 一般一致 |
| 6.未决诉讼仲裁 | 注意"重大"标准（如200万以上） | 小额诉讼可能未达重大标准 |
| 7.同业竞争 | — | 一般一致 |
| 8.关联交易 | 区分：个人关联方 vs 公司层面 | 外部董事答"不涉及"可能准确 |
| 9.增资扩股/重组 | — | 一般一致 |

发现不一致的处理原则：如实披露，"以招股说明书等申报文件披露的内容为准"。

---

## 五、专项事实核查（逐人）

### 担保题

- 核查招股说明书"关联担保"章节，确认哪些董监高为公司提供过担保
- 担保人改为如实披露："本人曾为公司及/或子公司的银行融资提供连带责任保证担保，具体情况以招股说明书披露的关联担保为准"
- 未担保的董监高保持"不存在上述事项"

### 对赌条款

- 确认是否已彻底解除
- 如已解除："截至目前已彻底解除，且约定自始无效"

### 律所名称

- ⚠️ 全文统一（含鉴于段、表格"访谈参加人"栏、落款——容易遗漏表格！）
- 先全文扫描确认无残留旧名称

---

## 六、对接券商修订意见

### 接收券商修订版

1. 对比券商v2版与当前版，找出所有修改
2. ⚠️ 关键陷阱：如果券商发来的是"修订模式"（含w:ins/w:del痕迹），python-docx的p.text返回的是"接受修订后"的文本，删除的文字不显示，会误判为"语义反转"。必须先检查是否含修订标记：

```python
import zipfile, re
with zipfile.ZipFile(fpath) as z:
    xml = z.read('word/document.xml').decode('utf-8')
    has_revisions = bool(re.search(r'<w:ins[\s>]|<w:del[\s>]', xml))
```

### 接受全部修订转清洁版

确认含修订标记后，用以下逻辑一次性接受所有 w:ins/w:del，转为清洁版：

```python
import zipfile, re, shutil
from lxml import etree

NS = {
    'w': 'http://schemas.openxmlformats.org/wordprocessingml/2006/main',
    'w14': 'http://schemas.microsoft.com/office/word/2010/wordml'
}

def accept_revisions_in_xml(xml_bytes):
    """对单个XML部件接受所有修订"""
    root = etree.fromstring(xml_bytes)

    # 1. w:ins / w:moveTo — 保留内部内容，去掉标签（接受插入）
    for tag in ['ins', 'moveTo']:
        for el in root.xpath(f'//w:{tag}', namespaces=NS):
            parent = el.getparent()
            idx = list(parent).index(el)
            for child in el:
                parent.insert(idx, child)
                idx += 1
            parent.remove(el)

    # 2. w:del / w:moveFrom — 整块删除（接受删除）
    for tag in ['del', 'moveFrom']:
        for el in root.xpath(f'//w:{tag}', namespaces=NS):
            el.getparent().remove(el)

    # 3. 格式修订标记 — 去除
    for tag in ['rPrChange', 'pPrChange', 'sectPrChange', 'tblPrChange', 'trPrChange', 'tcPrChange']:
        for el in root.xpath(f'//w:{tag}', namespaces=NS):
            el.getparent().remove(el)

    return etree.tostring(root, xml_declaration=True, encoding='UTF-8', standalone=True)

def process_docx(filepath):
    """处理docx中所有XML部件"""
    tmp_path = filepath + '.tmp'
    with zipfile.ZipFile(filepath, 'r') as zin:
        with zipfile.ZipFile(tmp_path, 'w', zipfile.ZIP_DEFLATED) as zout:
            for item in zin.namelist():
                data = zin.read(item)
                if item.endswith('.xml') and ('document' in item or 'header' in item or 'footer' in item or 'footnotes' in item):
                    data = accept_revisions_in_xml(data)
                zout.writestr(item, data)
    shutil.move(tmp_path, filepath)
```

### 接受修订后的三重验证

```python
# 1. 残留修订标记扫描
def check_clean(filepath):
    with zipfile.ZipFile(filepath) as z:
        for item in z.namelist():
            if item.endswith('.xml'):
                content = z.read(item).decode('utf-8', errors='ignore')
                if 'w:ins ' in content or 'w:del ' in content:
                    return False, f"残留修订标记: {item}"
    return True, "CLEAN"

# 2. XML良构性检查 — etree.fromstring 不报错
# 3. 文本一致性 — python-docx p.text 前后对比（注意：p.text 本身已自动接受修订）
```

---

## 七、陷阱清单（踩坑总结）

1. **python-docx 修订陷阱**：`p.text` 返回"接受修订后"文本，删除内容不可见，会误判"语义反转"。必须先 regex 检测 `w:ins|w:del`
2. **表格单元格易遗漏**：改正文段落后必须扫描表格、页眉、页脚中同一表述（如律所名称常在"访谈参加人"表格栏遗漏）
3. **跨 run 文字替换**：用 `p.text` 判断/拼接全文 → 写入第一个 run → 清空其余 run
4. **OCR 防幻觉**：关键信息（企业名、金额、数字）必须逐字对照原文，不轻信二次归纳
5. **板块改造"需判断项"**：不是所有"新三板/挂牌"都要改——"挂牌公司"指现状应保留，法规原文列举的"全国股转公司"应保留
6. **担保问题逐人区分**：不同董监高的担保范围不同（公司及子公司 vs 仅子公司 vs 不存在），不能一刀切
7. **公司法条文号**：2024 年新公司法条文号与旧法不同（如第178条 vs 旧第146条），需核对
8. **文件命名**：序号-项目名访谈提纲-姓名-职务.docx，统一格式便于排序和归档
