# 0406_homework

### 아래 코드들을 참고하여 각 문항에 답하시오.

```python
# reservations/urls.py
from django.urls import path
from . import views

app_name = 'reservations'
urlpatterns = [
    path('', views.index, name="index"),
    path('<int:id>/edit/', views.edit, name="edit"),
    path('<int:id>/update/', views.update, name="update"),
    path('<int:reservation_id>/delete/', views.delete, name="delete"),
]
```

```python
# models.py
class Reservation(models.Model):
    name = models.CharField(max_Length=10)
    date = models.DateField()
```

```python
# views.py
def edit(request, id):
    reservation = Reservation.objects.get(id=id)
    context = {
        'reservation': reservation,
    }
    return render(request, 'reservations/edit.html', context)
```

1. 수정기능을 구현하기 위해 빈 칸에 들어갈 코드를 작성하시오.

   ```html
   <!-- edit.html -->
   <h1>EDIT</h1>
   <form action="__(a)__" method="POST">
       __(b)__
       <input type="text" name="name" __(c)__>
       <input type="date" name="date" __(d)__>
       <input type="submit">
   </form>
   ```

   > - (a) : {% url 'reservations:update' reservation.id %}
   > - (b) : {% csrf_token %}
   > - (c) :  value="{{ reservation.name }}"
   > - (d) :  value="{{ reservation.date }}"

2. 삭제 버튼을 생성하기 위해 빈칸에 들어갈 코드를 작성하시오.

   ```html
   <a href="{% url '__(a)__' reservation.id %}"></a>
   ```

   > - (a) : reservations:delete

3. 삭제 기능을 구현하기 위해 빈칸에 들어갈 코드를 작성하시오.
   단, 삭제가 완료되면 index 페이지로 이동해야 한다.

   ```python
   def delete(request, __(a)__):
       reservation = Reservation.objects.get(id=__(a)__)
       reservation.__(b)__()
       return redirect('__(c)__')
   ```

   > (a) : reservation_id
   >
   > (b) : delete
   >
   > (c) : reservations:index

4. form 태그의 method 속성은 GET과 POST 속성값을 가질 수 있다.
   이 때, 두 값을 비교하여 서술하시오.

   > - GET
   >   - 서버로부터 정보를 조회하기 위해 설계된 메소드이다.
   >   - 특정 리소스의 표시를 요청한다.
   >   - 요청을 전송할 때 필요한 데이터를 쿼리스트링(URL 끝에 ?와 함께 이름과 값으로 쌍을 이루는 요청 파라미터)을 통해 전송한다.
   >   - 이때 전송할 수 있는 요청 URL은 길이가 제한된다.
   >   - 링크를 통해 특정 페이지로 바로 이동이 가능하다.(URL에 파라미터가 있기 때문)
   >   - Idempotent
   >     - 서버에게 동일한 요청을 여러 번 전송하더라도, 동일한 응답이 돌아온다.
   > - POST
   >   - 리소스를 생성/변경하기 위해 설계된 메소드이다.
   >   - 특정 리소스에 인티티를 제출할 때 쓰인다. 서버의 변화나 부작용을 일으킨다.
   >   - 요청을 전송할 때 필요한 데이터를 HTTP 메시지의 Body에 담아 전송한다.
   >     (길이의 제한없이 데이터를 전송할 수 있다. 즉, 대용량 데이터를 전송 가능하다.)
   >   - 링크를 통해 특정 페이지로 바로 이동이 불가능하다.(Body에 파라미터가 있기 때문)
   >   - Non-idempotent
   >     - 서버에게 동일한 요청을 여러 번 전송하면, 응답은 서로 다를 수 있다.