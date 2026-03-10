# 📅Dicionário de Dados

Segue documentação do dicionário de dados criado pela ferramenta.



## Tabela ZZW - Produto x Fornecedor XML-e

### Campos




<style>
</style>

| Campo      | Tipo | Tam. | Dec. | Descrição    | Completa                      |
| ---------- | ---- | ---- | ---- | ------------ | ----------------------------- |
| ZZW_FILIAL | C    | 2    | 0    | Filial       | Filial do<br> Sistema         |
| ZZW_FORNEC | C    | 6    | 0    | Fornecedor   | Codigo do<br> Fornecedor      |
| ZZW_LOJA   | C    | 2    | 0    | Loja         | Loja do<br> Fornecedor        |
| ZZW_NOMFOR | C    | 40   | 0    | Nome Fornec. | Nome do<br> Fornecedor        |
| ZZW_CODPRF | C    | 30   | 0    | Cod.Prod.For | Codigo do<br> Produto no Forn |
| ZZW_PRODUT | C    | 15   | 0    | Produto      | Codigo do<br> Produto         |
| ZZW_NOMPRO | C    | 40   | 0    | Descricao    | Nome do Produto               |
| ZZW_SEGUM  | C    | 2    | 0    | Seg.Uni.Med. | Segunda Unidade<br> de Medida |
| ZZW_CONV   | N    | 5    | 2    | Fator Conv.  | Fator Conversao               |
| ZZW_TIPCON | C    | 1    | 0    | Tipo de Conv | Tipo de<br> Conversao         |
| ZZW_DPRODF | C    | 90   | 0    | Desc.Prd.For | Descricao Prod<br> Fornecedor |
| ZZW_CLIFOR | C    | 1    | 0    | Cliente/Forn | Cliente ou<br> Fornecedor     |



### Índices

<style>
</style>

| **Ordem** | **Chave**                                                                 |
| --------- | ------------------------------------------------------------------------- |
| 1         | ZZW_FILIAL + ZZW_FORNEC + ZZW_LOJA + ZZW_CODPRF + ZZW_PRODUT              |
| 2         | ZZW_FILIAL + ZZW_FORNEC + ZZW_LOJA + ZZW_PRODUT                           |
| 3         | ZZW_FILIAL + ZZW_CLIFOR + ZZW_FORNEC + ZZW_LOJA + ZZW_CODPRF + ZZW_PRODUT |

### 

## Tabela ZZZ - Documentos Gerenciados

### Campos

<style>
</style>

| Campo      | Tipo | Tam. | Dec. | Descrição    | Completa                     |
| ---------- | ---- | ---- | ---- | ------------ | ---------------------------- |
| ZZZ_FILIAL | C    | 2    | 0    | Filial       | Filial do<br> Sistema        |
| ZZZ_SITDOC | C    | 1    | 0    | Sit. NF-e    | Situacao da Nota Fiscal      |
| ZZZ_TIPO   | C    | 1    | 0    | Tipo XML     | Tipo de XML                  |
| ZZZ_STATUS | C    | 1    | 0    | Manif. Atual | Status da Manifestacao       |
| ZZZ_DOC    | C    | 9    | 0    | Nota Fiscal  | Numero da Nota Fiscal        |
| ZZZ_SERIE  | C    | 3    | 0    | Serie        | Serie da Nota Fiscal         |
| ZZZ_EMISNF | D    | 8    | 0    | Emissao NF   | Data Emissao da NF           |
| ZZZ_CNPJ   | C    | 14   | 0    | CNPJ Fornece | CNPJ Fornecedor              |
| ZZZ_NOEMIT | C    | 60   | 0    | Nome/Razao   | Nome/Razao                   |
| ZZZ_CHAVE  | C    | 60   | 0    | Chave NF     | Chave da Nota Fiscal         |
| ZZZ_CODEVE | C    | 3    | 0    | Cod.Evento   | Status do Evento             |
| ZZZ_XML    | M    | 10   | 0    | XML          | XML                          |
| ZZZ_DTRECB | D    | 8    | 0    | Data Recebto | Data de Recebimento          |
| ZZZ_ORIGEM | C    | 1    | 0    | Origem XML   | Origem XML                   |
| ZZZ_OK     | C    | 4    | 0    | OK           | OK                           |
| ZZZ_VLDOC  | N    | 13   | 2    | Valor NF-e   | Valor NF-e                   |
| ZZZ_ANONFE | C    | 4    | 0    | Ano Emissao  | Ano Emissao NFe              |
| ZZZ_MESNFE | C    | 2    | 0    | Mes Emissao  | Mes Emissao da NFE           |
| ZZZ_IEEMIT | C    | 18   | 0    | Inscr. Est.  | Inscricao Estadual emitente  |
| ZZZ_DESRES | C    | 150  | 0    | Desc.Proces. | Descricao do Processamento   |
| ZZZ_CODRET | C    | 3    | 0    | Cod.Process. | Status da Resposta           |
| ZZZ_DTREC  | D    | 8    | 0    | Data Aut.    | Data recebimento             |
| ZZZ_UF     | C    | 2    | 0    | Estado       | Estado de Origem             |
| ZZZ_ENVMAI | C    | 1    | 0    | Mail Enviado | E-Mail Enviado               |
| ZZZ_NSU    | C    | 40   | 0    | NSU          | NSU                          |
| ZZZ_PEDCHK | C    | 1    | 0    | Ped. Checado | Pedido Compra verificado     |
| ZZZ_PEDOBS | M    | 10   | 0    | Obs Ped Comp | Observacao<br> Pedido Compra |
| ZZZ_YHORA  | C    | 5    | 0    | Hora         | Hora do download XML         |
| ZZZ_ECKDOC | C    | 1    | 0    | Email CkDoc  | Email Enviado pelo CKDoc     |
| ZZZ_PDF    | M    | 10   | 0    | Doc. PDF     | Documento PDF                |
| ZZZ_PROVID | C    | 50   | 0    | Provider     | Provedor de XML              |

### 

### Índices

<style>
</style>

| **Ordem** | **Chave**                                   |
| --------- | ------------------------------------------- |
| 1         | ZZZ_FILIAL + ZZZ_CHAVE                      |
| 2         | ZZZ_FILIAL + ZZZ_CNPJ + ZZZ_DOC + ZZZ_SERIE |
| 3         | ZZZ_FILIAL + ZZZ_DOC + ZZZ_SERIE + ZZZ_CNPJ |
| 4         | ZZZ_FILIAL + ZZZ_EMISNF + ZZZ_CNPJ          |

### 

## Tabela SD1 - Itens Documento de Entrada

### Campos

<style>
</style>

| Campo      | Tipo | Tam. | Dec. | Descrição    | Completa              |
| ---------- | ---- | ---- | ---- | ------------ | --------------------- |
| D1_ZPEDIDO | C    | 6    | 0    | Pedido Temp  | Pedido<br> Temporario |
| D1_ZITEMPD | C    | 4    | 0    | Item Temp    | Item Temporario       |
| D1_ZITEMOR | C    | 4    | 0    | Item Orig    | Item Original         |
| D1_ZNFIMP  | C    | 1    | 0    | NF Importada | NF Importada          |
| D1_ZITEXML | C    | 5    | 0    | Item no XML  | Item no XML           |



## Tabela SX6 - Parâmetros do Sistema

<style>
</style>

| **Parâmetros** | **Tipo** | **Descrição**                                                                     |
| -------------- | -------- | --------------------------------------------------------------------------------- |
| ZZ_ARMZPED     | L        | Informa se busca o Armazem do Produto no Pedido de Compras<br> (C7_LOCAL)         |
| ZZ_AUTHLOG     | C        | Nome de usuário fornecido pela Facile                                             |
| ZZ_AUTHPSW     | C        | Senha fornecida pela Facile                                                       |
| ZZ_CERTCA      | C        | Caminho do arquivo CA.PEM                                                         |
| ZZ_CERTKEY     | C        | Caminho do arquivo KEY.PEM                                                        |
| ZZ_CERTPRI     | C        | Caminho do arquivo CERT.PEM                                                       |
| ZZ_CIENAUT     | L        | Manifesta ciência da operação automaticamente?                                    |
| ZZ_CLASSIF     | L        | Ativa a abertura da classificação do documento automaticamente ao gerar pré-nota? |
| ZZ_CODEAUT     | L        | Ativa autenticação na Facile                                                      |
| ZZ_CONFAUT     | C        | Tipo de tratativa para transmissao da confirmacao da operacao                     |
| ZZ_CONFFIS     | L        | Ativa integração com o módulo ACD Protheus para conferência Cega pelo FACILE XML-e. Necessário também ativar o MV_CONFFIS.  |
| ZZ_CTECAUT     | L        | Ativa a importação automática do CTE de Compra                                    |
| ZZ_CTECSPE     | L        | Especie do CTE de compra na entrada. Caso não exista, é definido como CTE.        |
| ZZ_CTEVAUT     | L        | Ativa a importação automática do CTE de Venda                                     |
| ZZ_CTEVSPE     | L        | Especie do CTE de venda na entrada. Caso não exista, é definido como CTE.         |
| ZZ_DADOSB1     | L        | Busca dados contábeis no cadastro do produto.                                     |
| ZZ_DCTECP      | N        | Até quantos dias para trás deve buscar os CT-e de Compra                          |
| ZZ_DCTEVD      | N        | Até quantos dias para trás deve buscar os CT-e de Venda                           |
| ZZ_DEBUG       | L        | Ativa o modo Debug no console do appserver                                        |
| ZZ_DELMAIL     | L        | Deleta o e-mail da caixa de correio apos o download do XML?                       |
| ZZ_DESTFIS     | C        | Destinatarios para workflow de  mudanças de status das NFe                        |
| ZZ_FILATIV     | L        | Desabilita a baixa de determinada Filial no FACILE XML-e. Preencher como .F. para desativar a filial. |
| ZZ_GRPBLOQ     | C        | Id dos Grupos de Usuários autorizados a bloquear/desbloquear documentos, separados por barra. Ex.: 000001/000010/000025 |
| ZZ_IEZZZ       | L        | Faz a leitura do campo ZZZ_IEEMIT ao invés da leitura dinâmica do XML para realizar a validação na entrada das notas. |
| ZZ_MAILXML     | L        | Ativa busca de XML no e-mail                                                      |
| ZZ_MUDASE3     | L        | Possibilita o usuário de alterar a série da NFS-e no momento do lançamento        |
| ZZ_NFSEATV     | L        | Ativa o download da NFSE em ambiente nacional                                     |
| ZZ_NFSEAUT     | L        | Ativa a importação automática da NFS-e                                            |
| ZZ_NFSESER     | C        | Altera a série padrão das NFS-e. **Importante:** Só utilizará a série personalizada caso não exista série no XML da NFS-e. |
| ZZ_NFSESPE     | C        | Altera a espécie padrão das NFS-e                                                 |
| ZZ_OPERNFS     | C        | Tipo de operação para busca de TES Inteligente na NFSe                            |
| ZZ_OPERCOM     | C        | Tipo de operação para entrada normal                                              |
| ZZ_OPECTEC     | C        | Tipo de operação para busca de TES Inteligente no CTE                             |
| ZZ_OPECTEV     | C        | Tipo de operação para busca de TES Inteligente no CTE                             |
| ZZ_OPERTRA     | C        | Tipo de operação para transferências                                              |
| ZZ_PCCTE       | L        | Ativa a solicitação de pedido de compras na entrada de CTE de Venda               |
| ZZ_PCOBRIG     | L        | Obrigatório vincular pedido de compra em todos os itens                           |
| ZZ_POPCNT      | C        | Conta de e-mail para conexão POP                                                  |
| ZZ_POPEND      | C        | Endereco do servidor POP de e-mail                                                |
| ZZ_POPPSW      | C        | Senha da Conta de e-mail para conexão POP                                         |
| ZZ_POPSSL      | L        | Utiliza conexao segura para acesso POP ao e-mail                                  |
| ZZ_PRODCTE     | C        | Produto padrão para entrada de CT-e                                               |
| ZZ_PSWENTR     | C        | Senha que autoriza entrada com divergência de impostos                            |
| ZZ_TESCTE      | C        | TES padrão para entrada de CT-e                                                   |
| ZZ_TESCTEC     | C        | TES padrão para entrada de CT-e de Compra                                         |
| ZZ_TIMEUPD     | N        | Tempo de refresh da tela de gestão à vista (minutos)                              |
| ZZ_ULTNSU      | C        | Ultimo NSU de busca para NFe                                                      |
| ZZ_UPDEAN      | L        | Atualiza o EAN no campo B1_CODBAR de acordo com o XML                             |
| ZZ_VERSAOM     | C        | Versão do webservice Sefaz                                                        |
| ZZ_VLDCEST     | L        | Ativa a validacao do CEST                                                         |
| ZZ_VLDCOFI     | L        | Ativa validação de COFINS na classificação                                        |
| ZZ_VLDICMS     | L        | Ativa validação de ICMS na classificação                                          |
| ZZ_VLDIPI      | L        | Ativa validação de IPI na classificação                                           |
| ZZ_VLDNCM      | C        | Regra de validação de NCM na classificação                                        |
| ZZ_VLDNFE      | L        | Desativa (.T.) a tela de confronto de dados entre XML e ERP                       |
| ZZ_VLDPIS      | L        | Ativa validação de PIS na classificação                                           |
| ZZ_VLDST       | L        | Ativa validação de ICMS ST na classificação                                       |
| ZZ_XMLAUTO     | L        | Informa se irá baixar o XML automaticamente via JOB                               |

