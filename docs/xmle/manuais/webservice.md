<style>
    p{
        text-align: justify;
    }
    #format{
        font-style: italic; 
        font-size: 15px;
    }
    #green{
        background-color: #16F529;
        color: black;
    }
    #red{
        background-color: red;
        color: black;
    }
    #yellow{
        background-color: yellow;
        color: black;
    }
    b{
        color: red;
    }
</style>

# Manual de configuração do Webservice Checkdoc

## Introdução

O objetivo de configurar um Webservice para o CheckDoc é realizar uma análise <b>AUTOMÁTICA</b> do XML recebido do Sefaz e verificar no ERP Protheus® se as informações contidas nele estão corretas.

Será verificado:

- Abertura do HTML do Checkdoc por link no e-mail;

## Como usar?

Após a configuração, será enviado automaticamente para o(s) e-mail(s) cadastrado(s) no parâmetro: <b>ZZ\_ECKDOC</b> - Parâmetros com e-mails separados por (;)


## Detalhamento dos Serviços / Observações

Atividades incluídas:

* Viabilizar a abertura e exibição das informações registradas com base na execução, através do hyperlink que passa a ser formatado sob a chave que corresponde à uma das colunas do e-mail com as informações, da apuração checkdoc.

* Agregar às informações do e-mail de divergência emitido pós apuração checkdoc. 


## Informações técnicas relevantes

Parâmetros envolvidos:

* <b>ZZ\_PATHWS</b> - Parâmetro para registro do path no Protheus\_Data, do webservice, onde serão gerados os arquivos. 

**Exemplo:** \web\facile\_checkdoc

* <b>ZZ\_DFWEBS</b> - Parâmetro para registro da url do serviço HTTP/HTTPS do Protheus, direcionado à pasta onde estarão salvos os arquivos e que será utilizado para carga do arquivo em navegador web (browse). 

**Exemplo:** [http://192.168.200.171:8079/facile\_checkdoc/](http://192.168.200.171:8079/facile\_checkdoc/)

* <b>ZZ\_ECKDOC</b> - Parâmetros com e-mails que irão receber, separados por (;)

**Exemplo:** compras@nomedaempresa.com.br;outroemail@nomedoemail.com.br 


**ATENÇÃO**: É necessário que a funcionalidade **HTTP** do Protheus esteja configurada e em execução para o correto funcionamento dessa rotina.


## Configuração do webservice Checkdoc

### Appserver\_FACILE.ini

Incluir no serviço Appserver.ini destinado ao FACILE XML-e (normalmente nomeado como appserver\_Facile.ini, Appserver01...), na pasta do serviço do Facile XML-e, o job <span style="color: red">PTXJ005</span>.

Ex. (<span style="color: red">em vermelho</span>)

<b>AppServer01:</b>

    ;;Job Responsável pelo Workflow do Checkdoc
    [PTXJ005]
    MAIN=U_PTXJ005
    ENVIRONMENT=FACILE
    nparms=2
    Parm1=01
    Parm2=0101

    ;;Tag responsável por inicializar e controlar os jobs
    [ONSTART]
    JOBS=PTXJ001,PTXJ003,PTXJ008,PTXJ005
    REFRESHRATE=4000

**O que significa cada TAG?**

**ENVIRONMENT**     => Ambiente que o JOB será executado                                <br>
**MAIN**  		    => Nome do programa a ser chamado                                   <br>
**nparms** 		    => Quantidade de parâmetro a serem utilizados                       <br>
**Parm1**		    => Informe o código da Empresa                                      <br>
**Parm2**		    => Informe o código da Filial                                       <br>
**REFRESHRATE**	    => Intervalo de tempo, em segundos, para que o Job seja executado   <br>

Com base na execução da rotina JOB, integrante do FACILE XML-e, para apuração de divergências nos registros identificados, passa a ser formatado um arquivo contendo as informações da apuração.

Este arquivo é registrado em diretório específico ligado ao webservice – Protheus®.

![Figura 01: Diretório Webservice](../../assets/webservice/ws_direweb.png "Diretório Webservice"){: .center-img }
<span class="format">Figura 01: Diretório Webservice</span>

Ao receber o e-mail contendo as informações de divergência, passe-se a observar e ter a ação de click na coluna: Chave.

Ao clicar na informação, será aberto – em navegador WEB (browse), o arquivo contendo as informações apuradas.

![Figura 02: Divergência encontrada](../../assets/webservice/ws_divenc.png "Divergência encontrada"){: .center-img }
<span class="format">Figura 02: Divergência encontrada</span>

Ao clicar em um dos links abrirá sua consulta:

![Figura 03: Consulta da divergência](../../assets/webservice/ws_consulta.png "Consulta da divergência"){: .center-img }
<span class="format">Figura 03: Consulta da divergência</span>


## Workflow de notificação Checkdoc

### Resumo

1. Enviar workflow com todas as chaves que estão com divergência no CheckDoc e ainda não foram corrigidas;
2. Criar parâmetro para definir data inicial da busca.

### Detalhamento dos Serviços

Atividades incluídas

*  Possibilitar que os usuários envolvidos sejam constantemente lembrados dos problemas nas notas fiscais que precisam ser corrigidos

### Informações técnicas / Relevantes

Parâmetros envolvidos:

* <b>ZZ\_CHKRETR</b> - Parâmetro numérico informando a quantidade de dias será retrocedido para buscar as notas fiscais que continuam com falha no CheckDoc.

**Exemplo**: 30

### Passo a passo

O workflow será enviado através do job **PTXJ005**, que hoje já é utilizado para realizar a primeira checagem do CheckDoc das notas fiscais baixadas do Sefaz.

Para desativar o envio do workflow basta configurar o parâmetro **ZZ\_CHKRETR** com o valor 0 (zero).

<div style="text-align: center; font-weight: bold;">-FIM-</div>
