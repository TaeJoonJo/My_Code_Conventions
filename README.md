# My_Code_Conventions


### - Naming

 ####	**파일명**
   * 각 단어의 첫 글자를 대문자를 사용합니다
   *	파일은 *“.h”* 와 *“.cpp”*를 한쌍으로 이루는 것을 기본으로 합니다.
   *	인터페이스만을 구현한 파일이라면 *“.h”*만을 사용합니다.
   *	Template 관련 파일이라면 *“.h”*와 *“.hpp”*로 분리하는 것으로 합니다.

 ####	**#define, const, constexpr**
 *	대문자와 밑줄만을 사용합니다.
>   +	`#define MAX_USER 10`
>   +	`const int WAIT_TIME = 100;`
>   +	`constexpr int MAX_THREAD = 16;`

 ####	**typedef, using**
 *	밑줄없이 대문자만을 사용합니다.
>   +	`Typedef std::function<void(void*)> THREADFUNC;`
>   +	`Using SESSIONPOOL = std::unordered_map<void*, MAX_SESSION>;`

 ####	**namespace**
 *	시작을 대문자로 단어별 첫 글자를 대문자를 사용합니다.
>   +	`namespace Network { … }`

 ####	**enum, enum class**
 *	앞에 대문자 ***E***로 시작하며 단어 별로 첫 문자를 대문자로 사용합니다.
>   +	`enum ESessionStatus { … };`
>   +	`enum class EContextType { … }`
 *	내부 네이밍은 대문자를 사용하며 끝에 언더바를 붙입니다.
>   +	`{ LOGIN_, … } `

 ####	
 *	각 단어의 첫 글자를 대문자를 사용하며, 기능을 최대한 나타내도록 표현합니다.
>   +	`Point* GetSessionStatus( … );`
 *	*Get*, *Set*이름의 함수를 사용하며 리턴값이 bool일경우에는 *Is*를 붙입니다.
 *	**static** 함수의 경우, 언더바로 시작합니다.
>   + `static const bool _SetNetwork();`

 ####	변수
 *	각 단어의 첫글자를 대문자로 사용하며 뒤에 언더바를 붙이며, 기능을 최대한 나타내도록 표현합니다.
>   +	`wchar_t PlayerName_[MAX_STR];`
 *	**포인터**의 경우 *p*, **레퍼런스**의 경우 *r*, **bool**일 경우 *is*를 앞에 붙이며, 이는 소문자를 사용합니다.
>   +	`CSession* pNowAggroSession;`
>   +	`CMutexLock& rMutex;`
>   +	`bool isRun;`
 *	**지역변수**의 경우 맨앞 단어를 소문자로 사용합니다.
>   +	`Point* GetSessionStatus(CSession* psession) {bint sessionID = psession->GetID(); … }`
 *	**static** 변수일 경우 앞에 언더바를 붙여 사용합니다.
>   +	`static unsigned Int _SessionID;`

 ####	class, struct
 *	**class** 앞에는 대문자 ***C***를 붙이며, 각 단어의 첫 글자를 대문자로 사용합니다.
>   +	`CSession { … };`
 *	**Struct** 앞에는 대문자 ***ST***를 붙이며, 각 단어의 첫 글자를 대문자로 사용하며, typedef로 ST를 붙이지 않은 이름을 붙여줍니다.
>   +	`typedef STIOContext { … } IOContext;`


### - 중괄호, 개행

#### class, struct, namespace, enum, enum class
* 개행하지 않고 선언합니다.
```c
class CSession {
protected:
  CSession();
  virtual ~CSession();
  ...
}

typedef struct STIOContext {
...
} IOContext;

namespace Network {
...
}

enum class ESessionStatus {
...
}
```
 + 다만 상속받는 경우, 개행 해줍니다.
 ```c
 class CSession
   : public CSingleton<CSession>
 {
   ...
 }
 ```
 
#### 함수
* 개행해준후 정의합니다.
```c
void SetSessionStatus(CSession* psession, const ESessionStatus sessionStatus)
{
  ...
}
```
 + 다만 **inline** 함수일 경우 중괄호전에 개행해주지 않습니다.
 ```c
 inline std::string GetSessionName() {
   return SessionName_;
 }
 ```

#### if, else if, else, while, for
* 중괄호전에 개행하지 않습니다.
```c
int sessionHP = psession->GetHP();
if( 0 < sessionHP ) {
  ...
}
else if ( 0 == sessionHP ) {
  ...
}
else {
 ...
}

for(int i = 0; i < MAX_SESSION; ++i) {
  ...
}

while( nullptr != psession) {
  ...
}
```
* 조건문 뒤에 오는 실행문이 한 문장이라도 중괄호와 개행을 해줍니다.
```c
int sessionNum = pServerManager_->GetSessionNum();
if( 0 < sessionNum ) {
  pLogManager->Log("Current Session Num : %d", sessionNum);
}
```

#### Lock
* Lock을 수행하는 부분은 Lock을 호출한 후 개행한 후 중괄호를 사용합니다.
```c
MutexLock_.Lock();
{
  ...
}
MutexLock_.UnLock();
```

#### switch
* 개행하지 않고 사용하며, case 문에서는 개행한 후에 중괄호를 사용합니다.
* 반드시 break와 default를 명시해줍니다.
```c
switch( eioType ) {
case EIOType::RECV_:
{
  ...
} break;
case EIOType::SEND_:
{
  ...
} break;
default:
{
  pLogManager_->Log(...);
} break;
}
```

#### 초기화리스트
* 변수별 타입에 따라 개행해줍니다.
```c
CSession()
 : SessionInt1_(0), SessionInt2_(0)
 , SessionFloat1_(0.f), SessionFloat2_(0.f)
 , ...
 {
   ...
 }
```

#### define
* 한 문장일 경우 개행하지 않고, 한 문장을 넘어갈 경우 #을 사용해서 개행해줍니다.
```c
#define _LOG(str) _pLogManager->_Log(str, ELogType::INFO_);

#define _LOG(str, ...) std::string logString = _pLogManager->_AssembleString(str, ...);#
                       _pLogManager->_Log(logString, ELogType::INFO_);#
                       ...
```              


### - 순서

#### Header
* Header.h는 아래의 순서를 따릅니다.
```c
#ifndef ...
#define ...

#include ...

#define ...
constexpr ...
const ...

struct ...

class ...

class CHeader {
  ...
}

#endif ...
#define "....hpp" // if template
```

#### Source
* Source.cpp는 아래의 순서를 따릅니다.

```c

#include "Source.h"
#include ...

CSource::CSource()
  : ...
{
  ...
}

...
```

#### include
* include 순서는 아래의 순서를 따릅니다.
```c
#include "표준라이브러리를 포함한 사용자 정의 헤더"
#include <표준라이브러리 헤더>
#include "사용자 정의 헤더"
```
* 다만 *.cpp* 는 아래의 순서를 따릅니다.
```c
#include "자신을 선언한 헤더"
#include "표준라이브러리를 포함한 사용자 정의 헤더"
#include <표준라이브러리 헤더>
#include "사용자 정의 헤더"
```

#### class
* Session이라는 class 정의는 아래의 순서를 따릅니다.
```c
class CSession
  : public CSessionData
{
  public:
  생성자
  소멸자
  private:
   const ...
   class ... {
   }
   struct ... {
   }
  private:
   private 함수
  public:
   public 함수
  private:
   private 변수
  public:
   public 변수
}
```

#### 조건문
* 조건문을 작성할때 상수를 먼저오게 사용합니다.
```c
if( 0 < sessionNum) {
  ...
}
```
* !=보다 == 을 지향합니다.
```c
if( false == psession->IsRun() ) {
  ...
}
```
