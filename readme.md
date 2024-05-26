![Static Badge](https://img.shields.io/badge/Alura-%230b182c)
![Static Badge](https://img.shields.io/badge/Django-4.2.13-%23092E20?logoColor=ffffff)

# 1 - App usuários

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


