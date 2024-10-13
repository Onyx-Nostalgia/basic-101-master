![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&height=300&section=header&text=%3EBasic-101&fontSize=90&animation=fadeIn&fontAlignY=38&desc=but%20advance%20and%20best%20practices&descAlignY=51&descAlign=60)

แหล่งรวบรวมความรู้พื้นฐานและ Best Practices  

<details>
<summary>Table of Contents</summary>

<!--ts-->
- [📝 Conventional Commits](#-conventional-commits)
  - [🌈  Why Use Conventional Commits](#--why-use-conventional-commits)
  - [🧰 type (require)](#-type-require)
  - [🖍️ description (require)](#️-description-require)
  - [📄 body (optional)](#-body-optional)
  - [🩴 footer (optional)](#-footer-optional)
    - [Examples](#examples)
  - [💥BREAKING CHANGE](#breaking-change)
    - [commit message ที่มีการระบุรายละเอียด และลงท้ายด้วย BREAKING CHANGE](#commit-message-ที่มีการระบุรายละเอียด-และลงท้ายด้วย-breaking-change)
    - [commit message ที่มี ! เพื่อบ่งบอก breaking change](#commit-message-ที่มี--เพื่อบ่งบอก-breaking-change)
    - [commit message ที่มีทั้ง ! และ BREAKING CHANGE](#commit-message-ที่มีทั้ง--และ-breaking-change)
  - [🎭 Examples](#-examples)
    - [หลัง `:` (colons) หรือ emoji ให้เว้นวรรค 1 ครั้ง ก่อนพิมพ์ต่อ](#หลัง--colons-หรือ-emoji-ให้เว้นวรรค-1-ครั้ง-ก่อนพิมพ์ต่อ)
    - [commit message ที่มีเนื้อหา body หลายย่อหน้า และมีข้อความ footer หลายข้อความ](#commit-message-ที่มีเนื้อหา-body-หลายย่อหน้า-และมีข้อความ-footer-หลายข้อความ)
    - [commit message เมื่อเกิดการ revert commit](#commit-message-เมื่อเกิดการ-revert-commit)
  - [🍭 Bonus](#-bonus)
  - [❓ FAQ](#-faq)
    - [ควรทำอย่างไรหากการ commit ในครั้งนั้น สอดคล้องกับหลาย type commit ?](#ควรทำอย่างไรหากการ-commit-ในครั้งนั้น-สอดคล้องกับหลาย-type-commit-)
    - [นี่มันจะไม่ทำให้การ development และ workflow ช้าลงกว่าเดิมหรือ ?](#นี่มันจะไม่ทำให้การ-development-และ-workflow-ช้าลงกว่าเดิมหรือ-)
    - [นี่เกี่ยวข้องกับ SemVer อย่างไร?](#นี่เกี่ยวข้องกับ-semver-อย่างไร)
    - [ทำอย่างไรถ้าใส่ชนิดของ commit ผิดโดยไม่ได้ตั้งใจ ?](#ทำอย่างไรถ้าใส่ชนิดของ-commit-ผิดโดยไม่ได้ตั้งใจ-)
      - [เมื่อคุณใช้ชนิดที่เป็นส่วนหนึ่งในข้อตกลง แต่ผิดชนิด เช่น ใช้ `fix` แทนที่จะเป็น `feat`](#เมื่อคุณใช้ชนิดที่เป็นส่วนหนึ่งในข้อตกลง-แต่ผิดชนิด-เช่น-ใช้-fix-แทนที่จะเป็น-feat)
      - [เมื่อคุณใช้ชนิดที่ ไม่ได้ เป็นส่วนหนึ่งในข้อตกลง เช่น ใช้ `feet` แทนที่จะเป็น `feat`](#เมื่อคุณใช้ชนิดที่-ไม่ได้-เป็นส่วนหนึ่งในข้อตกลง-เช่น-ใช้-feet-แทนที่จะเป็น-feat)
  - [🧷 Ref;](#-ref)
<!--te-->

</details>

# 📝 Conventional Commits
> A specification for adding human and machine readable meaning to commit messages

ข้อตกลงอย่างง่ายในการเขียน Commit message อ้างอิงจาก [conventional commits v1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) 

## 🌈  Why Use Conventional Commits
- ช่วยให้สามารถเขียน automated tools on top ได้ง่ายขึ้น
    - ช่วยในการทำ CHANGELOG แบบอัตโนมัติ
    - ช่วยในการจับความหมายของ version อัตโนมัติ ตามประเภทของ commit
    - การมี Trigger เพื่อสั่งให้ Build / Publish ฟีเจอร์ต่าง ๆ ได้ด้วยตัวระบบเอง
    - etc.
- ช่วยในการสื่อสารบ่งบอกสิ่งที่เปลี่ยนแปลงไป ให้กับเพื่อนร่วมทีม หรือ คนอื่น ๆ 
- เป็นเหมือนกฎง่าย ๆ ทำให้มี commit history ที่ชัดเจน
    - ช่วยให้ผู้คนมีส่วนร่วมใน Project ของคุณได้ง่ายขึ้น โดยเฉพาะอย่างยิ่งกับ Project ที่มี commit history จำนวนมาก

เนื่องจาก [conventional commits v1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) สนับสนุนเรื่องความยืดหยุ่น เพื่อให้สามารถนำข้อตกลงหรือ structure ไปปรับใช้ได้ตามสะดวก ซึ่งในแต่ละที่เราก็อาจจะพบ structure ที่แตกต่างกันไปบ้าง ตามแต่ข้อตกลงกันในแต่ละที่

structure ที่เราจะใช้กันที่นี่ คือแบบนี้ ซึ่งจะแตกต่างจาก [conventional commits v1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) นิดหน่อย
```
<type-with-emoji>: [optional JIRA-ID]: <description>

[optional body]

[optional footer(s)]
```

## 🧰 type (require)
- **🌟 feat: เมื่อเพิ่มคุณสมบัติใหม่ (feature)**
- **🐛 fix: เมื่อแก้ไขข้อผิดพลาด (bug fix)**
- 🔧 chore: เมื่อมีการเปลี่ยนแปลงค่า Ignore หรือค่า Settings ที่ไม่กระทบกับ Code โดยตรง (เช่นที่: .gitignore หรือ .prettierrc)
- ♻️ refactor: การทำความสะอาดโค้ดให้อ่านง่าย เข้าใจมากยิ่งขึ้น (เช่น การเปลี่ยนชื่อตัวแปร/ ชื่อฟังก์ชัน) ปรับปรุงโครงสร้างภายใน โดยที่ไม่เกี่ยวข้องกับการเพิ่ม feature ใหม่ หรือแก้ bug
- 📝 docs: เมื่อเปลี่ยนแปลงที่เกี่ยวข้องกับเอกสาร เช่น README หรือ markdown file อื่น ๆ
- 💄 style: เมื่อเกี่ยวข้องกับ styling เช่น code formatting, การลืมใส่ semi-colins
- ✅ test: เมื่อเกี่ยวข้องกับการเขียน Testing เพิ่ม หรือ Refactoring tests โดยที่ไม่เกี่ยวข้องกับ Production code
- ⚡️ perf: เมื่อทำการเพิ่มประสิทธิภาพ (performance)
- 💚 ci: ปรับปรุง เปลี่ยนแปลง CI Config ของไฟล์ หรือ สคริปต์ เช่น Travis, Circle, BrowserStack
- 👷 build: เมื่อเกี่ยวข้องกับการ build ระบบ เช่น ปรับปรุง build config หรือ dependency ภายนอก เช่น npm, gulp, broccoli, etc.
- ⏪️ revert: revert commit 

ในกรณีต้องการนิยาม type ใหม่ขึ้นมาเอง ก็สามารถทำได้ เพราะ Conventional Commits สนับสนุนเรื่องความยืดหยุ่น เพื่อเป็นประโยชน์ต่อการอ่านและแบ่งประเภท commit รูปแบบใหม่ ๆ หรือ สร้าง type ใหม่มาเพื่อช่วยในการทำ automate tool ก็ย่อมทำได้เช่นกัน 
> ควรนิยามและตั้งวิธีใช้ที่ชัดเจนเพื่อให้คนในทีมเข้าใจตรงกันด้วยนะ

- type ใช้ UPPERCASE หรือ lowercase ก็ได้ ตามแต่ละที่ตกลงกัน แต่ควรใช้ให้เหมือน ๆ กันหมด
    - ทางนี้จะใช้ lowercase (🌟 feat: ...) เนื่องจากพิมพ์ง่ายสุด ๆ และเห็นจากที่อื่น ๆ นิยมใช้ lowercase มากสุด 

## 🖍️ description (require)
- เป็นเหมือน **สรุปสั้น ๆ** เกี่ยวกับการเปลี่ยนแปลงที่เกิดขึ้น 
- Description จะต้องอยู่ต่อจากเครื่องหมาย `:` ที่อยู่หลังจาก type และเว้นวรรค 1 ครั้ง
- Description นั้นมักจะเขียนในรูปแบบของ Imperative Mood หรือ การเขียนในรูปแบบประโยคคำสั่ง / ร้องขอ เช่น "fix bug …" หรือ "add function …"
- เป็นส่วนที่ควรระบุ และควรเขียนเป็นภาษาอังกฤษ โดยใช้ Present tense (e.g. ใช้อย่าใช้ "added" หรือ "adds" ให้ใช้ "add" แทน)
- ไม่จำเป็นต้องใช้ `.`(dot) เมื่อจบประโยค
- ไม่จำเป็นต้องใช้ตัวอักษรพิมพ์ใหญ่สำหรับขึ้นต้นประโยค

เพิ่มความเข้าใจได้อย่างรวดเร็ว ใน description ด้วย emoji ที่สื่อถึงความหมายจาก https://gitmoji.dev/  

ตัวอย่างที่คิดว่า น่าจะใช้บ่อย ๆ
```
🌟 feat: ETLP-123: 👔 add read_profile business logic
👷 build: ETLP-123: 🧱 infrastructure related changes
✅ test: ETLP-123: 🧪 add a failing test
🔧 chore: 🙈 add or update a .gitignore file
🌟 feat: ETLP-123: 🗃️ perform database related changes
♻️ refactor: ETLP-123:🚚 move or rename resources (e.g.: files, paths, routes)
🐛 fix: HEIM-1234:🚑️ critical hotfix
```

## 📄 body (optional)
ลงรายละเอียดของการเปลี่ยนแปลง เช่น เราแก้ไข Bug ตัวนี้ได้ยังไง, ปัญหาที่เราพบ, ขั้นตอนการทำงานของอะไรบางอย่าง 
- commit ใส่ได้ตามอิสระ และอาจจะมีหลายย่อหน้าก็ได้
- body จะต้องเริ่มด้วยการเว้นบรรทัดว่างหนึ่งบรรทัดหลังจาก description ในบรรทัดแรก

## 🩴 footer (optional)
จะกล่าวถึงผลที่เกิดจากการเปลี่ยนแปลง เช่น การประกาศการเปลี่ยนแปลงที่จะเกิดขึ้น (breaking) การเชื่อมโยง issues ที่ปิด การกล่าวถึง contributors และอื่น ๆ
- จะต้องเริ่มด้วยการเว้นบรรทัดว่างหนึ่งบรรทัดหลังจาก boddy หรือ description
- สามารถมีมากกว่า 1 footer ได้
- footer ประกอบด้วย `<word-token>: <value>` (e.g. `Reviewed-by: username`) หรือ `<word-token> #<value>` (e.g. `Closes #123`)
  > ที่นี่เราไม่ได้ใช้ issue ของ git เลย (หน้าตา git issue e.g. `#123`) จะใช้จาก jira issue-id (e.g. `ETLP-12`) ซะมากกว่า จึงจะไม่ได้เห็นการใช้ `<word-token> #<value>` ของที่นี่
- word-token ของ footer จะต้องใช้ `-` แทนการเว้นววรรค เช่น `Acked-by` เพื่อให้ง่ายต่อการแยกแยะข้อความว่าเป็น body หรือ footer
  - ยกเว้น `BREAKING CHANGE` ที่สามารถนำมาใช้เป็น word-token ได้เลย
### Examples
```
Reviewed-by: Z
Refs: #123
Closes: ETLP-222, ETLP-222, ETLP-222
BREAKING CHANGE: drop code unsupport for python 3
```

## 💥BREAKING CHANGE
commit ที่มี footer `BREAKING CHANGE:` หรือ type ที่มี `!` ต่อท้าย หมายถึง มีการเพิ่มการเปลี่ยนแปลงที่กระทบกับระบบเดิมอย่างมาก (การเปลี่ยนแปลงระดับ `MAJOR`)
- footer ของ `BREAKING CHANGE` ต้องพิมพ์ในลักษณะ  `BREAKING CHANGE: <value>`
- BREAKING CHANGE ต้องพิมพ์ใหญ่ทั้งหมด (UPPERCASE)
- สามารถระบุได้กับทุก type
- ทุก Commit ที่มี Breaking change จะทริกเกอร์เมื่อมีการทำ MAJOR release และจะแสดงบน Changelogs ตามแต่ละ Commit type

### commit message ที่มีการระบุรายละเอียด และลงท้ายด้วย BREAKING CHANGE
```
🌟 feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### commit message ที่มี ! เพื่อบ่งบอก breaking change
`🌟 feat!: send an email to the customer when a product is shipped`

### commit message ที่มีทั้ง ! และ BREAKING CHANGE
```
🔧 chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

## 🎭 Examples
### หลัง `:` (colons) หรือ emoji ให้เว้นวรรค 1 ครั้ง ก่อนพิมพ์ต่อ
- ❌ `🌟feat:ETLP-123:add some method`
- 👍 `🌟 feat: ETLP-123: add some method`

### commit message ที่มีเนื้อหา body หลายย่อหน้า และมีข้อความ footer หลายข้อความ
> ต้องมีบรรทัดว่าง คั่นระหว่าง description, body, footer 

```
🐛 fix: ETLP-432: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Reviewed-by: Z

Refs: #123
```
### commit message เมื่อเกิดการ revert commit
```
⏪️ revert: let us never again speak of the noodle incident

Refs: 676104e, a215868, COMMIT-ID
```
## 🍭 Bonus

ใครที่ใช้ vscode สามารถใช้ Extension เสริม เช่น [vscode-git-commit](https://marketplace.visualstudio.com/items?itemName=rioukkevin.vscode-git-commit) เรามี Config มาให้นำไปใช้กันเพียงนำไปเพิ่มใน settings (`Wins + Shift + p` search `User settings (JSON)`)

<script src="https://gist.github.com/Onyx-Nostalgia/418cee0fa5d7996c45705841d15922c7.js"></script>

**Preview**

![vscode-git-commit](https://github.com/user-attachments/assets/250d5341-f16a-49d6-8a5c-88bd4e4003c8)


## ❓ FAQ

### ควรทำอย่างไรหากการ commit ในครั้งนั้น สอดคล้องกับหลาย type commit ?
> Go back and make multiple commits whenever possible

กลับไปแก้ไขและพยายามแบ่งออกให้เป็นหลาย commit เท่าที่จะเป็นไปได้ ประโยชน์ส่วนหนึ่งของ Conventional Commits คือการที่มันช่วยให้เราสามารถจัดการกับ commit และ PR (pull request) หรือ MR (merge request) ได้ดีกว่าเดิม

### นี่มันจะไม่ทำให้การ development และ workflow ช้าลงกว่าเดิมหรือ ?
มันทำให้การทำงานแบบไม่มีการจัดการช้าลง แต่มันจะช่วยให้คุณทำงานได้เร็วขึ้นในระยะยาวกับหลาย ๆ project ที่มีส่วนร่วมจากหลาย ๆ คน

### นี่เกี่ยวข้องกับ SemVer อย่างไร?
commit ที่มีชนิดเป็น fix จะถูกมองเป็น `PATCH` ใน release ส่วน commit ชนิดที่เป็น feat จะถูกมองเป็น `MINOR` release และ commits ที่เป็น `BREAKING CHANGE` ไม่ว่าจะเป็นชนิดใดก็ตาม จะถูกมองเป็น `MAJOR` release

### ทำอย่างไรถ้าใส่ชนิดของ commit ผิดโดยไม่ได้ตั้งใจ ?
#### เมื่อคุณใช้ชนิดที่เป็นส่วนหนึ่งในข้อตกลง แต่ผิดชนิด เช่น ใช้ `fix` แทนที่จะเป็น `feat`
ก่อนที่จะ merge หรือ release ความผิดพลาดนั้น แนะนำให้ใช้ `git rebase -i` เพื่อแก้ไขข้อความใน commit ย้อนหลัง แต่ถ้าทำหลังจากที่ release ไปแล้ว การแก้ไขจะแตกต่างกันไปขึ้นอยู่กับ tool และวิธีการที่คุณใช้

#### เมื่อคุณใช้ชนิดที่ ไม่ได้ เป็นส่วนหนึ่งในข้อตกลง เช่น ใช้ `feet` แทนที่จะเป็น `feat`
ในสถานการณ์ที่แย่ที่สุด มันไม่ใช่วันสิ้นโลกถ้าคุณจะใส่ commit ที่ไม่สอดคล้องกับข้อกำหนดของ Conventional Commits มันมีความหมายง่าย ๆ คือ commit นั้นจะถูกมองข้ามไปถ้าใช้ tool ที่อ้างอิงตามข้อกำหนดนี้เท่านั้นเอง

## 🧷 Ref;
- https://www.conventionalcommits.org/en/v1.0.0/
- https://www.borntodev.com/2023/01/30/conventional-commits/
- https://blog.2my.xyz/2021/10/30/git-conventional-commits/
- https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/
- https://gitmoji.dev/



![footer](https://capsule-render.vercel.app/api?type=waving&color=auto&section=footer)
