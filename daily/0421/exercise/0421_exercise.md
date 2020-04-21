# 0421_exercise

### 주어진 정보를 활용하여 작성된 SQL문과 대응하는 ORM문을 작성하고 실행하시오.

#### Table Name : users

|    name    |  data type  |
| :--------: | :---------: |
|     id     | integer(pk) |
| first_name |    text     |
| last_name  |    text     |
|    age     |   integer   |
|  country   |    text     |
|   phone    |    text     |
|  balance   |   integer   |

1. user 테이블 전체 데이터를 조회하시오.

   ```sql
   SELECT * FROM users_user;
   ```

   ```bash
   User.objects.all()
   
   #<QuerySet [<User: User object (1)>, <User: User object (2)>, <User: User object (3)>, <User: User object (4)>, <User: User object (5)>, <User: User object (6)>, <User: User object (7)>, <User: User object (8)>, <User: User object (9)>, <User: User object (10)>, <User: User object (11)>, <User: User object (12)>, <User: User object (13)>, <User: User object (14)>, <User: User object (15)>, <User: User object (16)>, <User: User object (17)>, <User: User object (18)>, <User: User object (19)>, <User: User object (20)>, '...(remaining elements truncated)...']>
   ```

2. id가 19인 사람의 age를 조회하시오

   ```sql
   SELECT age FROM users_user WHERE id = 19;
   ```

   ```bash
   User.objects.get(id=19).age
   
   # 26
   ```

3. 모든 사람의 age를 조회하시오.

   ```sql
   SELECT age FROM users_user;
   ```

   ```bash
   User.objects.all().values('age')
   
   #<QuerySet [{'age': 40}, {'age': 36}, {'age': 37}, {'age': 40}, {'age': 30}, {'age': 26}, {'age': 18}, {'age': 33}, {'age': 23}, {'age': 22}, {'age': 15}, {'age': 22}, {'age': 32}, {'age': 35}, {'age': 24}, {'age': 19}, {'age': 34}, {'age': 17}, {'age': 26}, {'age': 17}, '...(remaining elements truncated)...']>
   ```

4. age가 40 이하인 사람들의 id와 balance를 조회하시오.

   ```sql
   SELECT id, balance FROM users_user
   WHERE age <= 40;
   ```

   ```bash
   User.objects.filter(age__lte=40).values('id', 'balance')
   
   #<QuerySet [{'id': 1, 'balance': 370}, {'id': 2, 'balance': 5900}, {'id': 3, 'balance': 3100}, {'id': 4, 'balance': 250000}, {'id': 5, 'balance': 220}, {'id': 6, 'balance': 530}, {'id': 7, 'balance': 390}, {'id': 8, 'balance': 3700}, {'id': 9, 'balance': 43000}, {'id': 10, 'balance': 49000}, {'id': 11, 'balance': 640000}, {'id': 12, 'balance': 52000}, {'id': 13, 'balance': 35000}, {'id': 14, 'balance': 720}, {'id': 15, 'balance': 35000}, {'id': 16, 'balance': 720}, {'id': 17, 'balance': 440}, {'id': 18, 'balance': 94000}, {'id': 19, 'balance': 6100}, {'id': 20, 'balance': 590}, '...(remaining elements truncated)...']>
   ```

5. last_name이 '김'이고 balance가 500 이상인 사람들의 first_name을 조회하시오.

   ```sql
   SELECT first_name FROM users_user
   WHERE last_name = '김' AND balance >= 500;
   ```

   ```bash
   User.objects.filter(last_name='김', balance__gte=500).values('first_name')
   
   #<QuerySet [{'first_name': '예진'}, {'first_name': '서현'}, {'first_name': '서영'}, {'first_name': '영일'}, {'first_name': '옥자'}, {'first_name': '광수'}, {'first_name': '성민'}, {'first_name': '정수'}, {'first_name': '서준'}, {'first_name': '은주'}, {'first_name': '미영'}, {'first_name': '우진'}, {'first_name': '순옥'}, {'first_name': '진우'}, {'first_name': '현지'}, {'first_name': '영호'}, {'first_name': '종수'}, {'first_name': '미숙'}, {'first_name': '민재'}, {'first_name': '경자'}]>
   ```

6. first_name이 '수'로 끝나면서 행정구역이 경기도인 사람들의 balance를 조회하시오.

   ```sql
   SELECT balance FROM users_user
   WHERE first_name LIKE '%수' AND country = '경기도';
   ```

   ```bash
   User.objects.filter(first_name__endswith='수', country='경기도').values('balance')
   
   #<QuerySet [{'balance': 590}, {'balance': 370}]>
   ```

7. balance가 2000 이상이거나 age가 40 이하인 사람의 총 인원수를 구하시오.

   ```sql
   SELECT COUNT(*) FROM users_user
   WHERE balance >= 2000 OR age <= 40;
   ```

   ```bash
   User.objects.filter(Q(balance__gte=2000)|Q(age__lte=40)).count()
   
   # 또 다른 방법(QuerySet을 하나의 set 처럼 활용)
   users1 = User.objects.filter(balance__gte=2000)
   users2 = User.objects.filter(age__lte=40)
   users = users1 | users2 # 합집합
   users.count()
   
   #100
   ```

8. phone 앞자리가 '010'으로 시작하는 사람의 총원을 구하시오.

   ```sql
   SELECT COUNT(*) FROM users_user
   WHERE phone LIKE '010%';
   ```

   ```bash
   User.objects.filter(phone__startswith='010').count()
   
   #21
   ```

9. 이름이 ‘김옥자’인 사람의 행정구역을 경기도로 수정하시오.

   ```sql
   UPDATE users_user SET country = '경기도'
   WHERE fist_name = '옥자' AND last_name = '김';
   
   SELECT country FROM users_user
   WHERE first_name = '옥자' AND last_name = '김';
   ```

   ```bash
   # 1.update 사용
   # update와 delete는 개별객체 & 쿼리셋 모두에 적용 가능하다.
   User.objects.filter(first_name='옥자', last_name='김').update(country='경기도')
   
   # 2.for문 사용
   okjakims = User.objects.filter(first_name='옥자', last_name='김')
   for okjakim in okjakims:
   	okjakim.country = '경기도'
   	okjakim.save()
   	
   User.objects.filter(first_name='옥자', last_name='김').values('country')
   #<QuerySet [{'country': '경기도'}]>
   ```

10. 이름이 ‘백진호’인 사람을 삭제하시오.

    ```sql
    DELETE FROM users_user
    WHERE first_name = '진호' AND last_name = '백';
    
    SELECT * FROM users_user
    WHERE first_name = '진호' AND last_name = '백';
    ```

    ```bash
    User.objects.filter(first_name='진호', last_name='백').delete()
    
    User.objects.filter(first_name='진호', last_name='백')
    #<QuerySet []>
    ```

11. balance를 기준으로 상위 4명의 first_name, last_name, balance를 조회하시오.

    ```sql
    SELECT first_name, last_name, balance FROM users_user
    ORDER BY balance DESC
    LIMIT 4;
    ```

    ```bash
    User.objects.order_by('-balance')[:4].values('first_name', 'last_name', 'balance')
    #User.objects.order_by('-balance').values('first_name', 'last_name', 'balance')[:4] 도 가능
    
    #<QuerySet [{'first_name': '순옥', 'last_name': '김', 'balance': 1000000}, {'first_name': '은주', 'last_name': '김', 'balance': 950000}, {'first_name': '미경', 'last_name': '이', 'balance': 890000}, {'first_name': '동현', 'last_name': '이', 'balance': 790000}]>
    ```

12. phone에 ‘123’을 포함하고 age가 30미만인 정보를 조회하시오.

    ```sql
    SELECT * FROM users_user
    WHERE phone LIKE '%123%' AND age < 30;
    ```

    ```bash
    User.objects.filter(phone__contains='123', age__lt=30)
    
    #<QuerySet [<User: User object (93)>]>
    ```

13. phone이 ‘010’으로 시작하는 사람들의 행정 구역을 중복 없이 조회하시오.

    ```sql
    SELECT DISTINC country FROM users_user
    WHERE phone LIKE '010%';
    ```

    ```bash
    User.objects.filter(phone__startswith='010').values('country').distinct()
    
    #<QuerySet [{'country': '충청북도'}, {'country': '경상북도'}, {'country': '경기도'}, {'country': '제주특별자치도'}, {'country': '경상남도'}, {'country': '전라남 도'}, {'country': '강원도'}, {'country': '전라북도'}]>
    ```

14. 모든 인원의 평균 age를 구하시오.

    ```sql
    SELECT AVG(age) FROM users_user;
    ```

    ```bash
    User.objects.all().aggregate(Avg('age'))
    #User.objects.aggregate(Avg('age')) 도 가능
    
    #{'age__avg': 28.343434343434343}
    ```

15. 박씨의 평균 balance를 구하시오.

    ```sql
    SELECT AVG(balance) FROM users_user
    WHERE last_name = '박';
    ```

    ```bash
    User.objects.filter(last_name='박').aggregate(Avg('balance'))
    
    #{'balance__avg': 196114.2857142857}
    ```

16. 경상북도에 사는 사람 중 가장 많은 balance의 액수를 구하시오.

    ```sql
    SELECT MAX(balance) FROM users_user
    WHERE country = '경상북도';
    ```

    ```bash
    User.objects.filter(country='경상북도').aggregate(Max('balance'))
    
    #{'balance__max': 400000}
    
    # 또 다른 방법
    User.objects.filter(country='경상북도').order_by('-balance')[0].balance
    #400000
    ```

17. 제주특별자치도에 사는 사람 중 balance가 가장 많은 사람의 first_name을 구하시오.

    ```sql
    SELECT first_name FROM users_user
    WHERE country = '제주특별자치도'
    ORDER BY balance DESC
    LIMIT 1;
    ```

    ```bash
    User.objects.filter(country='제주특별자치도').order_by('-balance')[0].first_name
    #User.objects.filter(country='제주특별자치도').order_by('-balance').first().first_name 도 가능!
    
    #'순옥'
    ```