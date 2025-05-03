
# Projeto de Validação de E-mail com Google Sheets e Expressões Regulares

## 🛠️ Procedimento e Material Utilizado

- **Ferramentas**: Google Sheets e Google Docs  
- **Fórmula utilizada (padrão brasileiro com `;`)**:
  ```excel
  =SE(REGEXMATCH(B2; "^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$"); "Válido"; "Inválido")
  ```

  ⚠️ **Atenção:**  
  Se o seu Google Sheets estiver configurado no padrão **americano** ou outro idioma com separador de argumentos por **vírgula (,)**, use:
  ```excel
  =IF(REGEXMATCH(B2, "^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$"), "Válido", "Inválido")
  ```

- **Formatação condicional**:
  - Se resultado for “Válido”: cor verde + negrito  
  - Se resultado for “Inválido”: cor vermelha + negrito  

- A planilha recebe uma coluna de e-mails e retorna se são válidos ou não, usando RegEx.

---

## 🧩 **Explicação das Expressões Regulares**

A expressão regular utilizada para validar e-mails foi:

```regex
^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$
```

A explicação de cada parte da expressão é:

1. `^`: **Início da string**. O que vem depois precisa estar no começo da string.
2. `[A-Za-z0-9._%+-]+`: 
   - Este conjunto define os **caracteres válidos** que podem aparecer no nome do usuário do e-mail.
   - `[A-Za-z0-9]` permite letras maiúsculas e minúsculas e números.
   - `._%+-` permite que também possam aparecer **pontos, sublinhados, percentuais, sinais de mais e menos**.
   - O `+` significa que pelo menos **um desses caracteres** deve aparecer (não pode ser vazio).
3. `@`: O **símbolo @** separando o nome do usuário e o domínio do e-mail.
4. `[A-Za-z0-9.-]+`: 
   - Define os caracteres válidos para o **domínio do e-mail**.
   - `[A-Za-z0-9]` permite letras e números.
   - `.-` permite o uso de **ponto e hífen** no nome do domínio.
   - O `+` significa que pelo menos **um desses caracteres** deve aparecer (novamente, não pode ser vazio).
5. `\.`: **Ponto literal**. Para garantir que o ponto seja tratado como um caractere literal (não como um metacaractere na RegEx).
6. `[A-Za-z]{2,}`: 
   - Refere-se ao **domínio de nível superior** (como `.com`, `.org`, `.edu`).
   - `[A-Za-z]` significa que apenas **letras** são permitidas.
   - `{2,}` significa que o domínio de nível superior deve ter pelo menos **dois caracteres**.
7. `$`: **Fim da string**. O que vem antes precisa estar no final da string.

### 🔄 Como funciona a validação:

- A expressão regular permite qualquer e-mail válido de acordo com os padrões gerais (letras, números, pontos, sublinhados, etc.).
- Exemplo de e-mails válidos: 
  - `usuario@dominio.com`
  - `nome.sobrenome@exemplo.org`
  - `usuario123@dominio.com.br`
- E-mails inválidos seriam aqueles que não seguem esse padrão, como:
  - `usuario@dominio` (sem o domínio de nível superior, como `.com`)
  - `@dominio.com` (sem nome de usuário)
  - `usuario@dominio,com` (erro no separador entre domínio e TLD)

---

## 📝 Considerações Finais

Este projeto tem como objetivo facilitar a validação de e-mails de usuários em sistemas que requerem um cadastro. Ao utilizar a função `REGEXMATCH` do Google Sheets, é possível realizar essa validação de forma simples e eficaz, garantindo que os e-mails sejam aceitos apenas se estiverem dentro do formato padrão esperado.

Este processo pode ser adaptado para outras ferramentas ou linguagens de programação que aceitem expressões regulares.
