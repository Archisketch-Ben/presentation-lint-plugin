---
theme: apple-basic
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides, markdown enabled
title: eslint-plugin-archisketch
info: |
  ## Introduce eslint-plugin-archisketch
  Presentation slides for developers.
# apply any unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
layout: fact
---

# 100%

ESLint plugin for Archisketch Dev Team

<span class="text-sm">아키스케치 내부에서 암묵적으로 사용되는 규칙을 ESLint 플러그인을 통해 정의하고 여러 프로젝트에서 표준화된 규칙을 적용</span>

<div class="absolute bottom-10 left-10">
  <span class="font-700">
    Ben
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: two-cols
layoutClass: gap-16
---

# 목차

<p class="pt-4">패키지의 구조와 규칙을 작성하고 관리하는 방법에 대해 단계별로 설명하는 자료입니다:</p>

::right::

<Toc v-click minDepth="1" maxDepth="2" class="transition-all text-[70%] max-h-[500px] overflow-y-auto"></Toc>

---
transition: slide-up
level: 2
---

# ESLint 플러그인과 규칙이란 무엇인가요?

<br />

ESLint 플러그인은 규칙을 정의해 ESLint를 확장합니다. 대부분의 경우 여러 프로젝트에서 공유하려는 추가 규칙을 캡슐화하는 플러그인을 생성하여 ESLint를 확장합니다.

<br />

<blockquote class="max-w-lg">
<strong>💡 ESLint?</strong>
<p>ESLint는 코드를 일관성 있게 만들고 버그를 방지하는 것을 목표로 JS 코드에서 발견되는 패턴을 식별하고 보고하는 도구입니다.</p>
</blockquote>

<img
  v-click
  class="absolute bottom-20 -left-4 w-80 opacity-50"
  src="https://sli.dev/assets/arrow-bottom-left.svg"
  alt=""
/>
<p v-after class="absolute bottom-50 left-45 opacity-30 transform -rotate-10">이게 왜 필요한 거죠?🦭</p>

---
transition: slide-up
---

# 이게 왜 필요한가요?

<div class="two-columns w-full h-full grid grid-rows-2 gap-x-10">
  <div id="top" class="grid grid-cols-2 gap-2">
    <div v-click>
      <div class="col-top-left">
        <h2>
          <ph-trend-up-light />
          프로젝트 확장
        </h2>
        <br />
        <ul>
          <li>
            부족한 리소스, 다양한 요구사항에 의해 어쩔 수 없이 복잡해지는 모듈
            종속성
          </li>
        </ul>
      </div>
    </div>
    <div v-click>
      <div class="col-top-right">
        <h2>
          <svg
            class="slidev-icon"
            xmlns="http://www.w3.org/2000/svg"
            width="28"
            height="28"
            viewBox="0 0 24 24"
          >
            <path
              fill="currentColor"
              d="M14.4 20L13 18.6l2.6-2.6l-2.6-2.6l1.4-1.4l2.6 2.6l2.6-2.6l1.4 1.4l-2.6 2.6l2.6 2.6l-1.4 1.4l-2.6-2.6zm1.975-9l-3.55-3.55l1.4-1.4l2.125 2.125l4.25-4.25L22 5.35zM2 17v-2h9v2zm0-8V7h9v2z"
            />
          </svg>
          코딩 컨벤션
        </h2>
        <br />
        <ul>
          <li>개발자마다 다른 코딩 스타일 및 네이밍</li>
          <li>
            개발자마다 다른 선호하는 기술<small class="block"
              >(Tanstack-query & SWR, Moment & Dayjs) =>
              <del>최근 마이그레이션 작업을 끝내 꽤 안정적입니다.</del></small
            >
          </li>
        </ul>
      </div>
    </div>
  </div>
  <div id="bottom" class="grid grid-cols-2 mt-5">
    <div v-click>
      <div class="col-bottom-left">
        <h2>
          <svg
            class="slidev-icon"
            xmlns="http://www.w3.org/2000/svg"
            width="28"
            height="28"
            viewBox="0 0 12 12"
          >
            <path
              fill="currentColor"
              d="M5 2.5a1.5 1.5 0 1 1-3 0a1.5 1.5 0 0 1 3 0M6 7a1.5 1.5 0 1 0 0-3a1.5 1.5 0 0 0 0 3M3.55 5H2a1 1 0 0 0-1 1v.207c0 .596.343 1.086.797 1.407c.272.193.597.336.952.42c.269-.488.736-.85 1.292-.981A2.49 2.49 0 0 1 3.55 5m4.41 2.053a2 2 0 0 1 1.291.98c.355-.083.68-.226.952-.419c.454-.32.797-.811.797-1.407V6a1 1 0 0 0-1-1H8.45a2.51 2.51 0 0 1-.49 2.053M4.5 8a1 1 0 0 0-1 1v.167c0 .587.357 1.058.808 1.358C4.763 10.83 5.363 11 6 11s1.237-.171 1.692-.475c.45-.3.808-.771.808-1.358V9a1 1 0 0 0-1-1zM9 4a1.5 1.5 0 1 0 0-3a1.5 1.5 0 0 0 0 3"
            />
          </svg>
          커져가는 조직
        </h2>
        <br />
        <ul>
          <li>
            커뮤니티에서 만들어진 규칙만으로 부합하지 않는 조직 내 요구사항들
          </li>
        </ul>
      </div>
    </div>
  </div>
</div>

<style>
h1 {
  background: #a8c0ff;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #3f2b96, #a8c0ff);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #3f2b96, #a8c0ff); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: fade-out
layout: two-cols
layoutClass: gap-8
level: 2
---

## 어떻게 위 문제를 해결하나요?

운영 부채를 해결하기 위해 다양한 규칙을 회의를 통해 결정했다고 가정해보겠습니다.

<div v-click>

**❝비동기 데이터 관리는 swr이 아닌 Tanstack-query로 통일합시다❞**

</div>

<div v-click>

**❝이전 사명인 '아키드로우'는 사용하지 않도록 하며, 기능을 담당하는 로직은 특정 폴더에 넣는다 등 정보들은 보통 리드미 또는 노션에 작성됩니다.❞**

</div>

<div v-click>

그럼 이렇게 정한 규칙들은 대부분 노션이나 리드미를 통해 작성되고 관리됩니다.

</div>


<div v-click>

```md twoslash
### Tech Spec
비동기 데이터 관리는 Tanstack-query를 사용합니다.

### Structure
음식 주문을 담당하는 모듈은 `features/order` 폴더에 작성하면 됩니다.

### Business
이전 사명을 값으로 사용해선 안 됩니다. ex) '아키드로우', 'archidraw'

그 외 요구사항들...
```

</div>

::right::

<div v-click>

리드미 파일에 주의사항을 기재하거나 직접 대화를 통해 전달하는 방법은 새로운 개발자가 쉽게 <span v-mark.red="6">놓칠 수 있고, 지속적인 관리가 어렵다</span>는 단점이 있습니다.

이러한 변화들을 프로젝트에 새로 합류하는 개발자들에게 전달하는 더 좋은 방법은 없을까요?

</div>

---
layout: statement
---

<p class="text-xl">규칙을 모두 몰라도 코드 작성 단계에서 규칙을 잘 아는 누군가가 옆에서 가이드하는 건 어떨까요?</p>

---
transition: fade-out
---

이 패키지가 이를 도와주는 가이드 역할을 합니다.

먼저, 왜 간단한 정규식을 놔두고 ESLint 플러그인을 구현했는지 궁금할 수도 있습니다. `Editor` 프로젝트를 개발하던 때에, 코드 리뷰에서 디버깅 코드 포함 여부같은 사소한 리뷰를 방지하고자 로그가 함부로 찍히지 않도록 `console.log` 사용을 제한하는 규칙을 만들었습니다:

```shell
  no_console () {
    consoleRegexp='^[^-].*console.log'
    filenameRegexp='^[^-].*console.log(\|^+++'

    if test "$(git diff --cached | grep -c "$consoleRegexp")" != 0
    then
      git diff --cached | grep -ne "$filenameRegexp" | grep -B1 "$consoleRegexp"
      printf "\nSome files include ${red}console.log${no_color}.\n"
      confirm
    fi
  }
  check_branch
  no_console
```

<div v-click>

하지만 이러한 방법은 대부분 의도한만큼 **정확하게 동작하지 않습니다.** 예를 들어서,문자열 또는 주석 내부에 있는 `console.log`를 구분하지 못할 수도 있습니다. 더 정교한 정규식을 구현해 대응할 수 있지만 복잡해지니, AST를 사용하는 게 더 좋습니다.

</div>

---
transition: slide-left
layout: two-cols
layoutClass: gap-8
---

## RegExp

```js {0|1-2|4-5|7-8|all} twoslash
// trigger error!
console.log("디버깅해볼게요")

// trigger error!
const alertMessage = "console.log()는 개발 환경에서만 사용해주세요"

// trigger error!
// console.log("디버깅해볼게요")
```

<div v-after>

<h6 class="opacity-40 pt-4">PROS</h6>

- 구현이 간단합니다

<h6 class="opacity-40">PROS</h6>

- 복잡한 요구사항에 적합하지 않습니다
- 복잡해진 정규식은 유지보수가 쉽지 않습니다

</div>

::right::

## AST

```js {0|1-2|4|6|all} twoslash
// trigger error!
console.log("디버깅해볼게요")

const alertMessage = "console.log()는 개발 환경에서만 사용해주세요"

// console.log("디버깅해볼게요")
```

<div v-after>

<h6 class="opacity-40 pt-4">PROS</h6>

- 관리가 용이합니다.
- 복잡한 비즈니스 요구사항에 대해 구현이 가능합니다

<h6 class="opacity-40">PROS</h6>

- 유지보수를 위해선 AST에 대한 지식이 필요합니다 => 프로젝트의 "CONTRIBUTING.md"에서 이를 위한 리소스를 제공합니다.

</div>

<div v-click>

암묵적으로 생성된 규칙들을 잘 관리하고자 ESLint-Plugin을 만들게 되었습니다.

</div>

---
layout: statement
transition: slide-up
---

# 코드 자세히 살펴보기

---
transition: fade-out
---

## 폴더 구조

`docs/rules`에 <span v-mark.red="1">규칙에 대한 문서</span>가 작성됩니다.

`lib/rules/`에 <span v-mark.orange="2">규칙을 정의</span> 하는 스크립트가 정의되어 있습니다. `configs` 폴더에는 이 플러그인을 사용할 때 규칙에 대한 추천 구성을 설정할 수 있습니다.

`tests/lib/rules`에 <span v-mark.green="3">규칙에 대한 테스트 케이스</span>가 정의되어 있습니다.

```md {all|1-3|4-10|11-14}
├── docs
│  └── rules
│    └── no-archidraw.md
├── lib
│  ├── configs
│  │  └── recommended.js
│  ├── docsUrl.js
│  ├── index.js
│  └── rules
│    └── no-archidraw.js
└── tests
  ├── lib
  │  └── rules
  │    └── no-archidraw.test.js
```

---
transition: fade-out
---

## 프로젝트 초기화

<br />

사내 프로젝트와 마찬가지로 패키지 매니저는 `npm`을 사용합니다.

<v-clicks>

- `npm install`을 실행해 종속성을 설치합니다.
- `npm run build`를 실행해 플러그인의 진입점이 되는 파일<small>(build/index.js)</small>을 생성합니다.
- 작업을 시작합니다.

</v-clicks>

---
transition: fade-out
---

## 작업을 위한 CLI 제공

<br />

편의를 위해 작업에 필요한 파일을 자동으로 생성하는 CLI를 제공합니다.

또한 문서를 업데이트하는 CLI도 제공합니다.

---
transition: fade-out
---

### 파일 생성

새로운 규칙을 추가하려면 다음 명령어를 실행하세요:

```bash
npm run generate-rule
```

---
transition: fade-out
---

### 파일 생성

`no-archidraw` 규칙을 구현하는 것을 예시로 들어보겠습니다.

명령어를 실행하고 질문에 대한 답을 입력해주세요:

````md magic-move
```bash
✔ 규칙을 만드는 작성자의 이름을 입력해주세요: ben
```

```bash {2-7}
✔ 규칙을 만드는 작성자의 이름을 입력해주세요: ben
✔ 새 규칙의 이름을 입력해주세요! 다음 ESLint 규칙 네이밍 컨벤션을 따라야 합니다:

- 규칙에서 무언가를 허용하지 않는 경우에는 no- 접두사를 붙이세요(예: eval()을 허용하지 않으려면 no-eval, 디버거를 허용하지 않으려면 no-debugger).
- 규칙에서 특정 항목의 포함을 강제하는 경우에는 특별한 접두사 없이 짧은 이름을 사용하세요.
- 단어 사이에는 대시(-)를 사용하세요.
새 규칙의 이름은 무엇인가요? … no-archidraw
```

```bash {8}
✔ 규칙을 만드는 작성자의 이름을 입력해주세요: ben
✔ 새 규칙의 이름을 입력해주세요! 다음 ESLint 규칙 네이밍 컨벤션을 따라야 합니다:

- 규칙에서 무언가를 허용하지 않는 경우에는 no- 접두사를 붙이세요(예: eval()을 허용하지 않으려면 no-eval, 디버거를 허용하지 않으려면 no-debugger).
- 규칙에서 특정 항목의 포함을 강제하는 경우에는 특별한 접두사 없이 짧은 이름을 사용하세요.
- 단어 사이에는 대시(-)를 사용하세요.
새 규칙의 이름은 무엇인가요? … no-archidraw
✔ 규칙에 대한 간단한 설명을 입력해주세요: … 이전 사명 사용을 금지합니다.
```

```bash {9}
✔ 규칙을 만드는 작성자의 이름을 입력해주세요: ben
✔ 새 규칙의 이름을 입력해주세요! 다음 ESLint 규칙 네이밍 컨벤션을 따라야 합니다:

- 규칙에서 무언가를 허용하지 않는 경우에는 no- 접두사를 붙이세요(예: eval()을 허용하지 않으려면 no-eval, 디버거를 허용하지 않으려면 no-debugger).
- 규칙에서 특정 항목의 포함을 강제하는 경우에는 특별한 접두사 없이 짧은 이름을 사용하세요.
- 단어 사이에는 대시(-)를 사용하세요.
새 규칙의 이름은 무엇인가요? … no-archidraw
✔ 규칙에 대한 간단한 설명을 입력해주세요: … 이전 사명 사용을 금지합니다.
✔ 경고를 트리거하지 않는 코드의 간단한 예를 입력해주세요: … import {} from 'archidraw';
```

```bash {10}
✔ 규칙을 만드는 작성자의 이름을 입력해주세요: ben
✔ 새 규칙의 이름을 입력해주세요! 다음 ESLint 규칙 네이밍 컨벤션을 따라야 합니다:

- 규칙에서 무언가를 허용하지 않는 경우에는 no- 접두사를 붙이세요(예: eval()을 허용하지 않으려면 no-eval, 디버거를 허용하지 않으려면 no-debugger).
- 규칙에서 특정 항목의 포함을 강제하는 경우에는 특별한 접두사 없이 짧은 이름을 사용하세요.
- 단어 사이에는 대시(-)를 사용하세요.
새 규칙의 이름은 무엇인가요? … no-archidraw
✔ 규칙에 대한 간단한 설명을 입력해주세요: … 이전 사명 사용을 금지합니다.
✔ 경고를 트리거하지 않는 코드의 간단한 예를 입력해주세요: … import {} from 'archidraw';
✔ 경고를 트리거하는 코드의 간단한 예를 입력해주세요: … const name = 'archidraw';
```

```bash {11}
✔ 규칙을 만드는 작성자의 이름을 입력해주세요: ben
✔ 새 규칙의 이름을 입력해주세요! 다음 ESLint 규칙 네이밍 컨벤션을 따라야 합니다:

- 규칙에서 무언가를 허용하지 않는 경우에는 no- 접두사를 붙이세요(예: eval()을 허용하지 않으려면 no-eval, 디버거를 허용하지 않으려면 no-debugger).
- 규칙에서 특정 항목의 포함을 강제하는 경우에는 특별한 접두사 없이 짧은 이름을 사용하세요.
- 단어 사이에는 대시(-)를 사용하세요.
새 규칙의 이름은 무엇인가요? … no-archidraw
✔ 규칙에 대한 간단한 설명을 입력해주세요: … 이전 사명 사용을 금지합니다.
✔ 경고를 트리거하지 않는 코드의 간단한 예를 입력해주세요: … import {} from 'archidraw';
✔ 경고를 트리거하는 코드의 간단한 예를 입력해주세요: … const name = 'archidraw';
✔ 경고를 트리거하는 코드에 대한 수정된 코드를 입력해주세요: … const name = 'archisketch';
```

```bash {12-15}
✔ 규칙을 만드는 작성자의 이름을 입력해주세요: ben
✔ 새 규칙의 이름을 입력해주세요! 다음 ESLint 규칙 네이밍 컨벤션을 따라야 합니다:

- 규칙에서 무언가를 허용하지 않는 경우에는 no- 접두사를 붙이세요(예: eval()을 허용하지 않으려면 no-eval, 디버거를 허용하지 않으려면 no-debugger).
- 규칙에서 특정 항목의 포함을 강제하는 경우에는 특별한 접두사 없이 짧은 이름을 사용하세요.
- 단어 사이에는 대시(-)를 사용하세요.
새 규칙의 이름은 무엇인가요? … no-archidraw
✔ 규칙에 대한 간단한 설명을 입력해주세요: … 이전 사명 사용을 금지합니다.
✔ 경고를 트리거하지 않는 코드의 간단한 예를 입력해주세요: … import {} from 'archidraw';
✔ 경고를 트리거하는 코드의 간단한 예를 입력해주세요: … const name = 'archidraw';
✔ 경고를 트리거하는 코드에 대한 수정된 코드를 입력해주세요: … const name = 'archisketch';
create /Users/jaemin/develop/archisketch/eslint-plugin-archisketch/lib/rules/no-archidraw.js
create /Users/jaemin/develop/archisketch/eslint-plugin-archisketch/tests/lib/rules/no-archidraw.test.js
create /Users/jaemin/develop/archisketch/eslint-plugin-archisketch/docs/rules/no-archidraw.md
✔ 새로 생성된 파일을 VS Code에서 열까요? … no
```

```bash {16-17|all}
✔ 규칙을 만드는 작성자의 이름을 입력해주세요: ben
✔ 새 규칙의 이름을 입력해주세요! 다음 ESLint 규칙 네이밍 컨벤션을 따라야 합니다:

- 규칙에서 무언가를 허용하지 않는 경우에는 no- 접두사를 붙이세요(예: eval()을 허용하지 않으려면 no-eval, 디버거를 허용하지 않으려면 no-debugger).
- 규칙에서 특정 항목의 포함을 강제하는 경우에는 특별한 접두사 없이 짧은 이름을 사용하세요.
- 단어 사이에는 대시(-)를 사용하세요.
새 규칙의 이름은 무엇인가요? … no-archidraw
✔ 규칙에 대한 간단한 설명을 입력해주세요: … 이전 사명 사용을 금지합니다.
✔ 경고를 트리거하지 않는 코드의 간단한 예를 입력해주세요: … import {} from 'archidraw';
✔ 경고를 트리거하는 코드의 간단한 예를 입력해주세요: … const name = 'archidraw';
✔ 경고를 트리거하는 코드에 대한 수정된 코드를 입력해주세요: … const name = 'archisketch';
create /Users/jaemin/develop/archisketch/eslint-plugin-archisketch/lib/rules/no-archidraw.js
create /Users/jaemin/develop/archisketch/eslint-plugin-archisketch/tests/lib/rules/no-archidraw.test.js
create /Users/jaemin/develop/archisketch/eslint-plugin-archisketch/docs/rules/no-archidraw.md
✔ 새로 생성된 파일을 VS Code에서 열까요? … no
 SUCCESS  
🚀 새 규칙을 만들 준비가 되었어요! 규칙을 작성하고 나면 `npm run test`를 실행하고, 테스트까지 성공했다면 `npm run update:eslint-docs`를 실행해 문서를 업데이트해주세요.
```
````

<div v-click="9">

이렇게 하면 새 규칙에 대한 문서, 테스트 및 규칙의 동작을 정의하는 코드가 생성됩니다. 지금은 문서 섹션을 건너뛰고 규칙 작성과 테스트 파일에 집중해보겠습니다.

</div>

---
transition: fade-out
---

### 규칙 작성

ESLint의 파서인 espree를 사용해 소스 코드를 AST로 변환하고, 정의한 규칙을 직접 플러그인을 통해 정의하고 실행할 수 있습니다.

Espree AST만 읽을 수 있다면 ESLint 규칙을 쉽게 만들 수 있습니다. `AST`에 익숙하지 않은 경우 [기여 가이드 문서](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/blob/master/CONTRIBUTING.md)에서 도움이 될 만한 몇 가지 리소스를 제공합니다. 🍺

이전 사명인 소스 코드에서 '아키드로우'를 값으로 사용하면 '아키스케치'로 바꿔야 한다고 알려주는 no-archidraw와 같은 규칙을 어떻게 정의할 수 있는지 알아보도록 하겠습니다.

먼저 코드 내 문자열이 Espree AST에서 어떻게 표현되는지 파악해야 합니다.

1. [AST Explorer](https://astexplorer.net/#/gist/eb5587c6479ffa3b23a95924bedc059e/a5d891aa1d41b3f967eaa60d92351bf1e1b02379)에 접속합니다.
2. 코드 입력 영역에 `const name = '아키드로우';`를 입력합니다.
3. 파서 설정에서 `Espree`를 선택합니다.

---
---

### 규칙 작성

`const name = '아키드로우';` 코드는 다음과 같은 AST 구조로 변환됩니다:

```json {all|11-13} twoslash
{
  "type": "VariableDeclaration",
  "declarations": [
    {
      "type": "VariableDeclarator",
      "id": {
        "type": "Identifier",
        "name": "name"
      },
      "init": {
        "type": "Literal",
        "value": "아키드로우",
        "raw": "'아키드로우'"
      }
    }
  ],
  "kind": "const"
}
```

이해하기 쉽게 일부 정보는 생략했습니다. `Literal` 타입의 노드에서 `value`를 읽으면 문자열 내용을 알 수 있습니다.

---
transition: fade-out
---

```js twoslash
console.log('아키드로우');
console.log('archidraw');
import { A } from 'archidraw-dev-team';
```

위 코드처럼 사내에서 어쩔 수 없이 `archidraw-*` 형식의 이름의 패키지를 사용하는 경우나 콘솔이나 변수명으로 사용할 때는 어떻게 해야 하는지도 감이 옵니다.

<div v-click>

import 구문은 AST로 변환했을 때 `ImportDeclaration` 타입의 노드를 가집니다. 반면 const 구문은 `VariableDeclaration` 타입의 노드를 가집니다. 코드에서의 구조를 분석할 수 있으므로 원하는 대로 범위를 좁힐 수 있습니다. 이게 정규식 대신 AST를 사용하는 이유입니다.

</div>

---
transition: slide-up
---

### 규칙 작성

<p class="text-sm">AST를 이해했으니 `lib/rules/no-archidraw.js`에서 ESLint 규칙의 동작을 정의할 수 있습니다. 아래 코드는 <span v-mark.red="1">Literal을 만났을 때</span>, 그 Literal의 값이 <br/><span v-mark.circle.orange="2">'아키드로우'를 포함</span>하는 문자열이면 에러를 <span v-mark.green="3">리포트</span>하고 올바른 문자열로 <span v-mark.circle.blue="4">수정</span>하는 코드입니다. 실제 함수는 이것보다 조금 더 복잡하지만 핵심 로직은 이게 전부입니다.</p>

````md magic-move
```js
module.exports = {
  meta: {
    /* ... */
  },
  create: function (context) {
    return {

    }
  }
}
```

```js {7-9}
module.exports = {
  meta: {
    /* ... */
  },
  create: function (context) {
    return {
      Literal(node) {

      }
    }
  }
}
```

```js {9-11}
module.exports = {
  meta: {
    /* ... */
  },
  create: function (context) {
    return {
      Literal(node) {
        if (typeof node.value !== string) return;
        if (/아키드로우/g.test(node.value)) {

        }
      }
    }
  }
}
```

```js {3-5,13-16}
module.exports = {
  meta: {
    messages: {
      useKoreanArchisketch: "'아키드로우' 대신 '아키스케치'를 사용해야 합니다.",
    },
    /* ... */
  },
  create: function (context) {
    return {
      Literal(node) {
        if (typeof node.value !== string) return;
        if (/아키드로우/g.test(node.value)) {
          context.report({
            node,
            messageId: 'useKoreanArchisketch',
          })
        }
      }
    }
  }
}
```

```js {16-18|all}
module.exports = {
  meta: {
    messages: {
      useKoreanArchisketch: "'아키드로우' 대신 '아키스케치'를 사용해야 합니다.",
    },
    /* ... */
  },
  create: function (context) {
    return {
      Literal(node) {
        if (typeof node.value !== string) return;
        if (/아키드로우/g.test(node.value)) {
          context.report({
            node,
            messageId: 'useKoreanArchisketch',
            fix: function (fixer) {
              return fixer.replaceText(node, node.raw.replace(patternKorean, '아키스케치'));
            },
          })
        }
      }
    }
  }
}
```
````

---
transition: fade-out
---

### 규칙 작성

추천 구성에 들어가야 하는 규칙이라면 `lib/configs/recommended.js` 파일의 `rules` 객체에 규칙을 추가해주세요.

```js twoslash
/** @type {import('eslint').Linter.Config}*/
module.exports = {
  plugins: ['@archisketch-dev-team'],
  rules: {
    '@archisketch-dev-team/no-archidraw': 'error',
    /* ... */
  },
};
```

---
transition: slide-up
---

### 테스트 작성

이 프로젝트에선 테스트 케이스를 작성할 시간이 충분하다면 작성할 것을 권장합니다. 누군가가 맡아서 하는 메인 프로젝트가 아니므로 다른 PR이 작업을 안전하게 계속할 수 있는 좋은 밑거름이 될 수 있도록 해주세요. 🙏

테스트 케이스를 작성하기 편하도록 테스트 케이스를 생성하고 모듈 참조 테스트 등을 위한 유틸 함수를 제공하고 있습니다. 테스트 케이스를 작성해보겠습니다:

````md magic-move
```js {*|7-13}
const path = require('node:path');

const testFilePath = (relativePath) => {
  return path.join(process.cwd(), './tests/files', relativePath);
};

const test = (t) => {
  return {
    ...t,
    filename: testFilePath(t.filename ?? 'foo.mjs'),
    parserOptions: { ecmaVersion: 2020, sourceType: 'module', ...t.parserOptions },
  };
};

module.exports = {
  testFilePath,
  test,
};
```

```js
const { test } = require('./utils');
```

```js
const { test } = require('./utils');
const rule = require('../../../lib/rules/no-archidraw'),
  RuleTester = require('eslint').RuleTester;

const ruleTester = new RuleTester();

ruleTester.run('no-archidraw', rule, {
});
```

```js
ruleTester.run('no-archidraw', rule, {
  valid: [].concat(
    test({
      code: `import { A } from 'archidraw-dev-team';`,
    }),
    test({
      code: `console.log('아키드로우');`,
    }),
  ),
});
```

```js
ruleTester.run('no-archidraw', rule, {
  valid: [].concat(
    test({
      code: `import { A } from 'archidraw-dev-team';`,
    }),
    test({
      code: `console.log('아키드로우');`,
    }),
  ),
  invalid: [].concat(
    test({
      code: `const name = '아키드로우';`,
      errors: [{ messageId: 'useKoreanArchisketch' }],
      output: `const name = '아키스케치';`,
    }),
  ),
});
```
````

---
transition: fade-out
---

## 문서 업데이트

이렇게 규칙을 하나씩 추가하다보면 10개, 100개까지 정말 많은 규칙들이 생성될 수 있습니다. <br/>그럼 규칙에 대한 <span v-mark.red="1">문서를 최신 상태로 유지</span>하기 힘들 수 있습니다.

이를 위해 문서를 업데이트하는 과정을 간소화하는 CLI를 제공합니다. 규칙을 추가하거나 규칙 메타데이터를 업데이트할 때마다 아래 명령어를 실행해주세요:

```bash
npm run update:eslint-docs
```

---
transition: fade-out
---

### README.md 업데이트

`no-archidraw` 규칙을 만들었으니 `README.md` 문서의 [기존 규칙] 목록에 추가해야 합니다. CLI를 사용하면 새 규칙은 `## 규칙들` 섹션에 자동으로 추가됩니다.

```md twoslash
<!-- README.md -->
## 규칙들
<!-- begin auto-generated rules list -->
| Name                                       | Description                                                | 💼 | ⚠️ | 🔧 |
| :----------------------------------------- | :--------------------------------------------------------- | :- | :- | :- |
| [no-archidraw](docs/rules/no-archidraw.md) | 이전 사명 사용을 금지합니다                                | ✅  |    | 🔧 |
<!-- end auto-generated rules list -->
```

<div v-click>

뿐만 아니라, `## 구성` 섹션도 업데이트됩니다.

```md twoslash
<!-- begin auto-generated configs list -->

|    | Name          |
| :- | :------------ |
| ✅  | `recommended` |

<!-- end auto-generated configs list -->
```

</div>

---
transition: fade-out
---

### 규칙 문서 업데이트

규칙에 대한 문서에서는 <span v-mark.circle.red="1">규칙 이름</span>을 포함한 <span v-mark.circle.orange="2">기본 정보</span>들이 각 규칙 문서의 상단에 자동으로 추가됩니다. 이 정보들은 규칙을 생성하는 CLI를 통해 입력한 정보를 바탕으로 생성됩니다.

```md twoslash
# 이전 사명 사용을 금지합니다 (`@archisketch-dev-team/no-archidraw`)

💼 이 규칙은 ✅ 'recommended' 구성에서 활성화됩니다.

🔧 이 규칙은 [`--fix` CLI 옵션](https://eslint.org/docs/latest/user-guide/command-line-interface#--fix)으로 자동으로 수정될 수 있습니다.

<!-- end auto-generated rule header -->
```

---
transition: fade-out
---

### 규칙 문서 검사

각 규칙에 대한 문서에는 해당 규칙에 대한 적절한 설명이 포함되어야 합니다. <br/>이를 필수로 구성되어야 할 섹션이 작성되어 있는지 여부를 검사합니다. 이 검사를 통과하지 못하면 커밋이 되지 않습니다.

```bash
npm run lint:eslint-docs
```

<div v-click>

필수로 구성되어야 하는 섹션은 다음과 같습니다:

- Rule Details
  - 이 규칙에 대한 <strong>잘못된</strong> 코드의 예
  - 이 규칙에 대한 <strong>올바른</strong> 코드의 예
- When Not To Use It
  - 이 규칙을 사용하지 않아도 되는 상황의 예

</div>

<div v-click>

규칙을 생성해주는 CLI를 이용해 생성된 문서에는 기본적인 정보를 포함해 필수 섹션이 자동으로 포함되어 있으므로 너무 걱정할 필요는 없습니다.

</div>

---
transition: fade-out
---

규칙의 <strong>이름</strong>을 수정하려면 lib/rules의 규칙 파일 이름과 일치하는 docs/rules의 문서의 규칙 설명을 업데이트해주세요. 그 뒤에 `npm run update:eslint-docs`를 실행하면 README.md의 규칙 테이블, README.md의 구성 테이블 및 해당 규칙 문서 헤더가 업데이트됩니다. 아래는 기존 `no-archidraw` 규칙을 `no-archisketch` 규칙으로 변경하는 예시입니다:

````md magic-move
```diff
// 규칙 파일 이름을 변경합니다.
- lib/rules/no-archidraw.js
+ lib/rules/no-archisketch.js
```

```diff
// `lib/index.js` 파일에서 내보내는 모듈을 업데이트합니다.
module.exports.rules = {
-  'no-archidraw': require('./rules/no-archidraw'),
+  'no-archisketch': require('./rules/no-archisketch'),
}
```

```diff
// 문서 파일 이름을 변경합니다.
- docs/rules/no-archidraw.md
+ docs/rules/no-archisketch.md
```

```diff
// 문서 내용을 변경된 내용에 맞게 수정합니다.
// @filename: docs/rules/no-archisketch.md
이 규칙에 대한 **올바른** 코드의 예입니다:
- const name = '아키스케치';
+ const name = '아키드로우';
```

```bash
npm run update:eslint-docs
```

```diff
// @filename: README.md
- | [no-archidraw](docs/rules/no-archidraw.md) | 이전 사명 사용을 금지합니다.
+ | [no-archisketch](docs/rules/no-archisketch.md) | 이전 사명 사용을 금지합니다.
```
````

<div v-click>

버그 수정을 할 땐 반드시 문서가 변경될 필요는 없지만, 기존 문서를 훑어보고 <span v-mark.red="6">수정해야 할 내용이 있는지 확인</span>하는 것이 좋습니다.

다양한 프로젝트에서 사용되므로 웬만하면 규칙의 이름을 변경하지 마세요. 이 부분에 대해서 CLI를 제공하지 않는 이유이기도 합니다.

</div>

---
transition: fade-out
---

# 플러그인 적용하기

### 설치

[ESLint](https://eslint.org/)를 먼저 설치해주세요:

```sh
npm i eslint --save-dev
```

그 다음, `.eslintrc.js` 파일을 생성해주세요:

```javascript
module.exports = {
  root: true,
};
```

`@archisketch-dev-team/eslint-plugin`를 설치해주세요:

```sh
npm install @archisketch-dev-team/eslint-plugin --save-dev
```

---
transition: fade-out
---

### 설치 및 구성

이 플러그인에는 **추천 설정이 함께 제공**됩니다. `.eslintrc` 파일에서 `extends` 속성에 `plugin:@archisketch-dev-team/recommended`를 추가해주세요:

```json
{
  "extends": ["plugin:@archisketch-dev-team/recommended"]
}
```

> 제공되는 프리셋을 사용하지 않는 경우 개별 규칙을 설정하고 일부 구성을 추가해야 합니다. 위에서 설명한 `lib/configs/recommended.js` 파일의 `rules` 객체에 추가한 규칙들이 설정됩니다.

### 규칙 재설정

특정 규칙을 재설정하고 싶다면, `rules` 섹션에서 해당 규칙을 오버라이드할 수 있습니다. 예를 들어, `no-archidraw` 규칙을 비활성화하고 `no-moment` 규칙을 오류로 표시하려면 다음과 같이 설정하세요.

```json
{
  "extends": ["plugin:@archisketch-dev-team/recommended"],
  "rules": {
    "@archisketch-dev-team/no-archidraw": "off",
    "@archisketch-dev-team/no-moment": "error"
  }
}
```

---
transition: slide-left
---

### 규칙 위반 코드 감지

이렇게 플러그인을 ESLint 구성에 추가하면 개발자들이 개발 중 규칙에 맞지 않는 코드를 작성했을 때 알려주고, 자동 수정 제안을 할 수 있습니다.

<img src="/trigger-error.png" class="max-w-[80%]">

<img src="/fixer.png" class="max-w-[80%]">

<div v-click>

Auto Fix를 실행할 경우, '(주)아키드로우' 문자열은 '(주)아키스케치'로 수정됩니다.

</div>

---
layout: statement
transition: slide-up
---

# 프로젝트 관리

---
transition: fade-out
---

## 이슈 관리

새로운 규칙을 제안하고 싶거나 규칙에 버그가 있다면 [이슈 생성](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/issues/new/choose) 페이지에서 제보할 수 있습니다.

![alt text](/issues.png)

해당하는 이슈 템플릿을 선택해 질문에 적절한 답을 작성해주면 빠르게 파악하는 데 도움이 됩니다.

---
transition: fade-out
---

## 코드 퀄리티 유지

코드 퀄리티를 유지하기 위해 딱히 해야 할 작업은 없습니다. 기본적으로 git hook을 이용해 품질을 검사하기 때문입니다.

하지만 작업 도중 확인해보고 싶다면 아래 명령어를 실행하면 됩니다:

```bash
npm run all-in-one
```

위 명령어는 다음 방법으로 전체적인 코드의 품질을 검사합니다.

---
transition: slide-up
---

### 코드 퀄리티 유지

크게 <span v-mark.red="1">커밋을 완료하기 전</span>에 <span v-mark.circle.red="1">커밋 메시지</span>와 <span v-mark.circle.red="2">변경된 문서, 스크립트</span>에 대한 검사를, 커밋을 <span v-mark.blue="3">푸시하기 전</span>에 <span v-mark.circle.blue="3">테스트 케이스</span> 통과 여부를 검사합니다.

````md magic-move
```yaml
commit-msg:
```

```yaml
# 커밋 메시지가 제안된 컨벤션에 맞는지, 스펠링이 올바른지 검사합니다.
commit-msg:
  commands:
    lint-commit-message:
      run: npx commitlint --edit $1
    spell-check:
      run: npx cspell --no-summary {1}
```

```yaml
# 문서의 정보가 올바르게 업데이트되어 있는지 검사합니다.
_pre-commit__format__docs:
  piped: true
  commands:
    1_update-docs:
      run: npm run update:eslint-docs
    2_lint-docs:
      run: npm run lint:eslint-docs

# 변경된 스크립트 파일을 컨벤션에 맞게 수정합니다.
_pre-commit__format__script:
  parallel: true
  commands:
    lint:
      glob: '*.{js}'
      run: npx eslint {staged_files}
    style:
      glob: '*.{js,json,yml}'
      run: npx prettier --write {staged_files} && git update-index --again
```

```yaml
# 커밋이 푸시되기 전에 테스트 케이스 통과 여부를 확인합니다.
pre-push:
  parallel: true
  commands:
    test:
      run: npm run test
```
````

---
transition: fade-out
---

## PR

### 기여하기

새로운 규칙을 생성하고 싶다면 PR을 생성하면 됩니다. PR의 제목은 다음 형식과 일치해야 합니다:

```bash
<type>[rule-scope]: <description>
```

> 모든 PR을 `master` 브랜치로 한 번에 병합하기 때문에 history에 있는 커밋의 수는 신경 쓰지 않습니다. 편하게 커밋해주세요.

---
transition: fade-out
---

### Type

type은 다음 중 하나여야 합니다.

<div v-click>

- feat - 새로운 규칙이 추가된 경우
- fix - 새로운 규칙을 추가하지 않는 모든 수정 사항
- docs - 문서만 변경한 경우
- test - 테스트만 변경한 경우
- chore - 위를 제외한 모든 경우

</div>

<div v-click>

### Rule Scope

변경한 규칙의 이름입니다. (예: no-archidraw)
여러 규칙을 변경한 경우 규칙 범위를 작성하는 것은 선택 사항입니다.

</div>

<div v-click>

### Description

PR 내용에 대한 명확하고 간결한 설명을 작성해주세요.

예를 들어, no-archidraw라는 새로운 규칙을 추가하기 위한 PR의 제목은 다음과 같이 작성하면 됩니다:

> feat(no-archidraw): 'archidraw' 문자열을 값으로 사용하는 것을 허용하지 않는 규칙 추가

</div>

---
transition: slide-left
---

## Commit

원활한 로그 파악을 위해 커밋 메시지에 대한 검사가 활성화되어 있습니다. 커밋 메시지에 대한 CLI를 사용하려면 아래 명령어를 입력해 커밋을 작성해주세요:

```bash
npm run cz
```

규칙에 대한 자세한 내용은 [commitlint.config](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/blob/master/commitlint.config.js)에서 확인할 수 있습니다.

---
transition: fade-out
---

## 배포

`GitHub Actions`와 `semantic-release`를 사용해 배포 과정을 자동화합니다.

---
transition: fade-out
---

### 프로세스

배포 프로세스는 다음 단계로 구성됩니다:

<div v-click>

1. 코드 변경 사항이 `master` 브랜치에 푸시됩니다.

</div>

<div v-click>

2. GitHub Actions 워크플로우(`release.yml`)가 트리거됩니다.

</div>

<div v-click>

3. 워크플로우는 노드 버전(20, 21)을 설정하고, 의존성을 설치하며, 테스트를 실행합니다.

</div>

<div v-click>

4. semantic-release가 새 버전을 결정하고, CHANGELOG를 업데이트하며, 태그를 생성하고, GitHub 릴리스를 생성합니다.

</div>

<div v-click>

5. 워크플로우가 성공적으로 완료되면, 패키지가 GitHub 패키지 레지스트리에 자동으로 배포됩니다.

</div>

---
transition: fade-out
---

### 워크플로우 주요 단계

먼저, `release.yml` 워크플로우 파일을 살펴봅니다.

````md magic-move
```yaml
# 1. 코드 변경 사항이 `master` 브랜치에 푸시되면, release.yml 워크플로우가 트리거됩니다.
on:
  push:
    branches:
      - master
```

```yaml{5-7|9-12,22-24|13|19}
# 저장소의 코드를 체크아웃하고, 필요한 노드 버전을 설정하고, 의존성을 설치하고, 테스트를 실행합니다.
jobs:
  build:
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: actions/setup-node@v4
        with:
          node-version: 21
          cache: npm
      - run: npm ci

      - name: Test build package on node@21 (Current)
        run: |
          node --version
          npm --version
          npm run test

      # `matrix`를 사용하지 않는 이유는 그냥 복제하고 새 인스턴스를 생성하지 않는 것이 더 간단하기 때문입니다.
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - name: test build package on node@20 (LTS)
        ...
```

```yaml{2-3|8-13|15-20}
# 패키지를 빌드하고, semantic-release를 사용해 새 버전을 결정하고 릴리스하고, npm publish를 사용해 패키지를 GitHub 패키지 레지스트리에 배포합니다.
- name: Build package
  run: npm run build

- name: Verify the integrity of provenance attestations and registry signatures for installed dependencies
  # 패키지가 변조되었는지 확인합니다.
  run: npm audit signatures

- name: Release
  if: github.event_name == 'push' && github.ref == 'refs/heads/master'
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  run: npx semantic-release
  continue-on-error: true

- name: Publish to GitHub Package Registry
  run: |
    npm run build
    npm publish
  env:
    # GitHub API에 액세스할 수 있도록 하는 토큰입니다.
    NODE_AUTH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
````

---
transition: fade-out
---

### Package.json

`package.json` 파일에선 패키지의 메타데이터와 스크립트를 정의해두었습니다.

```json twoslash
"name": "@archisketch-dev-team/eslint-plugin",
"version": "1.0.2",
"publishConfig": {
  "registry": "https://npm.pkg.github.com/"
},
"scripts": {
  "------------------------------TEST------------------------------": "",
  "test": "mocha tests --recursive",
  "------------------------------BUILD------------------------------": "",
  "build": "node tasks/build.js",
},
```

---
transition: slide-up
---

### Semantic Release Config

`semantic-release`의 설정은 `release.config.js` 파일에서 정의할 수 있습니다.

이 패키지에선 커밋 메시지 분석, 릴리스 노트 생성, CHANGELOG 업데이트, npm 및 GitHub 릴리스, git 태그 생성 등을 위한 플러그인을 설정해두었습니다.

```yaml
# 배포할 브랜치를 지정합니다.
branches: [{ name: 'master' }],
plugins: [
  # 커밋 메시지를 분석하여 버전을 자동으로 결정합니다. 커밋 메시지는 `conventional commit` 규칙을 따라야 합니다. (`npm run cz` 명령어로 커밋 메시지에 대한 CLI를 사용할 수 있습니다)
  ['@semantic-release/commit-analyzer', { preset: 'conventionalcommits' }],
  ['@semantic-release/release-notes-generator', { preset: 'conventionalcommits' }],
  # 자동으로 CHANGELOG를 생성하고, npm에 배포하지 않고 GitHub 릴리스를 생성합니다. `npm publish`는 release.yml 워크플로우에서 수동으로 실행합니다.
  '@semantic-release/changelog',
  [
    '@semantic-release/npm',
    {
      npmPublish: false,
    },
  ],
  ['@semantic-release/github', { successComment: false }],
  '@semantic-release/git',
  '@saithodev/semantic-release-backmerge',
],
```

---
---

# 지속 가능한 개발

이렇게 일반적인 작업을 자동화하고 필요한 규칙을 빠르게 구현할 CLI를 제공함으로써 프로젝트 구조를 잘 모르는 개발자도 JS와 AST만 이해하고 있다면 쉽게 규칙을 만들고 로직을 구현하는 데 더 집중할 수 있게 해줍니다.

이 패키지는 궁극적으로 <span v-mark.red="1">운영 부채를 상환</span>하는 데 큰 역할을 하는 것을 목표로 합니다.

앞으로 더 많은 ESLint 규칙을 만들어 프로젝트의 유지보수성을 향상할 계획입니다. 아래는 작업 예정에 있는 규칙입니다:

- ban-words: [기능 제안 이슈](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/issues/14)에서 해당 규칙에 대해 자세히 설명합니다.
- archi-design/hierarchical-import: 각 폴더의 계층 관계를 명확히 하기 위한 규칙입니다. ex) `shared/` 모듈에서 `features/` 내 모듈을 import할 수 없도록 강제합니다.

좋은 아이디어가 있다면 직접 [구현](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/blob/master/CONTRIBUTING.md)하거나 기능을 [요청](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/issues/new/choose)해주세요.

---

# 마무리

감사합니다

```js
module.exports = {
  extends: [
    'plugin:@archisketch-dev-team/recommended',
  ],
  ...
}
```

<div class="w-60 relative">
  <div class="relative w-40 h-40">
    <img
      v-motion
      :initial="{ x: 800, y: -100, scale: 1.5, rotate: -50 }"
      :enter="final"
      class="absolute inset-0"
      src="https://archisketch-resources.s3.ap-northeast-2.amazonaws.com/service/V2/9fadc5c2-3d4c-4ff3-b5c7-6aa1f24f0168.png"
      alt=""
    />
    <img
      v-motion
      :initial="{ y: 500, x: -100, scale: 2 }"
      :enter="final"
      class="absolute inset-0"
      src="https://avatars.githubusercontent.com/u/60460294?s=48&v=4"
      alt=""
    />
    <img
      v-motion
      :initial="{ x: 600, y: 400, scale: 2, rotate: 100 }"
      :enter="final"
      class="absolute right-0 size-12"
      src="https://upload.wikimedia.org/wikipedia/commons/e/e3/ESLint_logo.svg"
      alt=""
    />
  </div>

  <div
    class="text-5xl absolute top-14 left-40 text-[#2E2EE8] -z-1"
    v-motion
    :initial="{ x: -80, opacity: 0}"
    :enter="{ x: 20, opacity: 1, transition: { delay: 2000, duration: 1000 } }">
    ESLint Plugin Archisketch
  </div>
</div>

<!-- vue script setup scripts can be directly used in markdown, and will only affects current page -->
<script setup lang="ts">
const final = {
  x: 0,
  y: 0,
  rotate: 0,
  scale: 1,
  transition: {
    type: 'spring',
    damping: 10,
    stiffness: 20,
    mass: 2
  }
}
</script>

<div
  v-motion
  :initial="{ x:35, y: 30, opacity: 0}"
  :enter="{ y: 0, opacity: 1, transition: { delay: 3500 } }">

작성자: Ben

</div>

---
layout: center
class: text-center
---

# 자세히 알아보기

[GitHub](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/tree/master) · [Install](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/blob/master/README.md#archisketch-dev-teameslint-plugin-%EC%84%A4%EC%B9%98) · [Contribute Guide](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/blob/master/CONTRIBUTING.md) · [Issue Templates](https://github.com/archisketch-dev-team/eslint-plugin-archisketch/issues/new/choose)