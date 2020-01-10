# My_Code_Conventions

### - Naming

 #### 1.	**파일명**
   * 각 단어의 첫 글자를 대문자를 사용합니다
   *	파일은 *“.h”* 와 *“.cpp”*를 한쌍으로 이루는 것을 기본으로 합니다.
   *	인터페이스만을 구현한 파일이라면 *“.h”*만을 사용합니다.
   *	Template 관련 파일이라면 *“.h”*와 *“.hpp”*로 분리하는 것으로 합니다.

 #### 2.	**#define, const, constexpr**
 *	대문자와 밑줄만을 사용합니다.
>   +	`#define MAX_USER 10`
>   +	`const int WAIT_TIME = 100;`
>   +	`constexpr int MAX_THREAD = 16;`

 #### 3.	**typedef, using**
 *	밑줄없이 대문자만을 사용합니다.
>   +	`Typedef std::function<void(void*)> THREADFUNC;`
>   +	`Using SESSIONPOOL = std::unordered_map<void*, MAX_SESSION>;`

 #### 4.	**namespace**
 *	시작을 대문자로 단어별 첫 글자를 대문자를 사용합니다.
>   +	`namespace Network { … }`

 #### 5.	**enum, enum class**
 *	앞에 대문자 ***E***로 시작하며 단어 별로 첫 문자를 대문자로 사용합니다.
>   +	`enum ESessionStatus { … };`
>   +	`enum class EContextType { … }`
 *	내부 네이밍은 대문자를 사용하며 끝에 언더바를 붙입니다.
>   +	`{ LOGIN_, … } `

 #### 6.	함수
 *	각 단어의 첫 글자를 대문자를 사용하며, 기능을 최대한 나타내도록 표현합니다.
>   +	`Point* GetSessionStatus( … );`
 *	*Get*, *Set*이름의 함수를 사용하며 리턴값이 bool일경우에는 *Is*를 붙입니다.
 *	**static** 함수의 경우, 언더바로 시작합니다.
>   + `static const bool _SetNetwork();`

 #### 7.	변수
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

 #### 8.	class, struct
 *	**class** 앞에는 대문자 ***C***를 붙이며, 각 단어의 첫 글자를 대문자로 사용합니다.
>   +	`CSession { … };`
 *	**Struct** 앞에는 대문자 ***ST***를 붙이며, 각 단어의 첫 글자를 대문자로 사용하며, typedef로 ST를 붙이지 않은 이름을 붙여줍니다.
>   +	`typedef STIOContext { … } IOContext;`
