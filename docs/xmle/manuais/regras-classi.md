<style>
    p{
        text-align: justify;
    }
    #green{
        background-color: #16F529;
        display: inline;

    }
    #red{
        background-color: red;
        display: inline;
    }
    #blue{
        background-color: blue;
        display: inline;
    }
</style>

# Regras de Classificação

## Introdução

Rotina “Regras de Classificação” é o cadastro de regras da ferramenta Athos XML-e que vai ser utilizada para retornar de maneira inteligente qual será a informação mais apropriada a ser utilizada em cada tipo de documento (ZZV_TIPDOC). 


## Como usar?

Deverá ser cadastrado, por filial, todas as regras de filtros inteligentes para o retorno das informações necessárias para classificação do documento fiscal (TES, condição de pagamento, centro de custo e natureza).

Segue abaixo os campos e detalhes sobre o preenchimento:

### Regras de preenchimento da Tabela ZZV

| Campo      | Descrição           | <center>Observação</center> |
| ---------- | ------------------- | --------------------------- |
| ZZV_FILIAL | Filial              | As regras são exclusivas por filial |
| ZZV_TIPDOC | Tipo Doc            | 1 = CTE Venda; 2 = NF-e Compras; 3 = CTE Compras; 4 = Devolução Venda |
| ZZV_PROCE  | Processo            | 1 = Cond. Pgto; 2 = TES; 3 = C Custo; 4 = Natureza; |
| ZZV_CODPRO | Cod. Produto        | Informar o código do produto |
| ZZV_GRPPRO | Grupo Prod.         | Informar o grupo do produto |
| ZZV_CLIFOR | Cod. Clifor         | Informar o código do fornecedor ou cliente quando for devolução de venda |
| ZZV_LOJA   | Loja Cli. - Fornec. | Informar a loja do fornecedor ou cliente quando for devolução de venda |
| ZZV_CSICMS | CST ICMS            | CST a ser considerada. Deve ser um número de 00 a 99 |
| ZZV_DIAINI | Dia início emissão  | Número entre 1 e 31, período inicial da emissão do documento fiscal |
| ZZV_DIAFIM | Dia fim emissão     | Número entre 1 e 31, período final da emissão do documento fiscal |
| ZZV_TAG    | Tag XML             | Tag do XML a ser analisada. Deve iniciar obrigatoriamente com OXML:<br>**Exemplo:**<br> OXML:_CTEPROC:_CTE:_INFCTE:_INFCTENORM:_INFCARGA:_PROPRED |
| ZZV_VLRTAG | Valor Tag           | Valor a ser encontrado na TAG informada acima. <br>**Exemplo:** <br>LEITE CRU PRE BENEFICIADO PADRONIZADO |
| ZZV_RESULT | Resultado           | Resultado que será retornado pelo filtro no JOB (código da TES ou natureza ou centro de custo ou condição de pagamento) |

### Regras Gerais

- Os campos destacados em <div id="red">vermelho</div> são de preenchimento obrigatórios e indicam a filial, tipo de documento e o tipo de informação que será retornado.
- Os campos destacados em <div id="blue">azul</div> são utilizados para compor o filtro inteligente em busca da informação a ser retornada. 
- Caso não deseje que filtre alguns desses campos, basta deixá-los em vazios.
- Os campos “Dia início emissão” e “Dia fim emissão” se completam, portanto será pesquisado o dia de emissão do documento fiscal que está entre esses dois campos, caso eles estejam preenchidos.
- Os campos “Tag Xml” e “Valor Tag” se completam, portanto sempre que informar o campo “Tag Xml” deve ser informado no campo “Valor Tag” o que se deseja encontrar na tag do XML informada. Caso não deseje realizar filtro pela tag, basta deixar os dois campos vazios.
- Os campos destacados em <div id="green">verde</div> contém o valor a ser utilizado quando os filtros corresponderem ao processo (TES, condição de pagamento, natureza ou centro de custo).
- O critério de seleção do registro a ser retornado será aquele que atender ao maior número de semelhanças com os campos de filtros.
- Em caso de empate entre duas ou mais regras, será utilizado a registro mais antigo.


### A Tela de Cadastro

A tela de cadastro das regras de classificação poderá ser acessada no menu do Facile XML-e.

<center>![Figura 1: Menu com a opção 'Regras Classificação'](../../assets/regras-classi/menu-c-regras.png "Menu com a opção 'Regras Classificação'")
<br>*Figura 1: Menu com a opção 'Regras Classificação'*<br></center>
<br>

<center>![Figura 2: Tela de Cadastro de Regras de Classificação](../../assets/regras-classi/cad-regras.png "Tela de Cadastro de Regras de Classificação")
<br>*Figura 2: Tela de Cadastro de Regras de Classificação*<br></center>
<br>

<center>![Figura 3: Tela de Cadastro](../../assets/regras-classi/tela-cad.png "Tela de Cadastro")
<br>*Figura 3: Tela de Cadastro*<br></center>
<br>

**Campos obrigatórios:** Tipo Doc., Processo e Resultado

### Campos e validações

O Campo “Tag Xml” requer que seja configurado o caminho completo do nodo até a TAG, e deve iniciar com “OXML:” <br>***Exemplo:*** <br>OXML:_NFEPROC:_NFE:_INFNFE:_EMIT:_ENDEREMIT:_UF

E se faz o obrigatório informar o filtro **“Valor da Tag”**.
**Importante:** Nas regras cadastradas, os campos em branco, significam que servem para todos, por exemplo: 

*- “Cód. de Produto” em branco, a regra cadastrada, serve para todos os produtos.*

**- A pesquisa do resultado vai verificar a maior quantidade de campos coincidentes com as regras e vai retornar um só resultado.**

**- Dependendo dos conteúdos dos campos, pode não ter nenhum resultado.**

<div style="text-align: center; font-weight: bold;">-FIM-</div>