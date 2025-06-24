# API 문서

StarUML C# 확장 프로그램의 API 문서입니다.

## 📋 목차

- [CsharpCodeGenerator](#csharpcodegenerator)
- [CsharpPreferences](#csharppreferences)
- [CodeGenUtils](#codegenutils)
- [명령어 ID](#명령어-id)

## CsharpCodeGenerator

C# 코드 생성을 담당하는 메인 클래스입니다.

### 생성자

```javascript
CsharpCodeGenerator(baseModel, basePath)
```

**매개변수:**
- `baseModel` (type.UMLPackage): 코드 생성의 기준이 되는 UML 패키지
- `basePath` (string): 생성된 파일들이 저장될 기본 경로

### 주요 메서드

#### generate(baseModel, basePath, options)

UML 모델에서 C# 코드를 생성합니다.

**매개변수:**
- `baseModel` (type.UMLPackage): 코드 생성 대상 모델
- `basePath` (string): 출력 경로
- `options` (Object): 생성 옵션

**반환값:**
- `Promise`: 코드 생성 완료 시 resolve되는 Promise

**옵션 객체:**
```javascript
{
    csharpDoc: boolean,      // CsharpDoc 주석 생성 여부
    useTab: boolean,         // 탭 사용 여부
    indentSpaces: number     // 들여쓰기 스페이스 수
}
```

### 내부 메서드

#### writePackage(elem)
패키지를 처리하여 네임스페이스를 생성합니다.

#### writeClass(elem)
UML 클래스를 C# 클래스로 변환합니다.

#### writeInterface(elem)
UML 인터페이스를 C# 인터페이스로 변환합니다.

#### writeEnumeration(elem)
UML 열거형을 C# enum으로 변환합니다.

#### writeAttribute(attr)
UML 속성을 C# 필드/프로퍼티로 변환합니다.

#### writeOperation(op)
UML 연산을 C# 메서드로 변환합니다.

## CsharpPreferences

사용자 설정을 관리하는 클래스입니다.

### 설정 항목

#### csharp.gen.csharpDoc
- **타입**: Boolean
- **기본값**: true
- **설명**: CsharpDoc XML 주석 생성 여부

#### csharp.gen.useTab
- **타입**: Boolean
- **기본값**: false
- **설명**: 들여쓰기에 탭 사용 여부

#### csharp.gen.indentSpaces
- **타입**: Number
- **기본값**: 4
- **설명**: 스페이스 들여쓰기 크기

### 메서드

#### getId()
설정 ID를 반환합니다.

**반환값:**
- `string`: "csharp"

#### getGenOptions()
현재 설정된 코드 생성 옵션을 반환합니다.

**반환값:**
- `Object`: 코드 생성 옵션 객체

## CodeGenUtils

코드 생성을 위한 유틸리티 클래스들을 제공합니다.

### CodeWriter

코드 작성을 도와주는 유틸리티 클래스입니다.

#### 생성자

```javascript
CodeWriter(indentString)
```

**매개변수:**
- `indentString` (string): 들여쓰기 문자열 (기본값: 4개 스페이스)

#### 메서드

##### writeLine(line)
한 줄을 작성합니다.

**매개변수:**
- `line` (string): 작성할 텍스트

##### indent()
들여쓰기 레벨을 증가시킵니다.

##### outdent()
들여쓰기 레벨을 감소시킵니다.

##### getIndentString()
현재 들여쓰기 문자열을 반환합니다.

**반환값:**
- `string`: 현재 들여쓰기 문자열

##### getData()
작성된 모든 코드를 문자열로 반환합니다.

**반환값:**
- `string`: 완성된 코드 문자열

## 명령어 ID

확장 프로그램에서 사용하는 명령어 ID들입니다.

### 상수

- `CMD_CSHARP`: "csharp" - 메인 C# 명령어
- `CMD_CSHARP_GENERATE`: "csharp.generate" - 코드 생성 명령어
- `CMD_CSHARP_REVERSE`: "csharp.reverse" - 역공학 명령어 (미구현)
- `CMD_CSHARP_CONFIGURE`: "csharp.configure" - 설정 명령어

### 명령어 핸들러

#### _handleGenerate(base, path, options)
C# 코드 생성을 처리합니다.

**매개변수:**
- `base` (Element): 기준 모델 (선택사항)
- `path` (string): 출력 경로 (선택사항)
- `options` (Object): 생성 옵션 (선택사항)

**반환값:**
- `Promise`: 처리 완료 시 resolve되는 Promise

#### _handleReverse()
역공학을 처리합니다. (현재 미구현)

#### _handleConfigure()
설정 대화상자를 엽니다.

## 사용 예시

### 프로그래밍 방식으로 코드 생성

```javascript
// 모듈 로드
var CsharpCodeGenerator = require("CsharpCodeGenerator");
var CsharpPreferences = require("CsharpPreferences");

// 옵션 설정
var options = CsharpPreferences.getGenOptions();
options.csharpDoc = true;
options.useTab = false;
options.indentSpaces = 4;

// 코드 생성
var generator = new CsharpCodeGenerator(baseModel, "/output/path");
generator.generate(baseModel, "/output/path", options)
    .then(function() {
        console.log("코드 생성 완료");
    })
    .catch(function(error) {
        console.error("코드 생성 실패:", error);
    });
```

### 사용자 정의 CodeWriter 사용

```javascript
var CodeGenUtils = require("CodeGenUtils");

// CodeWriter 생성
var writer = new CodeGenUtils.CodeWriter("    "); // 4 스페이스 들여쓰기

// 코드 작성
writer.writeLine("public class MyClass");
writer.writeLine("{");
writer.indent();
writer.writeLine("private string name;");
writer.writeLine("");
writer.writeLine("public string Name");
writer.writeLine("{");
writer.indent();
writer.writeLine("get { return name; }");
writer.writeLine("set { name = value; }");
writer.outdent();
writer.writeLine("}");
writer.outdent();
writer.writeLine("}");

// 결과 출력
console.log(writer.getData());
```

## 확장 및 커스터마이징

### 새로운 코드 생성 규칙 추가

`CsharpCodeGenerator.js`를 수정하여 새로운 UML 요소나 C# 기능을 지원할 수 있습니다:

1. 새로운 `write*` 메서드 추가
2. `generate` 메서드에서 해당 메서드 호출
3. 필요한 경우 설정 옵션 추가

### 새로운 설정 옵션 추가

`CsharpPreferences.js`에서 새로운 설정을 추가할 수 있습니다:

```javascript
"csharp.gen.newOption": {
    text: "새 옵션",
    description: "새로운 옵션에 대한 설명",
    type: "Check", // 또는 "Number", "String" 등
    default: false
}
```

## 오류 처리

### 일반적인 오류 상황

1. **파일 시스템 오류**: 출력 경로에 쓰기 권한이 없는 경우
2. **모델 오류**: 잘못된 UML 모델이 전달된 경우
3. **설정 오류**: 잘못된 설정값이 전달된 경우

### 오류 처리 방법

```javascript
generator.generate(baseModel, basePath, options)
    .then(function(result) {
        // 성공 처리
    })
    .catch(function(error) {
        if (error === FileSystem.USER_CANCELED) {
            // 사용자 취소
        } else {
            // 기타 오류 처리
            console.error("오류 발생:", error);
        }
    });
```

