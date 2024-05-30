![Static Badge](https://img.shields.io/badge/Alura-%230b182c)
![Static Badge](https://img.shields.io/badge/Django-4.2.13-%23092E20?logoColor=ffffff)

# Passo a passo do curso

## 1 - App usuários

Criar novo app

```
python manage.py startapp usuarios
```

Adicinar no arquivo **setup/settings.py**

```
INSTALLED_APPS = [
    ...
    'usuarios.apps.UsuariosConfig',
]

```

Criar arquivo de rotas **usuarios/urls.py**  
Alterar **setup/urls.py**

```
urlpatterns = [
    ...
    path('', include('usuarios.urls')),
] ...
```
Adicionar as views em **usuarios/views.py**  
Criar arquivos html em **templates/usuarios/**

## 2 - Formulários no django

Criar arquivo **usuarios/forms.py**  
Alterar arquivo e view **usuarios/views.py**

```
...
from usuarios.forms import LoginForms

def login(request):
    form = LoginForms()
    return render(request, "usuarios/login.html", {"form": form})
...
```

Alterar arquivos html **templetes/usuarios/**

## 3 - Autenticação de usuários

Alterar arquivo **usuarios/views.py** para adicionar as validações e mensagens.
Alterar arquivo **templates/galeria/base.html** e adicionar as mensagens.

```
{% for message in messages %}
    <div class="alert alert-primary">
        <p id="messages">{{message}}</p>
    </div>
{% endfor %}
```

Opção de logout:  
Alterar arquivo **usuarios/views.py**

```
def logout(request):
    auth.logout(request)
    messages.success(request, "Logout efetuado com sucesso!")
    return redirect('login')
```

Alterar aarquivo **usuarios/urls.py**

```
path('logout', logout, name='logout'),
```

## 4 - Validações

Alterar o arquivo **usuarios/forms.py**, adicionando regras dde vaalidações do formulário.

```
def clean_nome_cadastro(self):
    nome = self.cleaned_data.get('nome_cadastro')
    if nome:
        nome = nome.strip()
        if ' ' in nome:
            raise forms.ValidationError('Espaços não são permitidos nesse campo')
        else:
            return nome

def clean_senha_2(self):
    senha_1 = self.cleaned_data.get('senha_1')
    senha_2 = self.cleaned_data.get('senha_2')
    if senha_1 and senha_2:
        if senha_1 != senha_2:
            raise forms.ValidationError('Senhas não são iguais')
        else:
            return senha_2
```

Alterar arquivo **templates/usuarios/cadastro.html** para colocar as mensagens de erro de validações.

```
{% for error in field.errors %}
<div class="alert alert-danger">
    {{error}}
</div>
{% endfor %}
```

## 5 - Refatoração

Criar arquivo **templates/galeria/partials/_alertas.html**  
Alterar arquivo **templates/galeria/base.html**
Alterar arquivo **setup/settings.py**

```
from django.contrib.messages import constants as messages
MESSAGE_TAGS = {
    messages.ERROR: 'danger',
    messages.SUCCESS: 'success'
}
```

Alterar pasta **galeria/partions** para **partions**
