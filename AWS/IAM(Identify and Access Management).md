### AWS서비스를 시작하며..

개발자로 aws에 가입하고 무엇을 해야할지 모르는 분들이 있을 것이라고 생각합니다.

저도 프리티어라는 1년간의 많은 자원을 어떻게 사용할지 모르지만

같이 공부하고 실습하며 배워가보자 합니다.

**첫 시작은 IAM입니다.** 서비스를 사용하기전 사용자에 대해서 알아봅시다.

( 잘못된 내용에 대해서는 댓글로 알려주시면 수정하겠습니다..)

---

### IAM (Identify and Access Managemet)

[여기](https://us-east-1.console.aws.amazon.com/iam/home#/home)에서 사용할 수 있는 서비스입니다.

인증(Identify)과 접근(Access)를 관리하는 서비스인데요.

저처럼 개인 프로젝트를 사용하는 것이 아닌 회사, 팀별로 아이디를 사용하는 경우가 있습니다.

그렇다면 해당 직책과 파트에 맞게 리소스 또는 서비스를 관리해야하는 상황이 오게됩니다.

바로 그 순간 사용하는 서비스라고 생각합니다.

정리하자면 사용자에 맞게 서비스나 리소스에 대한 권한을 정리하는 서비스라는 것이죠.

---

### IAM의 구성

![image](https://user-images.githubusercontent.com/68093714/160283537-3a033d88-1288-4e30-aaef-549bd619403b.png)

AWS의 서비스를 보면 대시보드에 중요 요소가 있는 것을 확인할 수 있습니다.

IAM의 대시보드를 보면 5가지의 구성이 있는데요.

**사용자 그룹, 사용자, 역할, 정책, 자격 증명 공급자**가 있고 뒤에서부터 하나씩 알아보도록 하겠습니다.

(자격 증명 공급자)에 대해서는 공부 후 추가하도록 하겠습니다.)

---

### 정책

AWS서비스들은 서비스가 제공하는 범위에 따라 권한이 주어집니다.

대표적인 서비스 EC2, S3, EBS 등등에 접근, 수정과 같이 권한이 나누어져 있습니다.

예를 들면, 집이라는 서비스에서 TV를 보는 권한, 사진첩을 보는 권한 이라고 나눌 수 있겠네요.

**정책**은 이러한 **권한을 묶어놓은 것**이라고 생각하면 됩니다.

사용자가 특정 서비스에 접근만 가능하다고 할때 서비스안에 있는 모든 접근이라는 권한을 한개씩 추가하는 것은 비효율적이겠죠..

따라서 AWS에서는 (AmazonEC2ReadOnlyAccess) 와 같이 권한을 묶어놓은 정책을 제공해줍니다.

\*AmazonEC2ReadOnlyAccess: 직관적으로 EC2를 읽을 수만 있는 권한의 묶음이라고 느껴지죠

AWS에서 제공했듯이 이름과 권한을 상황에 맞게 생성해서 쓰면 유용한 기능입니다.

---

### 역할

**역할**은 정책 또는 권한을 사용할 수 있는 직업이라고 생각하시면 좋습니다.

직업에 맞는 이름과 **적합한 정책 또는 권한들을 추가**하여 만들어 준 것인데요.

예를 들면, 마피아게임에서 마피아 또는 경찰이 될 사람은 모르지만 마피아는 밤에 일어나 시민을 해하는 권한을 갖고있고 경찰은 밤에 일어나 시민과 마피아를 확인할 수 있는 권한이 정해져 있는 것과 같습니다.

이처럼 역할은 누군가에게 맞는 직업을 주어 정책과 권한을 관리한다고 생각하시면 됩니다.

| 중요한 점은 지정된 사용자가 아닌 누군가에게 주는 역할이기 때문에 임시적인 액세스 권한입니다.   일반 사용자와 다르게 **임시적으로 보안 자격 증명(사용 접근 허가)을 제공**한다고 생각하시면 됩니다. |
| --- |

\* 정책과 권한이라고 했듯이 정책뿐만 아니라 권한 한개를 추가 가능합니다.

\*\* 역할에 맞는 권한을 아예 만들어서 사용하는 방법도 있지만.. 추가 또는 삭제가 자주 일어날 것 같습니다.

---

### 사용자

이제 **사용자**입니다. 이름에서 알 수 있듯이 사용하는 사람을 정의하는 기능인데요.

맨 처음에 회사 또는 팀에서 관리하는 계정이라고 말씀드렸듯이 계정 하나를 두고 여러 개의 사용자를 만들어서 사용할 수 있습니다. 바로 **루트 사용자**가 회사 또는 팀의 계정이고 **사용자**가 팀원들의 계정이 됩니다.

사용자를 생성시에는 AWS 자격 증명 유형이 두 가지가 있는데요.

```
액세스 키 : AWS API, CLI, SDK 및 기타 개발도구를 사용하는 액세스 키 ID와 비밀 액세스 키를 활성화  
암호 : AWS 콘솔(웹 환경)을 로그인할 수 있도록 암호를 만들어 활성화
```

꼭 한가지는 선택해야 사용자의 자격이 증명이 되고 두개 모두 사용할 수 있습니다.

이후 사용자에게 맞는 정책을 연결해주시면 됩니다. (역할과는 다르게 권한을 직접 적용할 수 없습니다..)

---

### 사용자 그룹

마지막으로 **사용자 그룹**입니다. 이것도 이름에서 알 수 있듯이 사용자를 모아놓은 그룹인데요.

부서에 맞는 **정책들을 모아놓고** 사용자를 추가하면, 사용자는 **그룹에서 정의해놓은 정책을 사용**할 수 있는 개념입니다.

예를 들면, 일반인이었던 제가 신발가게알바라는 그룹의 사용자가 되면 신발창고에 접근할 수 있다는 것과 비슷하네요.

회사와 팀에서는 각 부서 및 파트를 나누어 그룹으로 관리하고 해당하는 사람을 사용자로 넣어서 쉽게 관리할 수 있게 됩니다.

---

### 마무리

IAM에 대한 기능을 천천히 정리했습니다.

간단하게 개념을 이해한다면 콘솔(웹 환경)에서 생성, 제거와 같은 기능을 사용할 때

각 기능의 관계를 비교하면서 쉽게 사용할 수 있다고 생각합니다.

궁금하거나 잘못된 점을 댓글로 남겨주시면 열심히 답변 및 수정 하겠습니다.