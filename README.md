## Introdução

Este repositório apresenta a documentação da atividade prática de testes de caixa cinza em uma API de autenticação utilizando Supabase e Postman.

## Configuração do Supabase

Para a realização da atividade, inicialmente, foi criada uma conta na plataforma Supabase e, em seguida, um novo projeto foi configurado.

O tipo de autenticação utilizado foi a autenticação por e-mail e senha.

Foi criado um usuário válido para ser utilizado nos testes de autenticação.

Após a configuração do projeto e da autenticação, foram obtidas as credenciais necessárias para execução dos testes no Postman, incluindo a URL da API e a chave de API do Supabase.

As imagens abaixo apresentam as evidências da configuração realizada no Supabase:

![Projeto Criado](/prints/Create_%20Project.png)
![Painel do Supabase](/prints/Supabase_Panel.png)
![Autenticação Habilitada](/prints/Enabled_Auth.png)
![Usuário Criado](/prints/Created_User.png)
![Credenciais da API](/prints/API_CREDENTIALS.png)

## Configuração do Postman

Para a execução dos testes de autenticação, foi utilizado o Postman Desktop, inicialmente, foi criado um Workspace específico para a atividade.

Também foi criado um Environment para armazenar as variáveis utilizadas durante os testes. As variáveis configuradas foram:

| Variável   | Descrição                                             |
| ---------- | ----------------------------------------------------- |
| `base_url` | URL base da API do Supabase                           |
| `api_key`  | Chave de API utilizada para autenticar as requisições |
| `email`    | E-mail do usuário criado no Supabase                  |
| `password` | Senha do usuário criado no Supabase                   |

As imagens abaixo apresentam as evidências da configuração realizada no Postman:

![Workspace Criado](/prints/Workspace_Created.png)
![Variáveis configuradas](/prints/ENV_Variables.png)

## Configuração das requisições

Para realizar os testes de autenticação, foi criada uma requisição HTTP no Postman utilizando o método `POST`. A requisição foi configurada para acessar o endpoint de autenticação do Supabase responsável por validar login com e-mail e senha.

O endpoint utilizado foi:

```text
{{base_url}}/auth/v1/token?grant_type=password
```

A variável `{{base_url}}` representa a URL base da API do projeto criado no Supabase. O caminho `/auth/v1/token?grant_type=password` indica que a requisição será enviada para o serviço de autenticação, utilizando o fluxo de login por senha.

A requisição foi configurada com os headers necessários para permitir a comunicação com a API do Supabase. Os headers utilizados foram:

| Header          | Valor                |
| --------------- | -------------------- |
| `apikey`        | `{{api_key}}`        |
| `Authorization` | `Bearer {{api_key}}` |
| `Content-Type`  | `application/json`   |

O header `apikey` foi utilizado para identificar a aplicação que está acessando o projeto Supabase. O header `Authorization` foi configurado utilizando o formato `Bearer`, conforme a estrutura esperada para autenticação. Já o header `Content-Type` informa que os dados enviados no corpo da requisição estão no formato JSON.

O corpo da requisição foi configurado na aba `Body`, utilizando a opção `raw` com o formato `JSON`. Nele foram informados o e-mail e a senha do usuário criado anteriormente no Supabase.

Na configuração realizada no Postman, também foram utilizadas variáveis de ambiente para facilitar a execução dos testes:

```json
{
  "email": "{{email}}",
  "password": "{{password}}"
}
```

As imagens abaixo apresentam as evidências da configuração da requisição no Postman:

![Endpoint configurado](/prints/Request_Endpoint.png)
![Headers configurados](/prints/Request_Headers.png)
![Body JSON configurado](/prints/Request_Body.png)

## Execução dos testes

Após a configuração da requisição de autenticação no Postman, foram executados testes caixa cinza com o objetivo de validar o comportamento da API de autenticação do Supabase em diferentes cenários.

Durante a execução dos testes, foram analisados os seguintes pontos:

- status HTTP retornado pela API;
- estrutura da resposta JSON;
- mensagens de erro;
- retorno do `access_token` no login válido;
- comportamento da autenticação em cenários válidos e inválidos.

A requisição utilizada nos testes foi:

```text
POST {{base_url}}/auth/v1/token?grant_type=password
```

Os cenários executados foram:

| Cenário               | Entrada Utilizada                      | Resultado Esperado          | Resultado Obtido                                         | Status |
| --------------------- | -------------------------------------- | --------------------------- | -------------------------------------------------------- | ------ |
| Login válido          | E-mail e senha corretos                | Status 200 + `access_token` | Login realizado com sucesso e token retornado            | OK     |
| Senha incorreta       | E-mail correto e senha incorreta       | Erro de autenticação        | A API retornou erro informando falha na autenticação     | OK     |
| Usuário inexistente   | E-mail não cadastrado e senha qualquer | Acesso negado               | A API não permitiu o login e retornou mensagem de erro   | OK     |
| Campos vazios         | E-mail e senha vazios                  | Erro de validação           | A API retornou erro por ausência de dados válidos        | OK     |
| Credenciais inválidas | E-mail e senha inválidos               | Mensagem de erro            | A API retornou mensagem informando credenciais inválidas | OK     |

No cenário de login válido, a API retornou uma resposta de sucesso contendo o token de acesso, confirmando que o usuário cadastrado foi autenticado corretamente. Nos demais cenários, a API bloqueou o acesso e retornou mensagens de erro, demonstrando que a autenticação está validando as credenciais enviadas na requisição.

As imagens abaixo apresentam as evidências dos testes realizados no Postman:

![Teste Login Válido](/prints/Test_Login_Valido.png)
![Teste Senha Incorreta](/prints/Test_Senha_Incorreta.png)
![Teste Usuário Inexistente](/prints/Test_Usuario_Inexistente.png)
![Teste Campos Vazios](/prints/Test_Campos_Vazios.png)
![Teste Credenciais Inválidas](/prints/Test_Credenciais_Invalidas.png)

## Registro dos testes

Após a execução dos testes no Postman, os resultados foram registrados em uma planilha de controle de testes. Essa planilha foi utilizada para documentar cada cenário executado, as entradas utilizadas, o resultado esperado, o resultado obtido, o status final e observações sobre o comportamento da API.

O registro dos testes foi organizado com os seguintes campos:

| Campo              | Descrição                                               |
| ------------------ | ------------------------------------------------------- |
| ID do teste        | Identificação única do teste executado                  |
| Cenário            | Descrição do cenário testado                            |
| Entrada            | Dados utilizados na requisição                          |
| Resultado esperado | Comportamento esperado da API                           |
| Resultado obtido   | Resposta real retornada pela API                        |
| Status             | Indicação se o teste foi concluído com sucesso ou falha |
| Observações        | Comentários adicionais sobre o teste                    |

A documentação dos testes é importante porque permite manter um histórico claro dos cenários avaliados e facilita a análise dos resultados obtidos. Além disso, o registro ajuda a identificar se a API está se comportando conforme o esperado em situações válidas e inválidas.

Durante os testes realizados, não foram identificadas falhas críticas no funcionamento da autenticação. O cenário de login válido retornou o token de acesso corretamente, enquanto os cenários inválidos retornaram mensagens de erro e impediram o acesso, conforme esperado.

As imagens abaixo apresentam as evidências do registro dos testes na planilha:

![Planilha de testes preenchida](/prints/Planilha_Testes.png)

A planilha utilizada para o registro dos testes também foi adicionada ao repositório na pasta `/planilha/`.

## Resultados obtidos

## Conclusão
