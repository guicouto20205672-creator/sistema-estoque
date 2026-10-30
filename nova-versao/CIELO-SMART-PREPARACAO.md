# Preparação do Brasa PDV para Cielo Smart

Status: preparação técnica — ainda não conectado a pagamentos reais.

## Situação atual
- O Brasa PDV atual é uma aplicação web (HTML/CSS/JavaScript) publicada no GitHub Pages.
- A maquininha fotografada informa Positivo L300 V5 e mostra a interface Cielo.
- A compatibilidade específica do L300 V5 com o fluxo de integração e publicação precisa ser confirmada pela Cielo antes de gerar um pacote instalável.

## Arquitetura recomendada
1. Manter o PDV web atual como sistema principal de estoque, vendas, caixa e comandas.
2. Criar um aplicativo Android de terminal com uma camada nativa (Java/Kotlin) para comunicação com os recursos Cielo Smart.
3. Para integração remota, usar um serviço de backend HTTPS para autenticar e conversar com a API Order Manager. Não colocar Client Secret, Access Token ou outras credenciais privadas no HTML/JavaScript do navegador.
4. O aplicativo deve encaminhar o resultado da transação ao PDV e só marcar a venda como paga após confirmação válida da Cielo.
5. Implementar identificador único/idempotência, consulta de status e tratamento de cancelamento/timeout para evitar vendas duplicadas ou marcadas como pagas sem confirmação.
6. Testar primeiro em Sandbox/emulador; produção somente após autorização e credenciais apropriadas.

## O que já está preparado
- Este documento registra o plano sem alterar o sistema de produção nem os dados do Supabase.
- Nenhuma credencial foi criada, armazenada ou publicada.
- Nenhum pagamento real foi iniciado.

## Dependências externas
- Confirmação formal da Cielo de que o modelo Positivo L300 V5 aceita o fluxo escolhido e pode receber o aplicativo.
- Cadastro de desenvolvedor Cielo e criação das credenciais de Sandbox.
- Para produção, vínculo do estabelecimento comercial (EC) e emissão das credenciais de produção conforme processo da Cielo.
- Aprovação/publicação ou distribuição privada do aplicativo na Cielo Store, conforme as regras aplicáveis.

## Próximas etapas
1. Responsável pelo estabelecimento confirmar com a Cielo a compatibilidade do L300 V5 e solicitar orientação de integração/publicação.
2. Criar credenciais de Sandbox no Portal de Desenvolvedores Cielo.
3. Definir se o primeiro piloto será integração remota (PDV atual envia o pedido) ou aplicativo nativo com Deep Link.
4. Implementar e testar sem tocar no fluxo de vendas atual.
5. Após aprovação, configurar produção e testar com autorização do titular do estabelecimento.

## Referências oficiais
- https://docs.cielo.com.br/cielo-smart/docs/primeiros-passos
- https://docs.cielo.com.br/cielo-smart/docs/modelos-de-integracao
- https://docs.cielo.com.br/cielo-smart/docs/autenticacao-e-credenciais
- https://docs.cielo.com.br/cielo-smart/docs/fluxo-e-status-do-pedido
- https://docs.cielo.com.br/cielo-smart/docs/integracao-via-deep-link
