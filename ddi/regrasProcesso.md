---
currentMenu: ddi-regras-processo
parentMenu: ddi
---

# Dealer Data Integration

## 7. Regra de negócio
### 7.1. Venda
Produto que foi faturado para um cliente final.
Produto que foi faturado para outra concessionária AGCO não deve ser enviado como venda e sim como transferência. Ver item 4.2.3.

### 7.2. Devolução
Devolução de um produto do cliente final para a concessionária.
Devoluções da concessionária para a AGCO não devem ser enviadas.

### 7.3. Transferência
Transferência entre filiais ou transferência de uma concessionária para outra.

### 7.4. Campanha
Envio de campanha válida e existente no banco obecendo as seguintes regras:

 - Modelo do produto contido na NF deve ser válida para Campanha selecionada;
 - Ao selecionar Campanha é obrigatório o envio do XMLNFe;
 - Somente NF de venda poderão conter Campanha;
