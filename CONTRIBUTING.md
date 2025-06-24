# 기여 가이드

StarUML C# 확장 프로그램에 기여해주셔서 감사합니다! 이 문서는 프로젝트에 기여하는 방법을 안내합니다.

## 📋 목차

- [기여 방법](#-기여-방법)
- [개발 환경 설정](#-개발-환경-설정)
- [코딩 스타일](#-코딩-스타일)
- [테스트](#-테스트)
- [Pull Request 가이드라인](#-pull-request-가이드라인)
- [이슈 리포팅](#-이슈-리포팅)
- [문서화](#-문서화)

## 🤝 기여 방법

다음과 같은 방법으로 프로젝트에 기여할 수 있습니다:

- 🐛 **버그 리포트**: 발견한 버그를 이슈로 등록
- 💡 **기능 제안**: 새로운 기능이나 개선사항 제안
- 🔧 **코드 기여**: 버그 수정이나 새 기능 구현
- 📚 **문서 개선**: README, API 문서, 예제 등 개선
- 🌍 **번역**: 다른 언어로 문서 번역
- 🧪 **테스트**: 다양한 환경에서 테스트 및 피드백

## 🛠️ 개발 환경 설정

### 필수 요구사항

- StarUML 2.0.0 이상
- Git
- 텍스트 에디터 (VS Code, Sublime Text 등)

### 설정 단계

1. **저장소 포크 및 클론**
   ```bash
   git clone https://github.com/YOUR_USERNAME/CSharp.git
   cd CSharp
   ```

2. **개발 브랜치 생성**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **StarUML 확장 폴더에 링크 생성**
   
   **Windows:**
   ```cmd
   mklink /D "%APPDATA%\StarUML\extensions\user\staruml.csharp" "C:\path\to\your\CSharp"
   ```
   
   **macOS/Linux:**
   ```bash
   ln -s /path/to/your/CSharp ~/Library/Application\ Support/StarUML/extensions/user/staruml.csharp
   ```

4. **StarUML에서 확장 로드**
   - StarUML 실행
   - `Debug` > `Reload Extensions` 선택
   - 또는 `Ctrl+Shift+F5` (Windows/Linux) / `Cmd+Shift+F5` (macOS)

### 개발 워크플로우

1. 코드 수정
2. StarUML에서 `Debug` > `Reload Extensions`로 변경사항 로드
3. 기능 테스트
4. 필요시 반복

## 📝 코딩 스타일

### JavaScript 스타일 가이드

프로젝트는 다음 코딩 스타일을 따릅니다:

#### 기본 규칙

- **들여쓰기**: 4개 스페이스 사용
- **세미콜론**: 항상 사용
- **따옴표**: 문자열에 큰따옴표 사용
- **변수명**: camelCase 사용
- **상수**: UPPER_SNAKE_CASE 사용

#### 예시

```javascript
// 좋은 예
var myVariable = "hello world";
var MY_CONSTANT = 42;

function myFunction(param1, param2) {
    if (param1 === "test") {
        return param2 + 1;
    }
    return 0;
}

// 나쁜 예
var my_variable='hello world'
var myconstant=42

function myfunction(param1,param2){
if(param1=='test'){
return param2+1
}
return 0
}
```

#### JSLint 규칙

프로젝트는 JSLint를 사용합니다. 다음 설정을 준수해주세요:

```javascript
/*jslint vars: true, plusplus: true, devel: true, nomen: true, indent: 4, maxerr: 50, regexp: true */
```

#### AMD 모듈 패턴

모든 모듈은 AMD 패턴을 사용합니다:

```javascript
define(function (require, exports, module) {
    "use strict";
    
    // 모듈 의존성
    var Dependency = require("Dependency");
    
    // 모듈 구현
    function MyModule() {
        // 구현 내용
    }
    
    // 내보내기
    exports.MyModule = MyModule;
});
```

### 주석 스타일

#### JSDoc 주석

함수와 클래스에는 JSDoc 주석을 사용합니다:

```javascript
/**
 * 클래스에 대한 설명
 * @constructor
 * @param {type.UMLPackage} baseModel 기본 모델
 * @param {string} basePath 기본 경로
 */
function CsharpCodeGenerator(baseModel, basePath) {
    // 구현
}

/**
 * 메서드에 대한 설명
 * @param {Element} elem UML 요소
 * @return {string} 생성된 코드
 */
CsharpCodeGenerator.prototype.writeClass = function (elem) {
    // 구현
};
```

#### 인라인 주석

복잡한 로직에는 설명 주석을 추가합니다:

```javascript
// 사용자가 기본 모델을 선택하지 않은 경우 ElementPicker 표시
if (!base) {
    ElementPickerDialog.showDialog("Select a base model to generate codes", null, type.UMLPackage)
        .done(function (buttonId, selected) {
            // 처리 로직
        });
}
```

## 🧪 테스트

### 수동 테스트

현재 프로젝트는 자동화된 테스트가 없으므로 수동 테스트를 수행합니다:

#### 기본 기능 테스트

1. **코드 생성 테스트**
   - 다양한 UML 클래스 다이어그램 생성
   - `Tools` > `C#` > `Generate Code...` 실행
   - 생성된 C# 코드 확인

2. **설정 테스트**
   - `Tools` > `C#` > `Configure...` 실행
   - 각 설정 옵션 변경 후 코드 생성
   - 설정이 올바르게 적용되는지 확인

3. **다양한 UML 요소 테스트**
   - 클래스, 인터페이스, 열거형
   - 상속, 구현, 연관 관계
   - 다양한 가시성 수준

#### 테스트 체크리스트

- [ ] 기본 클래스 생성
- [ ] 인터페이스 생성
- [ ] 열거형 생성
- [ ] 상속 관계 처리
- [ ] 구현 관계 처리
- [ ] 속성 생성 (다양한 타입)
- [ ] 메서드 생성 (다양한 시그니처)
- [ ] CsharpDoc 주석 생성
- [ ] 들여쓰기 설정 적용
- [ ] 패키지 구조를 네임스페이스로 변환

### 테스트 환경

다음 환경에서 테스트해주세요:

- **운영체제**: Windows, macOS, Linux
- **StarUML 버전**: 2.0.0 이상의 다양한 버전
- **UML 모델**: 간단한 것부터 복잡한 것까지

## 📬 Pull Request 가이드라인

### PR 제출 전 체크리스트

- [ ] 코드가 프로젝트의 코딩 스타일을 따름
- [ ] 새로운 기능에 대한 테스트 완료
- [ ] 기존 기능이 정상 작동함을 확인
- [ ] 문서 업데이트 (필요한 경우)
- [ ] 커밋 메시지가 명확함

### PR 제목 및 설명

#### 제목 형식
```
[타입] 간단한 설명

예시:
[Feature] Add support for generic types
[Fix] Fix namespace generation bug
[Docs] Update API documentation
```

#### 설명 템플릿
```markdown
## 변경사항
- 변경된 내용을 간단히 설명

## 동기
- 왜 이 변경이 필요한지 설명

## 테스트
- 어떻게 테스트했는지 설명
- 테스트 결과

## 스크린샷 (해당하는 경우)
- 변경사항을 보여주는 스크린샷

## 체크리스트
- [ ] 코딩 스타일 준수
- [ ] 테스트 완료
- [ ] 문서 업데이트
```

### 커밋 메시지 가이드라인

#### 형식
```
[타입] 제목 (50자 이내)

본문 (필요한 경우, 72자로 줄바꿈)

- 변경사항 1
- 변경사항 2
```

#### 타입
- `feat`: 새로운 기능
- `fix`: 버그 수정
- `docs`: 문서 변경
- `style`: 코드 스타일 변경 (기능 변경 없음)
- `refactor`: 리팩토링
- `test`: 테스트 추가/수정
- `chore`: 빌드 프로세스나 도구 변경

## 🐛 이슈 리포팅

### 버그 리포트

버그를 발견했다면 다음 정보를 포함해서 이슈를 등록해주세요:

#### 템플릿
```markdown
## 버그 설명
버그에 대한 명확하고 간단한 설명

## 재현 단계
1. '...' 이동
2. '...' 클릭
3. '...' 입력
4. 오류 발생

## 예상 동작
무엇이 일어날 것으로 예상했는지

## 실제 동작
실제로 무엇이 일어났는지

## 환경
- OS: [예: Windows 10]
- StarUML 버전: [예: 2.8.0]
- 확장 버전: [예: 0.1.0]

## 추가 정보
스크린샷, 로그, 기타 관련 정보
```

### 기능 요청

새로운 기능을 제안할 때는 다음 정보를 포함해주세요:

#### 템플릿
```markdown
## 기능 설명
제안하는 기능에 대한 명확하고 간단한 설명

## 동기
이 기능이 왜 필요한지, 어떤 문제를 해결하는지

## 제안된 해결책
어떻게 구현할지에 대한 아이디어

## 대안
고려해본 다른 해결책들

## 추가 정보
기타 관련 정보나 스크린샷
```

## 📚 문서화

### 문서 기여

문서 개선도 중요한 기여입니다:

- **README.md**: 사용자 가이드 개선
- **API.md**: API 문서 업데이트
- **CONTRIBUTING.md**: 기여 가이드 개선
- **예제 추가**: 사용 예시나 튜토리얼

### 문서 작성 가이드라인

- 명확하고 간단한 언어 사용
- 코드 예시 포함
- 스크린샷이나 다이어그램 활용
- 다양한 사용자 레벨 고려 (초보자부터 고급자까지)

## 🌍 번역

다른 언어로 문서를 번역하고 싶다면:

1. 새로운 언어 폴더 생성 (예: `docs/ko/`, `docs/ja/`)
2. 해당 언어로 문서 번역
3. PR 제출

## 📞 도움이 필요한 경우

- **GitHub Issues**: 질문이나 도움 요청
- **이메일**: joon1251@gmail.com
- **토론**: GitHub Discussions (활성화된 경우)

## 🎉 기여자 인정

모든 기여자는 다음과 같이 인정받습니다:

- README.md의 기여자 섹션에 이름 추가
- 릴리스 노트에 기여 내용 언급
- 특별한 기여에 대해서는 별도 감사 표시

---

**여러분의 기여가 이 프로젝트를 더욱 발전시킵니다. 감사합니다!** 🙏

