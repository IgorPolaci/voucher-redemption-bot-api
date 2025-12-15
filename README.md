# 🎟️ Voucher Redemption & Campaign Automation API

![GoogleSheetsAPI](https://img.shields.io/badge/Google_Sheets-Integration-success) ![Automation](https://img.shields.io/badge/Sales-Automation-blue)

## 📌 Visão Geral
API desenvolvida para gerenciar a validação e "queima" (redemption) de cupons promocionais em tempo real dentro de fluxos conversacionais (WhatsApp/Chatbots). O sistema utiliza o **Google Sheets como Database/CMS**, permitindo que equipes de Marketing acompanhem a campanha instantaneamente sem necessidade de acesso a bancos de dados complexos.

## 💼 O Problema de Negócio
Durante uma campanha de vendas com cupons limitados, a empresa enfrentava gargalos:
1.  **Custo Operacional:** Consultores de vendas perdiam tempo validando códigos manualmente.
2.  **Risco de Fraude:** Sem validação centralizada em tempo real, o mesmo cupom poderia ser utilizado por múltiplas pessoas.
3.  **Lead Desqualificado:** A equipe de vendas recebia contatos que não possuíam o benefício real, diminuindo a conversão.

## 💡 A Solução
Implementei uma camada de automação entre o Bot e a gestão da campanha:
- O usuário insere o código no WhatsApp.
- A API consulta a planilha da campanha via **Google Sheets API**.
- Se válido, a API **atribui o cupom** ao usuário (registra nome/telefone) e marca como "UTILIZADO" na planilha.
- O Bot só transfere para o humano se a API retornar `success: true`.

**Resultado:** O time de vendas passou a receber apenas leads **pré-qualificados** e com desconto validado.

## 🛠️ Tecnologias
- **Backend:** Node.js.
- **Integração:** Google API (Sheets v4).
- **Autenticação:** Service Account (Google Cloud Platform).
- **Logica de Negócio:** Validação de status, verificação de duplicidade e escrita atômica.

## 🔄 Fluxo da Aplicação

1.  **Input:** Bot envia `cupom` e `telefone_usuario`.
2.  **Read:** API varre a coluna de códigos na planilha.
3.  **Validation:**
    - O código existe?
    - A coluna "Status" está vazia?
4.  **Write:** Se aprovado, preenche "Status" = "Usado" e salva os dados do cliente.
5.  **Output:** Retorna JSON liberando o transbordo.
