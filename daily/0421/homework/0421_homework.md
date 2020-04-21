# 0421_homework

##### 1. 지문의 코드에서 '__gt' 부분을 lookup이라고 한다. 링크를 참고하여 Django에서 사용 가능 한 lookup 세가지와 그 의미를 작성하시오.

https://docs.djangoproject.com/en/3.0/ref/models/querysets/#field-lookups

```bash
Entry.objects.filter(id__gt=4)
```

>### Field lookup
>
>- SQL WHERE 절을 처리하기 위한 django ORM 문법
>
>- QuerySet method **filter(), exlude(), get()** 안의 키워드로 `field__lookup` 형태로 사용된다.
>
>- 한 QuerySet method 안에 여러 개의 lookup을 이어붙여 사용 가능하다.
>
>  - ```bash
>    Entry.objects.filter(pub_date__month__gte=6)
>    ```
>
>- 커스텀 lookup도 만들어 사용가능하다.
>
>- ORM문 안에 lookup이 없을 경우, `exact`가 들어가 있는 걸로 간주
>
>### 대표적인 django lookup
>
>- exact: 필드의 값이 주어진 값과 일치하는 지 평가(대소문자 구분 O)
>
>  - ```bash
>    Entry.objects.get(id__exact=14)
>    Entry.objects.get(id__exact=None) # (id__isnull=True)
>    ```
>
>- iexact: 필드의 값이 주어진 값과 일치하는 지 평가(대소문자 구분 X)
>
>- contains: 필드의 값이 주어진 값을 포함하고 있는 지 평가(대소문자 구분 O)
>
>- icontatins: 필드의 값이 주어진 값을 포함하고 있는 지 평가(대소문자 구분 X)
>
>-  in: 주어진 iterable 안에, 필드의 값이 존재하는 지 평가
>
>  - ```bash
>    Entry.objects.filter(id__in=[1, 3, 4])
>    Entry.objects.filter(headline__in='abc')
>    
>    inner_qs = Blog.objects.filter(name__contains='Cheddar')
>    entries = Entry.objects.filter(blog__in=inner_qs)
>    ```
>
>- gt: Greater than. 필드의 값이 주어진 값보다 큰 지 평가
>
>- gte: Greater than or equal to.
>
>- lt: Less than.
>
>- lte: Less than or equal to.
>
>- startswith: 필드의 값이 주어진 값으로 시작하는 지 평가(대소문자 구분 O)
>
>- istartswith: 필드의 값이 주어진 값으로 시작하는 지 평가(대소문자 구분 X)
>
>- endswith: 필드의 값이 주어진 값으로 끝나는 지 평가(대소문자 구분 O)
>
>- iendswith: 필드의 값이 주어진 값으로 끝나는 지 평가(대소문자 구분 X)
>
>- range: 필드의 값이 주어진 범위 안에 포함되는 지 평가
>
>  - SQL 문의 BETWEEN과 대응
>
>  - ```bash
>    import datetime
>    start_date = datetime.date(2005, 1, 1)
>    end_date = datetime.date(2005, 3, 31)
>    Entry.objects.filter(pub_date__range=(start_date, end_date))
>    ```
>
>- 날짜 관련
>
>  - date / year / month / day / week / week_day
>
>- 시간 관련
>
>  - time / hour / minute / second

##### 2. 지문은 1:N 관계 설정을 하기 위하여 정의된 모델이다. 링크를 참고하여 빈 칸에 들어갈 수 있는 값 세가지와 그 의미를 작성하시오.

https://docs.djangoproject.com/en/3.0/ref/models/fields/#arguments

```python
class Comment(models.Model):
    content = models.CharField(max_length=100)
    article = models.ForeignKey(Article, on_delete=__(a)__)
```

> - CASCADE
>   - 참조 대상 삭제 시, 해당하는 모델 인스턴스를 함께 삭제한다.
> - PROTECT
>   - 참조 대상 삭제 시, ProtectedError 발생 시켜 삭제를 막는다.
> - SET_NULL
>   - 참조 대상 삭제 시, 해당하는 모델 인스턴스의 ForeignKey 필드를 null로 수정한다. 이때 해당 필드는 nullable 해야한다. 
> - SET_DEFAULT
>   - 참조 대상 삭제 시, 해당하는 모델 인스턴스의 ForeignKey 필드를 미리 지정해둔 default 값으로 수정한다.
> - SET()
>   - 참조 대상 삭제 시, 해당하는 모델 인스턴스의 ForeignKey 필드를 SET에 설정된 함수 등에 통해 수정한다. 
> - DO_NOTHING
>   - 참조 대상 삭제 시, 해당 데이터의 ForeignKey 필드를 그대로 둔다. 이때 해당 DB의 참조 무결성이 훼손된다.

##### 3. 지문은 댓글 기능을 작성하기 위한 코드이다. 빈 칸에 들어갈 코드를 작성하시오.

```python
def comment_create(request, id):
    article = Article.objects.get(id=id)
    if request.method == "POST":
        form = CommentForm(request.POST)
        if form.is_valid():
            comment = form.save(__(a)__)
            comment.article = article
            comment.save()
            return redirect('articles:index')
```

> (a) : commit=False

##### 4. 게시물 아래에 댓글을 출력하려고 한다. post 와 comment 모델이 1:N 으로 관계설정이
되어 있다고 가정 할 때 아래의 빈칸에 적절한 코드를 작성하시오.

```html
<h1>{{ post.title }}</h1>
{% for comment in __(a)__ %}
	<p>{{ comment.content }}</p>
{% empty %}
	<p>댓글이 없습니다.</p>
{% endfor %}
```

> (a) : post.comment_set.all
>
> 만약 comment 모델의 참조키 설정 시 `related_name`을 'comments'로 설정했다면, (a)를 post.comments.all로 작성해도 된다.