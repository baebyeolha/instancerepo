# instancerepo
인스턴스와 아키텍처에 따른 실행 시간 차이

## 실행 코드

    import requests
    from bs4 import BeautifulSoup

    def get_username_and_email(url):
        response = requests.get(url)
        soup = BeautifulSoup(response.text, 'html.parser')

        # 사용자 이름이 포함된 HTML 요소를 찾습니다.
        username = soup.find('h1').text

        # 이메일 주소가 포함된 HTML 요소를 찾습니다.
        email_tag = soup.find('a', href=lambda x: x and x.startswith('mailto:'))    if email_tag:
            email = email_tag['href'].replace('mailto:', '')
        else:
            email = '이메일 주소를 찾을 수 없습니다.'

    return username, email


    url = 'https://baebyeolha.github.io/baebyeolha/'
    username, email = get_username_and_email(url)
    print(f'Username: {username}')
    print(f'Email: {email}')
    print ('\n')

    url1 = 'https://eunxoo.github.io/eunxoo/'
    username1, email1 = get_username_and_email(url1)
    print(f'Username: {username1}')
    print(f'Email: {email1}')
    print ('\n')

    url2 = 'https://seo-yj.github.io/SEO-YJ/'
    username2, email2 = get_username_and_email(url2)
    print(f'Username: {username2}')
    print(f'Email: {email2}')
    print ('\n')


    url3 = 'https://tomk2d.github.io/Tomk2d/'
    username3, email3 = get_username_and_email(url3)
    print(f'Username: {username3}')
    print(f'Email: {email3}')



    import math
    import time

    start = time.time()
    math.factorial(100000)
    end = time.time()

    print(f"{end - start:.5f} sec")


## 결과

t2 small<br>
<img src="./img/t2small.png" width="400" height="300"/>
<br>
t3 small<br>
<img src="./img/t3small.png" width="400" height="300"/>
<br>
t3a small<br>
<img src="./img/t3asmall.png" width="400" height="300"/>
<br>
t4g small<br>
<img src="./img/t4gsmall.png" width="400" height="300"/>
<br>

t2 micro<br>
<img src="./img/t2micro.png" width="400" height="300"/>
<br>
t3 micro<br>
<img src="./img/t3micro.png" width="400" height="300"/>
<br>
t3a micro<br>
<img src="./img/t3amicro.png" width="400" height="300"/>
<br>
t4g micro<br>
<img src="./img/t4gmicro.png" width="400" height="300"/>


<img src="./1.png" width="200" height="400"/>

## 결과 분석

### 아키텍처 차이

처음에는 인스턴스로 실행속도를 비교하려 했으나 변경되지 않는 인스턴스가 있어 왜 그런지 생각해보았다<br>

<img src="./failx.png" width="400" height="50"/>
<img src="./failarm.png" width="400" height="50"/>

T3 인스턴스는 인텔 x86아키텍처, t3a 인스턴스는 AMD x86 아키텍처, T4g 인스턴스는 AWS Graviton의 프로세서로 <br>
아키텍처를 x86으로 설정했을 땐 t4g를 사용할 수 없고, arm으로 설정하면 t2,t3,t3a를 사용할 수 없었다

- micro<br>
<img src="./t3micro.png" width="400" height="50"/>
<img src="./t4gmicro.png" width="400" height="50"/>

- small<br>
<img src="./t3small.png" width="400" height="50"/>
<img src="./t4gsmall.png" width="400" height="50"/>

small의 vCPU는 2, 메모리는 2GiB로 , micro의 vCPU는 2, 메모리는 1GiB로 버전별로 동일하다 <br>
하지만 x86에서 t2,t3,t3a 인스턴스 코드 실행 시간이 arm에서 t4g 인스턴스 코드 실행 시간보다 빠른 것을 알 수 있다<br>


### 인스턴스 차이

<img src="./t3smallt.png" width="400" height="300"/>
<img src="./t3nano.png" width="400" height="300"/>

- 위의 표를 보면 micro와 small의 차이는 별로 없었다
- 오늘 small과 nano를 비교해보니 nano가 small보다 느린 것을 알 수 있다
- nano와 small의 vCPU는 동일하지만 메모리가 4배 작아 속도 차이가 나는 것 같다



