![AGCO_logo](http://www.agco.com.br/content/agcocorp/pt_BR/_jcr_content/footermainparsys/footer/footerlogoimage.img.png/1485893878104.png)
# Integração VMI

## Regras do processo de integração
Essa sessão contém as regras que devem ser utilizadas para enviar a primeira carga dos dados e para a configuração dos eventos que devem disparar novas mensagens.
As mensagens de cargas não tem ordem para envio, assim como não é necessário esperar a primeira carga finalizar para enviar as mensagens do dia.
 
|Interface|Primeira carga|Cargas direcionadas a eventos|
|---------|--------------|-----------------------------|
|DMS-01|	Enviar posição atual dos itens que estão disponível com pedidos em aberto, itens reservados ou retornados. |	Deve ser disparada quando um item tiver movimentação.|
|DMS-02	|Enviar todas as peças que já tiveram alguma movimentação.|	Deve ser disparada quando um item tiver uma primeira compra, uma primeira data de disponibilidade ou a peça for atualizada nos campos definidos para o contrato.|
|DMS-03	|Enviar todos os pedidos de compra feitos para a AGCO ou outros fornecedores nos últimos 6 meses. As transferências entre filiais devem ser enviadas, mas as vendas para concessionárias da rede não.|	Deve ser disparado quando uma compra para a AGCO ou outros fornecedores for feita e sempre que sofrer uma alteração. Caso uma nova linha seja incluída no pedido a mesma deve ser enviada. As transferências entre filiais devem ser enviadas, mas as vendas para concessionárias da rede não.|
|DMS-04|	Enviar os últimos 36 meses de pedidos/vendas (balcão e oficina) e devoluções. As transferências entre filiais devem ser enviadas, mas as vendas para concessionárias da rede não.	|Deve ser disparada quando uma venda e/ou pedido de venda for aberto e salvo (balcão e oficina) ou devolução for realizada para um cliente final e sempre que essas informações sofrerem uma alteração. Caso uma nova linha seja incluída no pedido a mesma deve ser enviada. As transferências entre filiais devem ser enviadas, mas as vendas para concessionárias da rede não.|
|DMS-05|	N/A|	Deve ser disparada quando for registrada uma venda perdida por falta de estoque.|
|DMS-06|	Enviar todos os clientes ativos nos últimos 36 meses. Sendo ativos todos aqueles que realizaram compra, devolução, orçamentos ou gerarem uma venda perdida na concessionária.	|Deve ser disparada quando um cliente realizar alguma movimentação como compra, devolução, orçamento ou gerar uma venda perdida na concessionária.|