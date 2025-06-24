# C# Extension for StarUML 2

StarUML 2용 C# 코드 생성 및 역공학 확장 프로그램입니다. UML 다이어그램에서 C# 코드를 자동으로 생성할 수 있습니다.

## 📋 목차

- [기능](#-기능)
- [설치](#-설치)
- [사용법](#-사용법)
- [설정](#-설정)
- [지원하는 UML 요소](#-지원하는-uml-요소)
- [생성되는 C# 코드 예시](#-생성되는-c-코드-예시)
- [개발자 정보](#-개발자-정보)
- [라이선스](#-라이선스)

## ✨ 기능

- **C# 코드 생성**: UML 클래스 다이어그램에서 C# 클래스, 인터페이스, 열거형 등을 자동 생성
- **CsharpDoc 주석 생성**: 코드와 함께 XML 문서 주석 자동 생성
- **사용자 정의 설정**: 들여쓰기, 탭/스페이스 선택 등 코드 스타일 커스터마이징
- **패키지 구조 지원**: UML 패키지 구조를 네임스페이스로 변환
- **역공학 지원**: C# 코드에서 UML 다이어그램 생성 (개발 예정)

## 🚀 설치

### 요구사항
- StarUML 2.0.0 이상

### 설치 방법

1. **Extension Manager를 통한 설치** (권장)
   - StarUML에서 `Tools` > `Extension Manager` 선택
   - `Registry` 탭에서 "C#" 검색
   - `Install` 버튼 클릭

2. **수동 설치**
   - 이 저장소를 다운로드하거나 클론
   - StarUML 확장 폴더에 복사:
     - Windows: `%APPDATA%\StarUML\extensions\user\staruml.csharp`
     - macOS: `~/Library/Application Support/StarUML/extensions/user/staruml.csharp`
     - Linux: `~/.config/StarUML/extensions/user/staruml.csharp`
   - StarUML 재시작

## 📖 사용법

### 1. C# 코드 생성

1. StarUML에서 UML 클래스 다이어그램 작성
2. 메뉴에서 `Tools` > `C#` > `Generate Code...` 선택
3. 코드를 생성할 기본 모델(패키지) 선택
4. 생성된 파일을 저장할 폴더 선택
5. 코드 생성 완료

### 2. 설정 변경

1. 메뉴에서 `Tools` > `C#` > `Configure...` 선택
2. 원하는 설정 변경:
   - **CsharpDoc**: XML 문서 주석 생성 여부
   - **Use Tab**: 들여쓰기에 탭 사용 여부
   - **Indent Spaces**: 스페이스 들여쓰기 크기 (기본값: 4)

## ⚙️ 설정

### 코드 생성 옵션

| 설정 | 설명 | 기본값 |
|------|------|--------|
| CsharpDoc | XML 문서 주석 생성 | true |
| Use Tab | 탭을 사용한 들여쓰기 | false |
| Indent Spaces | 스페이스 들여쓰기 크기 | 4 |

## 🎯 지원하는 UML 요소

### 클래스 (Class)
- 속성 (Attributes)
- 메서드 (Operations)
- 가시성 (Visibility): public, private, protected, internal
- 정적 멤버 (Static members)
- 추상 클래스 (Abstract classes)

### 인터페이스 (Interface)
- 메서드 시그니처
- 속성 정의

### 열거형 (Enumeration)
- 열거 값들
- 사용자 정의 값

### 관계 (Relationships)
- 상속 (Generalization)
- 구현 (Realization)
- 연관 (Association)
- 집합 (Aggregation)
- 합성 (Composition)

## 💻 생성되는 C# 코드 예시

### UML 클래스에서 생성되는 C# 코드

**UML 클래스:**
```
Person
- name: string
- age: int
+ getName(): string
+ setName(name: string): void
```

**생성되는 C# 코드:**
```csharp
/// <summary>
/// Person 클래스
/// </summary>
public class Person
{
    /// <summary>
    /// 이름
    /// </summary>
    private string name;
    
    /// <summary>
    /// 나이
    /// </summary>
    private int age;
    
    /// <summary>
    /// 이름을 반환합니다.
    /// </summary>
    /// <returns>이름</returns>
    public string getName()
    {
        // TODO: 구현 필요
        return null;
    }
    
    /// <summary>
    /// 이름을 설정합니다.
    /// </summary>
    /// <param name="name">설정할 이름</param>
    public void setName(string name)
    {
        // TODO: 구현 필요
    }
}
```

## 🏗️ 프로젝트 구조

```
├── main.js                 # 메인 진입점, 명령어 등록
├── CsharpCodeGenerator.js  # C# 코드 생성 로직
├── CsharpPreferences.js    # 사용자 설정 관리
├── CodeGenUtils.js         # 코드 생성 유틸리티
├── package.json           # 확장 프로그램 메타데이터
└── README.md              # 프로젝트 문서
```

### 주요 모듈 설명

- **main.js**: StarUML 확장의 진입점으로, 메뉴 등록 및 명령어 핸들러 정의
- **CsharpCodeGenerator.js**: UML 모델을 분석하여 C# 코드를 생성하는 핵심 로직
- **CsharpPreferences.js**: 사용자 설정 관리 및 기본값 정의
- **CodeGenUtils.js**: 코드 작성을 위한 유틸리티 클래스 (CodeWriter 등)

## 🔧 개발 및 기여

### 개발 환경 설정

1. 저장소 클론
```bash
git clone https://github.com/dongjoon1251/CSharp.git
```

2. StarUML 확장 폴더에 심볼릭 링크 생성
3. StarUML에서 `Debug` > `Reload Extensions` 실행

### 코드 스타일

- JavaScript ES5 문법 사용
- AMD 모듈 패턴 준수
- JSLint 규칙 준수

## 🐛 알려진 이슈

- 역공학 기능은 현재 개발 중입니다
- 복잡한 제네릭 타입 지원이 제한적입니다
- 일부 C# 고급 기능은 지원되지 않을 수 있습니다

## 📞 지원 및 문의

- **이슈 리포트**: [GitHub Issues](https://github.com/dongjoon1251/CSharp/issues)
- **이메일**: joon1251@gmail.com

## 👨‍💻 개발자 정보

- **개발자**: Dongjoon Lee
- **이메일**: joon1251@gmail.com
- **GitHub**: [@dongjoon1251](https://github.com/dongjoon1251)

## 📄 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

---

## 🔄 버전 히스토리

### v0.1.0
- 초기 릴리스
- 기본 C# 코드 생성 기능
- CsharpDoc 주석 생성
- 사용자 설정 지원

---

**StarUML 2와 함께 더 효율적인 C# 개발을 경험해보세요!** 🚀

