<style>
    p{
        text-align: justify;
    }
    #format-here{
        font-style: italic; 
        font-size: 12px;
    }
</style>

# Funcionalidades para o Pedido de Compra

## Conteúdo

**Este passo a passo contém as seguintes etapas:**

1. Ajustar o Pedido de compras para marcar **todos** os itens do pedido ao invés de apenas um.

2. Deixar entrar com um só item no **pedido de compra**.

3. Receber um item apenas no **xml** que entra no pedido de compra quebrado em mais itens.

Para acessar a nova funcionalidade, acesse a Central xml-e devidamente configurada em seu menu no Protheus e selecione o registro que deseja realizar a rotina.

Com o registro já selecionado clique em: **Gerar Entrada** > **Outras Ações > Buscar Pedido Compra**. Como na imagem abaixo:

![Figura 01: Buscar Pedido de Compra](../../assets/pc-completo/00-start-busca-pc.png "Buscar Pedido de Compra"){: .center-img }
<span class="format">*Figura 01: Buscar Pedido de Compra*


## Marcar todos os itens de um Pedido
<span id="format-here">Ajustar o Pedido de compras para marcar todos os itens do pedido ao invés de apenas um.</span>

Após fazer o passo anterior você verá uma nova tela com os pedidos de compra feitos para o fornecedor selecionado. Com isso você poderá selecionar/vincular os itens de forma mais conveniente e intuitiva veja:

![Figura 02: PC para o Fornecedor selecionado](../../assets/pc-completo/01-pc-fornecedor.png "PC para o Fornecedor selecionado"){: .center-img }
<span class="format">*Figura 02: PC para o Fornecedor selecionado*


### Selecionando/vinculando os itens

Siga a sequência:

![Figura 03: Seleção de itens](../../assets/pc-completo/02-selecao-itens.png "Seleção de itens"){: .center-img }
<span class="format">*Figura 03: Seleção de itens*


1.1. Selecione um único pedido de compra no campo **Filtrar Pedidos de Compras**.

1.2. Clique no botão **Gerar Pedido de Compra**.

1.3. Na caixa que abrir você selecionará os **Itens do XML** e assim os mesmos aparecerão no próximo passo. ***Caso a caixa não apareça, significa que os itens já foram vinculados (Produto x Fornecedor)***.

1.4. Os itens selecionados na **simulação da pré-nota** mudarão a cor do status para verde.  Para desfazer, clique no botão **Limpar Alterações Realizadas** ou clicar no botão **confirmar** para finalizar a ação. 

## Entrada com item único
<span id="format-here">Deixar entrar com um só item no pedido de compra.</span>

Com o registro já selecionado clique em: **Gerar Entrada > Outras Ações > Buscar Pedido Compra**. Como na imagem abaixo:

![Figura 04: Buscar Pedido de Compra](../../assets/pc-completo/00-start-busca-pc.png "Buscar Pedido de Compra"){: .center-img }
<span class="format">*Figura 4: Buscar Pedido de Compra*


2.1. Escolha um item do pedido e clique com o botão direito do mouse na **linha** do item escolhido.  Uma caixa abrirá com a opção de  **Replicar em todos os itens do XML.**  Clique na mesma.

![Figura 05: Replicar em todos os itens do XML](../../assets/pc-completo/04-replicar-ptodos.png "Replicar em todos os itens do XML"){: .center-img }
<span class="format">*Figura 05: Replicar em todos os itens do XML*


2.2. Um aviso de confirmação irá ser exibido.

![Figura 06: Confirmação de aplicação](../../assets/pc-completo/05-confirmacao.png "Confirmação de aplicação"){: .center-img }
<span class="format">*Figura 06: Confirmação de aplicação*


Clicando em SIM, os itens na seção **Simulação da Pré-Nota.** Ficarão com o status verde.

Depois basta clicar no botão **confirmar** para finalizar a ação ou no botão **Limpar Alterações Realizadas** para cancelar.

## Item único do XML quebrado em mais itens
<span id="format-here">Receber um item apenas no xml que entra no pedido de compra quebrado em mais itens.</span>

Com o registro já selecionado clique em: **Gerar Entrada > Outras Ações > Buscar Pedido Compra**. Como na imagem abaixo:

![Figura 07: Buscar Pedido de Compra](../../assets/pc-completo/00-start-busca-pc.png "Buscar Pedido de Compra"){: .center-img }
<span class="format">*Figura 07: Buscar Pedido de Compra*


3.1. Selecione um único pedido de compra no campo **Filtrar Pedidos de Compras.**

3.2. Depois clique em gerar pedido completo**.**

![Figura 08: Gerar Pedido Completo](../../assets/pc-completo/07-gerar-pc-completo.png "Gerar Pedido Completo"){: .center-img }
<span class="format">*Figura 08: Gerar Pedido Completo*


Alguns pedidos de compra que possuem muitos itens e quando o fornecedor envia a nota fiscal vem apenas um único item contemplando todos os itens do pedido de compra. Após esse processo os itens do pedido estarão na sessão da pré-nota, mesmo se o XML tiver apenas um único item.

<div style="text-align: center; font-weight: bold;">-FIM-</div>