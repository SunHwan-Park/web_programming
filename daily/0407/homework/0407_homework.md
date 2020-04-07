# 0407_homework

### 아래 코드들을 참고하여 각 문항에 답하시오.

```python
# models.py
class Reservation(models.Model):
    name = models.CharField(max_length=10)
    date = models.DateField()
```

1. 모델폼을 정의하기 위해 빈칸에 들어갈 코드를 작성하시오.

   ```python
   from django import forms
   from .models import Reservation
   
   class ReservationForm(__(a)__):
       class __(b)__:
           model = Reservation
           fields = '__all__'
   ```

   > (a) : ModelForm
   >
   > (b) : Meta

2. 글 작성 기능을 구현하기 위해 다음과 같이 코드를 작성하였다. 서버를 실행시킨 후 기능을 테스트 해보니 특정 상황에서 문제가 발생하였다. 이유와 해결방법을 작성하시오.

   ```python
   def create(request):
       if request.method == 'POST':
           form = ReservationForm(request.POST)
           if form.is_valid():
               article = form.save()
               return redirect('reservations:detail', reservation.id)
       else:
           form = ReservationForm()
           context = {
               'form': form,
           }
           return render(request, 'reservations/create.html', context)
   ```

   > 잘못된 양식으로 글쓰기 작성을 '제출' 했을 경우, 즉 `form.is_valid()` 값이 False일 경우, 함수 `create`에서 return 되는 값이 없어 오류가 발생한다.
   >
   > 
   >
   > ```python
   > context = {
   >     'form': form,
   > }
   > return render(request, 'reservations/create.html', context)
   > ```
   >
   > 위에 있는 파트의 들여쓰기를 한 칸(4 spaces) 밖으로 풀어주면, 문제가 해결된다. 

3. 글 수정 기능을 구현하기 위해 빈칸에 들어갈 코드를 작성하시오.

   ```python
   def update(request, pk):
       reservation = Reservation.objects.get(id=id)
       if request.method == 'POST':
           __(a)__
           if form.is_valid():
               reservation = form.save()
               return redirect('reservations:detail', reservation.id)
       else:
           __(b)__
       context = {
           'reservation':reservation,
           'form':form,
       }
       return render(request, 'reservations/update.html', context)
   ```

   > (a) : form = ReservationForm(request.POST, instance=reservation)
   >
   > (b) : form = ReservationForm(instance=reservation)

4. 글 수정 기능을 구현하기 위해 빈칸에 들어갈 수 있는 코드를 모두 작성하시오.

   ```html
   <h2>Edit</h2>
   <form action="{% url 'reservation:update' reservation.id %}" method="POST">
       {% csrf_token %}
       {{ form.__(a)__ }}
       <input type="submit" value="submit">
   </form>
   ```

   > - as_p
   > - as_ul
   > - as_table