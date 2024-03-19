# FIAP Tech Challenge Fase 5

Bem-vindo ao repositório do FIAP Tech Challenge Fase 5. Este documento fornece uma visão geral dos serviços constituintes do projeto, detalhes sobre o padrão arquitetural adotado, informações de segurança e um vislumbre da arquitetura do sistema.

## Repositórios dos Serviços

O projeto é dividido em três serviços principais, cada um com seu próprio repositório:

- **Produtos**: Gerencia informações de produtos. [Acessar repositório](https://github.com/souzantero/fiap-tech-challenge-product)
- **Pedido**: Responsável pela criação e gestão de pedidos. [Acessar repositório](https://github.com/souzantero/fiap-tech-challenge-order)
- **Pagamento**: Processa pagamentos e comunicações com gateways de pagamento. [Acessar repositório](https://github.com/souzantero/fiap-tech-challenge-payment)

Para instruções detalhadas sobre como executar cada projeto localmente, consulte o arquivo README dentro de cada repositório.

## Arquitetura e Padrões

### Padrão SAGA

Adotamos o padrão SAGA coreografado devido à sua simplicidade de implementação. Neste modelo:

- O serviço de **Pedidos** dispara uma mensagem para uma fila ao criar um pedido.
- O serviço de **Pagamentos** escuta esta fila e inicia a comunicação com o gateway de pagamento.
- Após a invocação do webhook pela API do serviço de pagamento, mensagens são enviadas para filas de pagamento aceito ou rejeitado, conforme o caso.
- O serviço de **Pedidos** é então responsável por processar estas mensagens e realizar as ações compensatórias necessárias.

### Segurança

#### OWASP Zap Reports

Avaliamos a segurança dos nossos serviços usando o OWASP ZAP. Aqui estão os relatórios de segurança antes e após as correções:

- **Antes das Correções de Segurança**:
  - Lista de produtos: [Ver relatório](./owasp/before/2024-03-12-ZAP-Report-x3a2295ks0.execute-api.us-west-2.amazonaws.com.html)
  - Checkout do pedido: [Ver relatório](./owasp/before/2024-03-12-ZAP-Report-1kw68cnuwb.execute-api.us-west-2.amazonaws.com.html)
  - Webhook de confirmação de pagamento: [Ver relatório](./owasp/before/2024-03-12-ZAP-Report-88m06gflm7.execute-api.us-west-2.amazonaws.com.html)

- **Depois das Correções de Segurança**:
  - Lista de produtos: [Ver relatório](./owasp/after/2024-03-13-ZAP-Report-x3a2295ks0.execute-api.us-west-2.amazonaws.com.html)
  - Checkout do pedido: [Ver relatório](./owasp/after/2024-03-13-ZAP-Report-1kw68cnuwb.execute-api.us-west-2.amazonaws.com.html)
  - Webhook de confirmação de pagamento: [Ver relatório](./owasp/after/2024-03-13-ZAP-Report-88m06gflm7.execute-api.us-west-2.amazonaws.com.html)

## Desenho da Arquitetura

Para uma visão completa da arquitetura do sistema, consulte a imagem abaixo:

![Desenho da Arquitetura](./diagram/architecture.png)