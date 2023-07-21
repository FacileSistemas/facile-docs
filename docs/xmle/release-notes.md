# 📝Notas de Versão

Detalhes das atualizações liberadas da ferramenta.

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
