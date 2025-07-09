# 📝Notas de Versão

Detalhes das atualizações liberadas da ferramenta.

### Versão 4.33.5072

09/07/2025

- BUG: Correção na busca de fornecedor considerando a inscrição estadual
- BUG: Não considerar pedidos rejeitados
- MELHORIA: Aumento do campo ZZZ_IEEMIT para 18 caracteres

### Versão 4.33.5071

27/06/2025

- MELHORIA: Melhorada a estilização das telas durante a utilização do DarkTheme
- MELHORIA: Incrementado tela de devolução para exibir lote e data de validade
- MELHORIA: Adicionado possibilidade de utilizar a Inscrição Estadual do emitente na busca do fornecedor no ERP
- BUG: Correção da valição não estava permitindo a entrada na alimentação do grid para notas de serviço
- BUG: Ajuste no CTE de compra para posicionar corretamente na SF1 após o execauto
- BUG: Configurado para quando a rejeição da manifestação for por duplicidade a ferramenta entenda que foi vinculado corretamente aquele evento
- BUG: Correção na impressão de impostos na NFS-e

### Versão 4.33.5070

31/03/2025

- MELHORIA: Impressão da DANFSe (Nota Fiscal de Serviço) importadas via WebService de prefeituras
- MELHORIA: Incluído funcionalidade de lançamento de CTE de Venda complementar
- MELHORIA: Adicionado o monitoramento em seguida a manifestação
- MELHORIA: Incluído entrada de NF-e de complemento de IPI
- MELHORIA: Criado ponto de entrada CHECKPED para informar o pedido de compra na execução do CheckDoc
- MELHORIA: Criado novo JOB no CheckDoc para reprocessar as análises sem o envio do workflow
- BUG: Corrigido erro de variável inválida ao buscar os dados do CTE Completo
- BUG: Correção na atualização da legenda após a transmissão da confirmação da operação

### Versão 4.33.5069

31/01/2025

- MELHORIA: Criado parâmetro ZZ_CTEOSPE para indicar a especie (F1_ESPECIE) a ser utilizada na entrada do CTE
- MELHORIA: Incluído data de fabricação da devolução de venda
- MELHORIA: Disponibilizando a funcionalidade para cadastro de fornecedor para as NF-e, e ampliando para disponibilizar a mesma automação para clientes
- MELHORIA: Impressão da DANFSe (Nota Fiscal de Serviço)
- BUG: Correção para desbloquear o documento após transmitir a confirmação da operação.
- BUG: Ajuste para CTE Complementar de compra

### Versão 4.33.5068

**Para essa versão, favor executar o compatibilizador apropriado para o seu ambiente.**

04/12/2024

- MELHORIA: Novo campo para identificar o tipo de documento na tabela ZZZ
- MELHORIA: Novo campo para identificar se a NF é de Entrada ou Saída do fornecedor
- MELHORIA: Refatorado o html do e-mail de documentos cancelados para ficar mais leve e clean
- MELHORIA: Somente atualizar o status da manifestação (ZZZ_STATUS) quando for aceito pelo Sefaz entrando no Monitorar
- MELHORIA: Informação do CFOP no relatório de documentos
- MELHORIA: Inclusão da baixa dos XMLs do CTEOS
- BUG: Correção no relatório de documentos PTXR008 na busca da UF do fornecedor

### Versão 4.33.5067

28/10/2024

- MELHORIA: Incluído opção de estornar a classificação da NF-e
- MELHORIA: Incluído mais opções de filtro na rotina de monitoramento da manifestação
- BUG: Incluído as informações complementares do CT-e no DACTE
- BUG: Correção no "Buscar Sefaz" do CT-e
- BUG: Passar a tratar o tipo de CT-e para imprimir o DACTE

### Versão 4.33.5066

18/09/2024

- MELHORIA: Incluído o ponto de entrada PX011CTE também na rotina de entrada automática de CTE
- MELHORIA: Adicionado a funcionalidade de importação de NF-e de complemento de ICMS
- MELHORIA: Adicionado a informação da UF do fornecedor no relatório de status das NF-e
- BUG: Mudança na URL da prefeitura de Cachoeiro de Itapemirim
- BUG: Removido validação de status do documento ao acessar rotina de exportar XML
- BUG: Correção na atualização da legenda após excluir um CTE de Compras lançado
- BUG: Correção no primeiro painel do gestão a vista (Notas não classificadas)
- BUG: Correção para liberar o bloqueio de entrada de documento quando é realizado a manifestação da confirmação da operação

### Versão 4.33.5065

01/08/2024

- BUG: Ajustes no checkdoc para ambiente Oracle
- BUG: Correção na legenda para NF de operação não realizada
- BUG: incluído código do item no execauto da NF-e
- MELHORIA: Inclusão da busca de NFS-e direto na prefeitura de Uberaba-MG

### Versão 4.33.5064

26/06/2024

- MELHORIA: Criado parametro ZZ_CTECBLQ para bloquear entrada de CTE de Compra quando tiver NF vinculada que ainda não está classificada
- MELHORIA: Funcionalidade para exportar as DANFE/DACTE em lote
- MELHORIA: Desenvolvido função U_PTX0060_Importa_Xml(cStringXml) para importar uma NF-e ou CT-e passando diretamente a string do XML, mantendo o padrão da ferramenta
- MELHORIA: Alterado para não abrir tela de amarração ao cancelar a tela de tipo de documento
- BUG: Correção no compatibilizador para criar o campo D1_ZNFIMP e F1_ZNFIMP

### Versão 4.33.5063

06/06/2024

- MELHORIA: Criado campo F1_ZNFIMP para informar que o documento foi importado pelo Facile XML-e

### Versão 4.33.5062

22/05/2024

- BUG: Corrigido francionamento para NFS-e
- BUG: Incluído tratativa de pedido por fornecedor vinculado na busca avançada de produtos
- BUG: Incluído preenchimento do campo D1_ZNFIMP na entrada dos CTE
- BUG: Ajuste na tela de confronto de impostos para melhor visualização em resoluções menores

### Versão 4.33.5061

23/04/2024

- MELHORIA: Criado workflow para envio de e-mail avisando ao comprador quando o pedido de compras dele der entrada pela NF (parâmetro ZZ_AVISENT = .T.)
- BUG: Corrigido busca na SF1 para NFS-e na opção de excluir o documento

### Versão 4.33.5060

03/2024

- BUG: Corrigido para não importar XML do computador que não possui assinatura digital
- MELHORIA: Criado ponto de entrada P07GERAENT que é chamado ao clicar no botão "Gerar Entrada"
- MELHORIA: Criado ponto de entrada P018SF1 para manipular o array de cabeçalho da NFe
- BUG: Correção no sequencial de NSU para NFS-e Nacional

### Versão 4.33.5059

27/02/2024

- BUG: Correção de variável na entrada em lote
- MELHORIA: Informação do vencimento da primeira parcela na tela de entrada de CTE de Compras
- BUG: Correção para não apresentar a tela de manifestação quando configurado para manifestar a confirmação automaticamente

### Versão 4.33.5058

12/01/2024

- MELHORIA: Incluido no ponto de entrada SAVEZZZ a informação se o documento já existia na ZZZ
- MELHORIA: Relatório de status dos documentos
- MELHORIA: Possibilidade de desativar a verificação do IPI quando a CST for 99

### Versão 4.33.5057

04/12/2023

- BUG: Ajuste para impressão da Danfe quando não há a chave da NFE da referenciada
- MELHORIA: Criação de nova legenda para pré-nota bloqueada para conferência fisica
- MELHORIA: Fracionamento automático de acordo com os lotes do produto
- BUG: Corrigido vinculo com pré-nota de transferência

### Versão 4.33.5056

09/11/2023

- BUG: Correção para importação de CTE com CPF no destinatário
- MELHORIA: Incluído possibilidade de informar o range de data para buscar a NF referenciada no CTE de compra
- MELHORIA: Alterado a Busca CTE Sefaz manual utilizando o novo processo de download de CTEs

### Versão 4.33.5055

19/10/2023

- MELHORIA: Rotina para importar vários XMLs do computador simultaneamente

### Versão 4.33.5054

06/10/2023

- MELHORIA: Criado parametro ZZ_BUSCAPC para deixar já marcado a pesquisa de produtos com pedido de compra
- MELHORIA: Incluído o XML dos parametros do ponto de entrada P018COLS

### Versão 4.33.5053

18/09/2023

- MELHORIA: Alterado para não precisar do Parm2 para realizar a autenticação dos JOBs
- BUG: Removido a busca da logo da empresa na impressão do DACTE
- MELHORIA: Inclusão de entrada de CT-e de compras referenciado a beneficiamento e devolução


### Versão 4.33.5052

28/08/2023

- MELHORIA: Criado dois parâmetros para alterar a data de busca dos CTEs de compra (ZZ_DCTECP) e dos CTEs de venda (ZZ_DCTEVD) na rotina de classificação automática
- BUG: Removido as NFS-e do primeiro painel do gestão a vista, será desenvolvido um painel própria para a NFS-e

### Versão 4.33.5051

14/08/2023

- BUG: Tratativa no relatório de entradas para a NFS-e
- MELHORIA: Incluído download da NFS-e Nacional via webservice
- BUG: Ajuste automático do tamanho do campo do Código do Produto do Fornecedor

### Versão 4.33.5050

27/07/2023

- MELHORIA: Criado ponto de entrada PTXF1SER para manipular a série dos documentos
- MELHORIA: Inclusão de novos campos na entrada da NFS-e

### Versão 4.33.5049

21/07/2023

- BUG: Corrigido importação de CTE de compra com amarração em NF de importação (formulário próprio)

### Versão 4.33.5048

14/07/2023

- MELHORIA: Incluído o código do cliente/fornecedor na tela de gerar entrada
- MELHORIA: Incluído opção de pesquisa e filtro na tela de amarração de produtos x fornecedor

### Versão 4.33.5047

14/07/2023

- MELHORIA: Incluído a informação de UF e município de origem/destino ativando parâmetro ZZ_UFTRANS
- MELHORIA: Incluído a informação do Tipo de Frete na entrada de NF-e
- MELHORIA: Melhorado para que no CTE ao informar a TES seja sempre em letras maiúsculas
- MELHORIA: Inclusão da opção de "Formato de Tabela" na impressão de relatório de CTEs


### Versão 4.33.5046

14/07/2023

- BUG: Correção na paginação para download de NFS-e


### Versão 4.33.5045

11/07/2023

- MELHORIA: Alterado função de filtro do browse para não perder a funcionalidade de filtrar a tela


### Versão 4.33.5044

07/07/2023

- MELHORIA: Criado ponto de entrada PTX01FIL que permite filtrar o browse de documentos XMLs

### Versão 4.33.5043

07/07/2023

- BUG: Ajuste na série para buscar a NFe para classificar
- BUG: Ajuste para não enviar o campo do IPI quando for zerado


### Versão 4.33.5042

03/07/2023

- MELHORIA: Incluído informação do Tipo de Frete na rotina de Entrada em Lote
- BUG: Correção na busca por pedido de compra


### Versão 4.33.5041

27/06/2023

- MELHORIA: Desenvolvido novo JOB para realizar a manifestação e download de XMLs que ficaram pra trás


### Versão 4.33.5040

23/06/2023

- BUG: Mudança no nome do objeto da tela para evitar conflito com o padrão (PTX0018)
  
### Versão 4.33.5039

20/06/2023

- BUG: Alterado forma de ler o IPI do XML no confronto para casos em que não possui base e aliquota, mas possui valor de IPI
- MELHORIA: Incluido a informação de total da NF na tela de confronto de impostos

### Versão 4.33.5038

16/06/2023

- BUG: Correção na conversão de unidade de medida padrão do Protheus
- BUG: Correção na validação de NF-e antes do ponto de entrada P018PROPRIO

### Versão 4.33.5037

10/06/2023

- BUG: Correção na impressão do valor do ICMS na Danfe
- MELHORIA: Impressão de DACTE direto na pasta

### Versão 4.33.5036

29/05/2023

- BUG: Correção nos JOB para ignorar as filiais com o parâmetro ativo (ZZ_FILATIV)
- BUG: Correção na opção de classificar pré-nota quando não encontra o documento na SF1
- BUG: Correção na tela de gestão a vista para banco de dados Oracle

### Versão 4.33.5035

15/05/2023

- BUG: Correção da falha ao encontrar a NFS-e na rotina de classificação
- BUG: Alterado o CONCAT no gestão a vista para compatibilizar com versão antiga do SQL Server

### Versão 4.33.5034

12/05/2023

- BUG: Correção em novo de user function para evitar duplicidade

### Versão 4.33.5033

09/05/2023

- MELHORIA: Criado ponto de entrada PTCTEDAD para permitir manipular os dados do CTE antes do lançamento
- BUG: Correção na entrada de NFS-e

### Versão 4.33.5032

02/05/2023

- BUG: Correção no endereço do tomador para prefeitura de SP
- MELHORIA: Criado ponto de entrda PTCLIFOR para que seja possível customizar a busca de cliente/fornecedor

### Versão 4.33.5031

23/04/2023

- MELHORIA: Adicionado a importação automática de NFS-e via webservice para a prefeitura de Cariacica/ES
- MELHORIA: Criado parametro ZZ_MUDASE3 para ativar a possibilidade do usuário mudar a série da NFS-e no momento do lançamento
- BUG: Correção na exclusão de NFS-e

### Versão 4.33.5030

11/04/2023

- BUG: Ajustes em mensagens de CTE
- BUG: Tratamento para CTE de Complemento
- MELHORIA: Reestruturado para entrada de mais prefeituras

### Versão 4.33.5029

30/03/2023

- BUG: Corrigido para não considerar NF-e de devolução no CheckDoc
- BUG: Corrigido erro ao exportar XMLs

### Versão 4.33.5028

29/03/2023

- MELHORIA: Adicionado a importação automática de NFS-e via webservice para a prefeitura de Nova Friburgo/RJ
- MELHORIA: Adicionado a importação automática de NFS-e via webservice para a prefeitura de Ipatinga/MG
- MELHORIA: Incluido informação de vencimento de certificado na tela principal
- MELHORIA: Adicionado a importação de Lote, Fabricação e Vencimento para produtos que controlam lote (B1_RASTRO igual a L ou S)
- BUG: Correção para importação de PDF de NFS-e contendo mais de um item de serviço
- BUG: Correção na transmissão automática da confirmação da operação quando utiliza a opção Classificar NF-e

### Versão 4.33.5027

28/03/2023

- MELHORIA: Adicionado a importação automática de NFS-e via webservice para a prefeitura de Cachoeiro de Itapemirim/ES

### Versão 4.33.5026

27/03/2023

- MELHORIA: Adicionado botão para exclusão da amarração produto x fornecedor na tela principal de entrada
- MELHORIA: Ajuste na mensagem de XML não baixado para orientar melhor o usuário
- BUG: Corrigido relatório para informação da NFS-e na coluna TIPO

### Versão 4.33.5025

20/03/2023

- BUG: Corrigido tratamento para formatos de datas diferentes

### Versão 4.33.5024

17/03/2023

- BUG: Corrigido importação da SA5 que estava duplicando registros
- MELHORIA: Criado ponto de entrada P018ZZW para ações após inclusão da amarração produto x fornecedor

### Versão 4.33.5023

16/03/2023

- BUG: Correção no controle de horário de execução do JOB
- BUG: Configurado para o Busca Avançada Sefaz desconsiderar filiais inativas
- MELHORIA: Incluído na exportação de XML a opção para exportar CTe e NFe juntos

### Versão 4.33.5022

01/03/2023

- MELHORIA: Criado ponto de entrada que permite utilizar formulário próprio P018PROPRIO

### Versão 4.33.5021

24/02/2023

- BUG: Correção na geração da DANFE

### Versão 4.33.5020

15/02/2023

- BUG: Correção na importação de PDF para appserver no linux e versão 12.1.27

### Versão 4.33.5019

09/02/2023

- MELHORIA: Ponto de entrada para manipular a ZZZ após gravação: SAVEZZZ
- BUG: Ajuste no execauto da MATA116 para que ainda está com a rotina desatualizada (criado parametro ZZ_OLDM116)

### Versão 4.33.5018

04/02/2023

- MELHORIA: Desenvolvido busca de NFS-e na prefeitura de SP via WebService
- BUG: Corrigido importação de XML do computador para CPF

### Versão 4.33.5017

25/01/2023

- MELHORIA: Criado novo campo a ser utilizado pela NFS-e

### Versão 4.33.5016

23/01/2023

- BUG: Corrigido status do CTE

### Versão 4.33.5015

19/01/2023

- BUG: Corrigido falha ao alterar pré-nota de NF-e

### Versão 4.33.5014

18/01/2023

- NOVIDADE: Criado relatório para Gestão de CTE de Venda

### Versão 4.33.5013

17/01/2023

- BUG: Corrigido erro ao realizar entrada em lote

### Versão 4.33.5012

16/01/2023

- NOVIDADE: Permite classificar CTE diretamente da Central XML-e
- NOVIDADE: Criado ponto de entrada P09ALTPN para controlar quem pode classificar a NFE e CTE

### Versão 4.33.5011

13/01/2023

- NOVIDADE: Criado a tabela FACX003 para gestão dos CTEs
- NOVIDADE: Incluído importação de CTE no controle de NSUs (FACX002)
- NOVIDADE: Criado ponto de entrada P018COLS para manipular o aCols do documento de entrada antes do execauto
- BUG: Correção na importação de NFe onde o destinatário é CPF
- BUG: Correção para exclusão de pré-nota de CTE diretamente da Central XML-e
- BUG: Correção no congelamento ao dar entrada em CTE
- BUG: Corrigido peso bruto e liquido na DANFE

### Versão 4.33.5010

04/01/2022

- NOVIDADE: Criado novo compatibilizador único para dicionário na System (U_UPDXSYS)

- BUG: Incluído novas validações ao importar NFS-e via PDF

### Versão 4.33.5009

22/12/2022

- NOVIDADE: Incluído nova tabela para registrar todos os NSUs

- NOVIDADE: Desenvolvido para salvar os NSUs das NF-e

- NOVIDADE: Denvolvido classe e JOB para buscar no sefaz os NSUs faltantes

- NOVIDADE: Criado tela para demonstrar a carta de correção

### Versão 4.33.5008

22/12/2022

- NOVIDADE: Incluído a informação do armazém do pedido na tela principal de entrada de doc.

- NOVIDADE: Incluído opção de visualizar, alterar e excluir pré-nota

- NOVIDADE: Incluído opção de visualizar e excluir documento de entrada

- BUG: Removido os documentos bloqueados dos relatórios

### Versão 4.33.5007

22/12/2022

- NOVIDADE: Criado ponto de entrada P011ITEM para manipular os itens da SD1 no CTE de venda

### Versão 4.33.5006

21/12/2022

- NOVIDADE: Incluído campo Tipo de Produto no filtro de regras por processo

### Versão 4.33.5005

19/12/2022

- NOVIDADE: Finalizado a primeira versão da importação automática do CTE de venda

### Versão 4.33.5004

16/12/2022

- BUG: Correção na descrição do produto na tela de entrada

- BUG: Tratativa para não permitir XML sem filial

### Versão 4.33.5003

08/12/2022

- NOVIDADE: Cria parametro para permitir grupos de usuários a bloquear entrada de documento

- NOVIDADE: Incluído informação da unidade de pedido do XML, produto e pedido de compras na tela de entrada

### Versão 4.33.5002

01/12/2022

- BUG: Correção na geração da devolução de venda

### Versão 4.33.5001

01/12/2022

- NOVIDADE: Implantado melhoria de importação de NFS-e

### Versão 4.33.5000

22/11/2022

- NOVIDADE:  Entrada de beneficiamento

- NOVIDADE:  Bloqueio de entrada

- NOVIDADE:  Nova legenda

### Versão 4.33.1042

10/11/2022

- Ajuste no PTX008 para o ponto de entrada de numero de documento

### Versão 4.33.1041

09/11/2022

- Correção no execauto do CTE (MATA116) após atualização da Totvs

### Versão 4.33.1040

08/11/2022

- Correção no busca quando a empresa utiliza CPF no sigamat

- Correção no PTX0008 para utilizar a nova rotina de numero de documento

### Versão 4.33.1039

03/11/2022

- Criado ponto de entrada P007CTE

### Versão 4.33.1038

01/11/2022

- Ajuste na ordenação da SD1 quando possui conversão de unidade de medida

### Versão 4.33.1037

28/10/2022

- Removido validação de cnpj raiz nos jobs

### Versão 4.33.1036

26/10/2022

- Criado parametro ZZ_ORDEDIC para indicar se deve ordenar o array de itens de acordo com a SD1

### Versão 4.33.1035

24/10/2022

- Correção no update das legendas

- Correção na criação de arquivos de logs

### Versão 4.33.1034

20/10/2022

- Criação de ponto de entrada XCarregDados para alterar a filial de destino do XML

### Versão 4.33.1033

14/10/2022

- Correção na função de validação de impostos

### Versão 4.33.1032

13/10/2022

- Melhoria para gravar na ZZW a descrição do produto que vem no XML

### Versão 4.33.1031

11/10/2022

- Correção na impressão do CTE na tag CEP

- Melhoria para preencher o campo D1_DFABRIC através da tag dFab

### Versão 4.33.1030

05/10/2022

- Ajuste no checkdoc automático e workflow

### Versão 4.33.1029

30/09/2022

- Melhoria no checkdoc para incluir filial e cnpj no assunto do workflow

- Considerar pedido de compras faltando zeros a esquerda no xPED

- Melhorado processo dos JOBS para controle de semaforo e logs

### Versão 4.33.1028

26/09/2022

- Correção na query de exportação de XML para banco de dados Oracle

### Versão 4.33.1027

14/09/2022

- Corrigido erro após incluir novas colunas no grid de pedido de compras

### Versão 4.33.1026

11/09/2022

- Melhoria incluindo valores do pedido de compra

### Versão 4.33.1025

06/09/2022

- Incluído tratamento de serie 3 digitos para CTE

### Versão 4.33.1024

01/09/2022

- Alterado para não exportar XML de documento cancelado
