# XCarregDados

O XCarregDados é um ponto de entrada para manipular valores durante o processamento do XML recebido.

O presente ponto de entrada é executado tanto em job, quanto em tela. É necessário tomar cuidado com as funções visuais a serem utilizadas.

Esse ponto de entrada é executado antes da leitura da classe de domínio, para manipular os valores antes mesmo da primeira interpretação do XML. Em suma, o que é manipulado aqui interfere até mesmo na gravação das tabelas de log, sendo elas, as FACX002 (Controle de NSU) e FACX003 (Gestão de CT-e). Dessa forma, apesar de ser possível, não encorajamos que os XMLs não desejados sejam descartados nesse ponto de entrada, sendo o **SAVEZZZ** o ponto de entrada ideal para esse comportamento.

Os parâmetros de entrada são o mesmo objeto de retorno do ponto de entrada.

## Parâmetros

* **oDados:** object, Objeto com os dados do XML recebido, objeto da classe PTX_Cabecalho_Model


## Retorno

* **oDados:** object, Objeto com os dados a serem interpretados pela classe de domínio, objeto da classe PTX_Cabecalho_Model. Ainda pendentes das validações usuais da ferramenta.

### Ponto de atenção 

O **oDados** de retorno nunca poderá ser nulo; um retorno nulo interrompe o download de notas. Sendo assim, existem duas formas válidas de retorno:

* Seguir com o documento: retorne o **oDados** recebido em Paramixb[1], com ou sem alterações. 
* Descartar o documento: retorne uma nova instância vazia, PTX_Cabecalho_Model():New(). O documento não será gravado e seu NSU será, inclusive, pulado na FACX002.


## Exemplo de utilização

O exemplo abaixo é ilustrativo e não deve ser utilizado em produção sem revisão e adaptação à regra de negócio do cliente.

```AdvPL
User Function XCarregDados()

  Local oDados   := ParamIxb[1] as Object
  Local cFilNova := ""          as Character

  If !Empty(oDados:cIEDestinatario) .And. oDados:cCodigoFilial == "0101"  //|Só processa na filial 1 |

    If oDados:cIEDestinatario == "INSCRICAO_FICTICIA_01" 
    
      cFilNova := "0102"
      oDados:cCodigoFilial := cFilNova //Altera oDados quando é recebido na primeira filial e tem outra IE.
    
    Endif

  EndIf

  //Se não é da filial 0101, não modifica o oDados e o retorna do mesmo jeito que veio.
Return oDados
```


## oDados

O **oDados**, dentro da lógica deste presente ponto de entrada, é um DTO (*Data Transfer Object*) de atributos fixos, um objeto da classe PTX_Cabecalho_Model e transporta os dados lidos do XML até suas respectivas classes de domínio, sem regra de negócio a priori.

A Classe PTX_Cabecalho_Model só tem um método, o New, que seria o constructor base, sem quaisquer informações preenchidas. A manipulação de seu conteúdo deve ser feita utilizando o método de acesso direto, ou seja, conforme exemplo abaixo, onde a propriedade é acessada e modificada diretamente.

```AdvPL
  Local oObj := Nil

  oObj := PTX_Cabecalho_Model():New()

  oObj:cCodigoFilial := "0101"
```

### Propriedades

Abaixo, segue uma tabela com as propriedades e seus respectivos fins. 

Recomenda-se não alterar nenhuma propriedade além do necessário. As propriedades cuja coluna "Manipulação" está preenchida com "Não recomendada" são aquelas cuja manipulação pode violar o comportamento padrão da ferramenta.

| Propriedade | Tipo | Descrição | Manipulação |
| ----------- | ---- | ---------- | ----------- |
| cCodigoFilial | Character | Filial destino do documento | |   
| cIEDestinatario | Character | Inscrição Estadual do destinatário do documento | |  
| cTipoXml | Character | Tipo do documento, referente ao ZZZ_TIPO | Não recomendada |           
| cNotaFiscal | Character | Número do documento | |        
| cSerieNF | Character | Série do documento | |           
| cCnpjEmissor | Character | CNPJ do Emissor | |       
| cNomeEmissorNF | Character | Razão Social do Emissor | |     
| cChaveNF | Character | Chave da NF | Não recomendada |           
| cAnoNF | Character | Ano de emissão | |             
| cMesNF | Character | Mês de emissão | |             
| cIEEmitente | Character | Inscrição Estadual do emitente do documento | |        
| cStatus | Character | Status do XML, referente ao ZZZ_STATUS | |            
| cCodigoEvento | Character | Evento do XML, referente ao ZZZ_CODEVE | |      
| cOk | Character | Legenda do Facile XML-e, referente ao ZZZ_OK | |                
| cCodigoRetorno | Character | Código de retorno do provider, referente ao ZZZ_CODRET | |     
| cDescricaoRetorno | Character | Mensagem de retorno do provider, referente ao ZZZ_DESRES | |  
| cHoraBaixa | Character | Hora do download, referente ao ZZZ_YHORA | Não recomendada |         
| cSituacaoDocumento | Character | Situação do documento no serviço do provedor | | 
| cArquivoXml | Character | XML recebido da nota | Não recomendada |        
| cPdf | Character | **DESCONTINUADO** | Não recomendada |         	    
| cEventoXml | Character | Evento recebido do XML | |    	    
| cDhResp | Character | Data / Hora da autorização | |    		    
| cSchema | Character | Schema do XML, referente aos arquivos .XSD disponíveis no serviço de cada provedor | |    		    
| cProvider | Character | Identificador do provedor do XML | Não recomendada |   		    
| cTipoNfFornecedor | Character | Tipo da NF do Fornecedor | Não recomendada |  
| cTipoDocumento | Character | Ler abaixo | Não recomendada |     
| dDataRecebimento | Date | Data do Recebimento do provedor | |   
| dEmissaoNF | Date | Data da Emissão da nota | |         
| dDataRecibo | Date | Data da Autorização do provedor | |        
| nValorNF | Numeric | Valor referente a nota| |           
| nNsu | Integer (Numeric) | NSU da nota| Não recomendada |               
| nRecnoZZZ | Integer (Numeric) | Recno da ZZZ da nota, caso exista | Não recomendada |          
| aItens | Array | Array com os Itens da Nota Fiscal, cada posição contendo um objeto PTX_Item_Model | |          


#### cTipoDocumento

cTipoDocumento é uma propriedade simples de controle interno. Seus possíveis tipos seguem abaixo.

```
1=NFe normal
2=NFe complem.
3=NFe ajuste
4=NFe Devolução
5=CTe Venda Normal
6=CTe Compra Normal
7=CTe Venda Complem.
8=CTe Compra Complem.
9=CTe Venda Anulação
A=CTe Compra Anulação
B=CTe Venda Substituto
C=CTe Compra Substituto
D=NFSe normal
```


## Como testar

O XCarregDados é executado em qualquer interpretação de XML da ferramenta, sendo assim, a função "Importar XML do Computador" presente no PTX0001 (Central XML), é a forma ideal de realizar os testes dessa função, verificando se o retorno foi suficiente para importação ou se o fluxo de entrada foi quebrado durante a execução.


## Consequências

O fluxo de personalização do XCarregDados pode interferir em toda recepção de documentos pelo Facile XML-e. É necessário extrema cautela na personalização deste fluxo, dessa forma, qualquer eventual erro pode ocasionar em NSUs sendo pulados na FACX002. Fora dos casos de descarte intencional, um NSU pulado é a principal evidência de erro durante a execução do ponto de entrada.

Com isso em mente, a personalização desse fluxo foge do suporte usual do Facile XML-e, necessitando de um consultor para apoio ou análise de qualquer eventual problema, sendo necessário acionar o comercial da Facile Soluções em Sistemas.
