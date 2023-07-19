<style>
    p{
        text-align: justify;
    }
</style>

# Entrada em Lote

## Objetivo

Facilitar a entrada massiva de: Pré-notas e Documento de Entrada, sempre que, exista previamente o cadastro de fornecedores, e a ralação de produtos x fornecedor na Central XML.

*Observação: A rotina usa os XML´s baixados.*

Para utilizar a funcionalidade, acesse a central xml-e devidamente configurada em seu menu no Protheus e selecione: **Central Xml > Outras Ações > Entrada em Lote.**

- Como na imagem abaixo:

<center>![Figura 1: Opção entrada em lote](../../assets/entrada-lote/01-outras-ac.png "Opção entrada em lote")
<br>*Figura 1: Opção entrada em lote*<br></center>
<br>

## Definir os filtros para receber os XMLs

<center>![Figura 2: Tela de Parâmetros](../../assets/entrada-lote/02-param.png "Tela de Parâmetros")
<br>*Figura 2: Tela de Parâmetros*<br></center>
<br>

- **Filial de; até:** Selecionar a filial;
- **Documento de; até:** Números de documentos de entrada;
- **Serie de; até:** Séries dos documentos de entrada;
<br><br>

<center>![Figura 3: Tela de Parâmetros](../../assets/entrada-lote/03-param.png "Tela de Parâmetros")
<br>*Figura 3: Tela de Parâmetros*<br></center>
<br>

- **CNPJ de; até:** CNPJ´s dos fornecedores – numérico sem formatação-;
- **Emissão de; até:** Datas das entradas das notas;
- **Tipo de Documento:** Nf-e ou CT-e;
<br><br>

Caso os filtros não encontrem concordância com os dados no sistema (datas, documentos, cnpj e etc.), será apresentada a tela abaixo.

<center>![Figura 4: Erro nos filtros dos Parâmetros](../../assets/entrada-lote/04-alerta-recno.png "Erro nos filtros dos Parâmetros")
<br>*Figura 4: Erro nos filtros dos Parâmetros*<br></center>
<br>

***Nessa situação, refaça os filtros e tente de novo.***

Após fazer o passo anterior você verá uma nova tela com os XML´s.

<center>![Figura 5: Pré-Nota em Lote](../../assets/entrada-lote/05-prenota.png "Pré-Nota em Lote")
<br>*Figura 5: Pré-Nota em Lote*<br></center>
<br>

Para selecionar todos os xmls, é necessário apertas duas vezes na coluna em amarelo, agora, se quer selecionar os xmls individualmente, é necessário apertar duas vezes cada quadradinho referente a cada xml.

## Gerar Pré-Nota

Após selecionar os xmls que deseja, clicar em "Gerar Pré-nota".

<center>![Figura 6: Resultado do Processamento em Lote](../../assets/entrada-lote/06-resumo.png "Resultado do Processamento em Lote")
<br>*Figura 6: Resultado do Processamento em Lote*<br></center>
<br>

Foi gerada a pre-nota..!

Em seguida, fechar a tela de entrada em lote e sair da rotina Central-xml para atualizar o status.

<center>![Figura 7: Tela Principal da Central XML-e com as Legendas](../../assets/entrada-lote/07-legenda.png "Tela Principal da Central XML-e com as Legendas")
<br>*Figura 7: Tela Principal da Central XML-e com as Legendas*<br></center>
<br>

Essa nota fica com amarelo: “documento com pré-nota”

Acessse a rotina padrão “Pre Nota Entrada”, e verifique que já esta essa nota.

*OBS.: pode excluir a prenota e repetir o processo em lote.*

## Gerar Documento de Entrada

Ao apertar o botão "Gerar Doc. Entrada", aparecerá a tela abaixo.

<center>![Figura 8: Informar TES e Condição de Pagamento](../../assets/entrada-lote/08-ptx0035b-dados.png "Informar TES e Condição de Pagamento")
<br>*Figura 8: Informar TES e Condição de Pagamento*<br></center>
<br>

Informar TES e condição de Pagamento.

***<span style="color: red">OBS.: Esta rotina dara entrada em notas, sem considerar obrigatoriedade de pedidos de compra.</span>***
***<span style="color: red">Só recomendada para entradas de notas com a mesma TES e condição de pagamento.</span>***

Mostra a tela confrontando os dados de impostos do XML, e o que esta calculando nas configuraçoes de impostos do Protheus.

<center>![Figura 9: Confronto de dados de impostos do XML](../../assets/entrada-lote/09-confronto-xml.png "Confronto de dados de impostos do XML")
<br>*Figura 9: Confronto de dados de impostos do XML*<br></center>
<br>

Se tiver inconsistencias, vai avisar se deseja mesmo assim, dar entrada na nota. Só podera dar entrada se tiver a senha que autoriza.

*Obs: no cabeçaho de totais, mostra os impostos procipais, e no detalhe, mostra as divergencias ou não,  por item (use a barra de rolagem)*

Após “SALVAR”, pode verificar na rotina padrao protheus: “Documanto de Entrada”, a nota de entrada.

## Erros nos processos, Gerar Pré-Nota e Gerar Documento de Entrada

<center>![Figura 10: Possíveis erros na Entrada em Lote](../../assets/entrada-lote/10-resultado.png "Possíveis erros na Entrada em Lote")
<br>*Figura 10: Possíveis erros na Entrada em Lote*<br></center>
<br>

Caso o xml esteja sem vinculo com dados do Portheus, por exemplo: Fornecedor ou codigo de produto ralacionado. 

Sera apresentado o aviso de erro.

<div style="text-align: center; font-weight: bold;">-FIM-</div>