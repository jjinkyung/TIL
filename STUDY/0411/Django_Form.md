# Django Form

- Form
- Model Form
- Rendering Fields Manually

---

> ## Form
>
> > **lntro**
>
> - HTML form, input을 통해서 사용자로부터 직접 데이터를 받으면 입력된 데이터의 유효성을 검증하고 필요시에 입력된 데이터를 검증 결과와 함께 다시 표시함 -> 사용자가 입력한 데이터가 개발자가 요구한 형식이 아닐 수도 있음
> - 이렇게 사용자가 입력한 데이터를 검증하는 것을 '유효성 검증'이라고 하는데, 이 과정을 코드로 모두 구현하는 것은 많은 노력이 필요
>
> 
>
> > **Django's forms**
>
> - Form은 Django의 유효성 검사 도구 중 하나로 외부의 악의적 공격 및 데이터 손상에 대한 중요한 방어 수단
>
> - Django는 Form과 관련한 유효성 검사를 단순화하고 자동화할 수 있는 기능을 제공하여 개발자로 하여금 직접 작성하는 코드보다 더 안전하고 빠르게 수행하는 코드를 작성할 수 있게함
>
> - Django는 form에 관련된 작업의 아래 부분을 처리해줌
>
>   1. 렌더링을 위한 데이터 준비 및 재구성
>   2. 데이터에 대한 HTML forms 생성
>   3. 클라이언트로부터 받은 데이터 수신 및 처리
>
>   
>
> > **Form 선언**
>
> ```python
> # articles/forms.py
> from django import forms
> 
> class ArticleForm(forms.Form):
> 	title = forms.CharField(max_length=10)
> 	content = forms.Charfield()
> ```
>
> - forms 라이브러리에서 파생된 Form 클래스를 상속받음
>
> 
>
> > **Form 사용**
>
> ```python
> # articles/views.py
> from .forms import ArticleForm
> 
> def new(request):
> 	form = ArticleForm
> 	context = {
> 		'form' : form,
> 	}
> 	return render(request, 'articles/new.html', context)
> ```
>
> ```html
> # new.html
> {% extends 'base.html' %}
> 
> {% block content %}
>   <h1>NEW</h1>
>   <form action="{% url 'articles:create' %}" method="POST">
>     {% csrf_token %}
>     {{ form.as_p }}
>     <input type="submit">
>   </form>
>   <hr>
>   <a href="{% url 'articles:index' %}">BACK</a>
> {% endblock content %}
> ```
>
> 
>
> > **Form rendering options**
>
> - <label> & <input> 쌍에 대한 3가지 출력 옵션
>
>   1. **as_p()** - 각 필드가 단락(<p> 태그)으로 감싸져서 렌더링 됨
>   2. **as_ul()** - 각 필드가 목록 항목(<li> 태그)으로 감싸져서 렌더링 됨
>   3. **as_table()** - 각 필드가 테이블(<tr> 태그)으로 감싸져서 렌더링 됨
>
>   
>
> > **Form fields & Widgets**
>
> - Form field는 input 유효성 검사를 처리
> -  Widgets은 웹페이지에서 input element의 단순 raw한 렌더링 처리



> ## ModelForm
>
> > **Intro**
>
> - form을 사용하다 보면 Model에 정의한 필드를 유저로부터 입력받기 위해 Form에서 Model 필드를 재정의하는 행위가 중복될 수 있음
>
> 
>
> > **ModelForm 선언**
>
> ```python
> # articles/forms.py
> from django import forms
> from .models import Article
> 
> 
> class ArticleForm(forms.ModelForm):
>     class Meta:
>         model = Article
>         fields = '__all__'
>         # exclude = ('title',)  # title만 빼고 나머지 모두
> ```
>
> - forms 라이브러리에서 파생된 ModelForm 클래스를 상속받음
> - 정의한 클래스 안에 Meta 클래스를 선언하고 어떤 모델을 기반으로 Form을 작성할 것인지에 대한 정보를 Meta 클래스에 지정
>
> ```python
> # articles/views.py
> def create(request):
>     form = ArticleForm(request.POST)
>         if form.is_valid():
>             article = form.save()
>             return redirect('articles:detail', article.pk)
>     	return redirect('articles:new')
> ```
>
> - **is_valid() method**
>   - 유효성 검사를 실행하고, 데이터가 유효한지 여부를 boolean으로 반환
>   - **유효성 검사** : 데이터베이스 각 필드 조건에 올바르지 않은 데이터가 서버로 전송되거나 저장되지 않도록 하는 것
>
> > **함수 구조 변경**
>
> **CREATE**
>
> ```python
> # articles/views.py
> def create(request):
>     if request.method == 'POST':
>         form = ArticleForm(request.POST)
>         if form.is_valid():
>             article = form.save()
>             return redirect('articles:detail', article.pk)
> 
>     else:
>         form = ArticleForm()
>     context = {
>         'form':form,
>     }
>     return render(request, 'articles/create.html', context)
> ```
>
> ```html
> # create.html
> {% extends 'base.html' %}
> 
> {% block content %}
>   <h1>CREATE</h1>
>   <form action="{% url 'articles:create' %}" method="POST">
>     {% csrf_token %}
>     {{ form.as_p }}
>     <input type="submit" value="CREATE">
>   </form>
>   <hr>
>   <a href="{% url 'articles:index' %}">BACK</a>
> {% endblock content %}
> ```
>
> - new.html -> create.html 이름 변경/ 이제는 action 값이 없어도 동작
>
> ```html
> # index.html
> {% extends 'base.html' %}
> {% block content %}
> <h1>Articles</h1>
> <a href="{% url 'articles:create' %}">CREATE</a>
> <hr>
> {% csrf_token %}
> {% for article in articles %}
>   <p>글 번호: {{ article.pk }}</p>
>   <p>글 제목: {{ article.title }}</p>
>   <p>글 내용: {{ article.content }}</p>
>   <a href="{% url 'articles:detail' article.pk %}">DETAIL</a>
>   <hr>
> {% endfor %}
> {% endblock content %}
> ```
>
> - input 태그에 공백 데이터를 넣고 글 작성하면 에러 메세지 출력
>
> 
>
> **DELETE**
>
> ```python
> # views.py
> def delete(request, pk):
>   article = Article.objects.get(pk=pk)
>   if request.method == 'POST':
>     article.delete()
>     return redirect('articles:index')
>   return redirect('articles:detail', article.pk)
> ```
>
> ```html
> # detail.html
> <form action="{% url 'articles:delete' article.pk %}" method="POST">
>   {% csrf_token %}
>   <input type="submit" value="DELETE">
> </form>
> ```
>
> 
>
> **UPDATE**
>
> ```python
> # articles/views.py
> def update(request, pk):
>   article = Article.objects.get(pk=pk)
>   if request.method == 'POST':
>     form = ArticleForm(request.POST, instance=article)
>     if form.is_valid():
>       form.save()
>       return redirect('articles:detail', article.pk)
>   else:
>     form = ArticleForm(instance=article)
>   context = {
>     'form' : form,
>     'article' : article,
>   }
>   return render(request, 'articles/update.html', context)
> ```
>
> ```html
> # update.html
> {% extends 'base.html' %}
> 
> {% block content %}
>   <h1>UPDATE</h1>
>   <form action="{% url 'articles:update' article.pk %}" method="POST">
>     {% csrf_token %}
>     {{ form.as_p }}
>     <input type="submit" value="UPDATE">
>   </form>
>   <a href="{% url 'articles:detail' article.pk %}">BACK</a>
> {% endblock content %}
> ```
>
> - edit.html -> update.html 파일명 변경
>
> 
>
> > **Form & ModelForm 비교**
>
> - **Form**
>   - 어떤 Model에 저장해야 하는지 알 수 없으므로 유효성 검사 이후 cleaned_data 딕셔너리를 생성
>   - cleaned_data 딕셔너리에서 데이터를 가져온 후 .save() 호출해야 함
>   - Model에 연관되지 않은 데이터를 받을 때 사용
> - **ModelForm**
>   - Django가 해당 model에서 양식에 필요한 대부분의 정보를 이미 정의
>   - 어떤 레코드를 만들어야 할지 알고 있으므로 바로 .save() 호출 가능



> ## Rendering Fields Manually
>
> 