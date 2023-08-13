# Class Base View
- They provide a more organized and reusable way to handle different types of HTTP requests and responses. 
- Class-based views encapsulate the logic for rendering content, processing forms, handling different HTTP methods, and more, within specific class methods.

# 1. Based View

1. View
2. TemplateView
3. RedirectView

## 1. View
- manage request methods
```py
import : django.views.generic.base.View

- Attributes :
http_method_names = 'get','post','put','patch','delete','options','trace'
 
example:
# urls.py
path('home/',MyViewTest.as_view(),name='home')

from django.views import View
class MyViewTest(View):
    # if request method is GET 
    def get(self,request):
        get method logic .....
        return render (request,'home.html')

```


## 2. TemplateView
- manage templates 
```py
from django.views.generic,base import TemplateView
class MyViewTest(TemplateView):
    template_name = "Homepage.html"

    def get_context_data(self,**kwargs):
        context = super().get_context_data(**kwargs)# if need perent class context
        context['name']= "Jay"
        # or
        context = {"name":"jaypatel"}
        return context

```

## 3. RedirectView


```py
path('home/<int:id>/',MyViewTest.as_view(url='/'),name='home')
# or
class MyViewTest(TemplateView):
    url = "home/"
    def get_redirect_url(self,*args,**kargs):
        my_id = kargs['id']
        return super().get_redirect_url(*args,**kargs)
```


# 2. Generic View 

1. Display View
    - ListView (all Data fetch and return in template )
    - DetailView (get only one data using ID)
2. Editing View
    - FormView (pass the form)
    - CreateView (CreateData)
    - UpdateView (Update data)
    - DeleteView (Delete data)


## 1. Display View 
### 1. ListView
- get all data 
- filter and all 
- ex. Model.objects.all()
- ex. Model.objects.filter(name="name")
```py
from django.views.generic.list import ListView
from .models import TestModel
class TestView(ListView):
    model = TestModel

    # default
    # testmodel_list (context_name)
    # testmodel_list.html (template name )

    # Custom d
    template_name ="home.html"
    context_object_name ="data"

    ordering =['name']# data order by name 


    # if need any filters
    def get_queryset(self):
        return Student.Objects.filter(name="jay")
    # If need Custom Context
    def get_context_data(self):
        conext= super().get_context_data(*ar,**kar)
        context['roll']=21
        return context
    # if need Change template setting
    def get_template_names(self):
        template_name = "test.html"
        ...logic....
        return [template_name]
``` 
### 2.  DetailView
- Get Single Object using id 
- ex. Model.objects.get(id=1)
```py

# urls.py
path("home/<int:id>/",TestView.as_view(),name=test)


from django.views.generic.detail import DetailView
from .models import TestModel

class TestView(DetailView):
    model = TestModel

    # default
    # testmodel (context_name)
    # testmodel_detail.html (template name )

     # Custom d
    template_name ="home.html"
    context_object_name ="data"

    # detailView have id 
    pk_url_kwarg ='id'
    # id is the same as url id 
```




## 2. EditView

### 1.FormView
- simple pass the form from view to templates
```py
from django.views.generic.edit import FormView
from .form import testform
class TestView(FormView):
    template_name = "test.html"
    form_class = testform
    success_url ='/home/'# when form are submit then redirect thsi url 

    # if need form data print or create logic 
    def form_valid(self,form):
        print(form)
        ...logic...
        return super().form_valid(form)
```
### 2.CreateView
- Create Form and Save data in database with logic

```py
from django.views.generic.edit import CreateView
from .form import loginform
from django.url import reverse
class LoginPage(CreateView):
    model = loginform
    fields =["name","email","password"]
    # default template (loginform_form.html)
    success_url ="homepage/"
    # need to return again this page
    def get_absolute_url(self):
        return reverse("loginpage")
```
### 3.UpdateView
- update the form or data 

```py

from django.views.generic.edit import UpdateView
from .form import loginform
from django.url import reverse_lazy

class MyClassView(UpdateView):
    model = MyModel
    form_class = MyForm
    template_name = 'your_model_update_form.html'
    success_url = reverse_lazy('your_form')
```



``
### 4.DeleteView
- delete data 

```py

from django.views.generic.edit import DeleteView
from .form import loginform
from django.url import DeleteView

class MyClassView(UpdateView):
    model = MyModel
    form_class = MyForm
    template_name = 'your_model_update_form.html'
    success_url = reverse_lazy('your_form')
```






# EXMPLE ________________________________________
from django.views.generic import ListView,DetailView
from django.views.generic.edit import CreateView


class HomePageClass(ListView):
    model=Category
    template_name = 'Pages/home.html' 
    context_object_name ="categories"
    def get_context_data(self, **kwargs: Any) -> Dict[str, Any]:
        context = super().get_context_data(**kwargs)
        cat_id = self.request.GET.get('category')
        search = self.request.GET.get("search")
        print("search:",search)
        if cat_id:
            context['products'] = Product.objects.filter(category_id=cat_id)
        elif search:
            context['products'] = Product.objects.filter(Q(title__icontains=search) | Q(description__icontains=search) )
        else:
            context['products'] = Product.objects.all()

        return context



class ProductViewClass(DetailView):
    model = Product
    template_name = 'Pages/ProductsView.html'
    context_object_name = 'details'
    pk_url_kwarg = 'id'







