# Cronograma de Estudos para Residência Médica (MVP)

Este é o projeto frontend compilado para o aplicativo web PWA "Cronograma de Estudos para Residência Médica". Ele inclui a integração inicial com o Supabase para autenticação de usuários (Alunos e Administradores).

## Configuração do Supabase

Antes de implantar, certifique-se de ter configurado seu projeto no Supabase. Você precisará de:

1.  **URL do Projeto Supabase:** Encontrada em `Settings` -> `API`.
2.  **Chave Anon Pública do Supabase:** Encontrada em `Settings` -> `API`.

**Importante:** Você deve substituir `SUA_URL_SUPABASE` e `SUA_CHAVE_ANON_SUPABASE` no arquivo `index.html` com suas credenciais reais do Supabase.

```html
<script>
  const SUPABASE_URL = 'SUA_URL_SUPABASE';
  const SUPABASE_ANON_KEY = 'SUA_CHAVE_ANON_SUPABASE';
  const supabase = Supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
</script>
```

### Configuração do Banco de Dados Supabase

Para as funcionalidades de cronograma e usuários, você precisará criar as seguintes tabelas no seu projeto Supabase:

**Tabela: `schedules`**

| Coluna       | Tipo     | Descrição                               |
| :----------- | :------- | :-------------------------------------- |
| `id`         | `uuid`   | Chave primária (gerada automaticamente) |
| `title`      | `text`   | Título do cronograma                    |
| `description`| `text`   | Descrição detalhada do cronograma       |
| `is_active`  | `boolean`| Indica se o cronograma está ativo       |
| `current_week`| `int`    | Semana atual do cronograma              |
| `created_at` | `timestamp with time zone` | Data de criação (padrão: `now()`)       |

**Tabela: `user_profiles` (Opcional, para gerenciar roles mais facilmente)**

| Coluna       | Tipo     | Descrição                               |
| :----------- | :------- | :-------------------------------------- |\n| `id`         | `uuid`   | ID do usuário (referência a `auth.users.id`) |
| `role`       | `text`   | Papel do usuário (`aluno` ou `admin`)   |

Você também pode gerenciar as roles dos usuários diretamente na `user_metadata` do Supabase Auth, como implementado no `index.html`.

## Como Implantar

Este projeto é um site estático compilado, o que o torna fácil de implantar em serviços como GitHub Pages ou Vercel.

### Opção 1: GitHub Pages

1.  **Crie um Novo Repositório no GitHub:** Crie um novo repositório público (ex: `medical-residency-pwa`).
2.  **Faça Upload dos Arquivos:** Faça upload de todo o conteúdo desta pasta (`medical-residency-frontend/`) para a raiz do seu novo repositório.
3.  **Configure o GitHub Pages:**
    *   Vá para as `Settings` do seu repositório.
    *   Clique em `Pages` na barra lateral esquerda.
    *   Em `Source`, selecione a branch `main` (ou a que você usou para o upload) e a pasta `/ (root)`.
    *   Clique em `Save`.
4.  **Aguarde:** O GitHub Pages levará alguns minutos para implantar seu site. O URL será algo como `https://<seu-usuario>.github.io/<nome-do-repositorio>/`.

### Opção 2: Vercel

1.  **Crie um Novo Repositório no GitHub:** Se ainda não o fez, crie um novo repositório no GitHub e faça upload de todo o conteúdo desta pasta para ele.
2.  **Importe o Projeto para o Vercel:**
    *   Vá para [Vercel Dashboard](https://vercel.com/dashboard).
    *   Clique em `Add New...` -> `Project`.
    *   Selecione seu repositório GitHub que contém o projeto.
    *   O Vercel detectará automaticamente que é um projeto estático. Mantenha as configurações padrão.
    *   Clique em `Deploy`.
3.  **Aguarde:** O Vercel construirá e implantará seu site. Você receberá um URL de implantação (ex: `https://<nome-do-projeto>.vercel.app/`).

Após a implantação, você poderá acessar seu PWA e testar as funcionalidades de autenticação e as áreas de Aluno/Administrador.

---

**Observação:** Como este projeto foi reconstruído a partir de uma versão compilada, o código-fonte original do React não está incluído. As modificações foram feitas diretamente no `index.html` e nos scripts JavaScript para adicionar as funcionalidades solicitadas. Para futuras manutenções e desenvolvimento, é altamente recomendável manter e trabalhar com o código-fonte original do React. 

