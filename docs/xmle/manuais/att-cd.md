<style>
    p{
        text-align: justify;
    }
    #yellow{
        background-color: yellow;
        display: inline;
    }
</style>

# Atualização do Certificado Digital

## Passo a Passo

### Observações iniciais

Importação do certificado digital para comunicação com o SEFAZ.

**Importante:** O arquivo do certificado digital precisa estar no mesmo computador que estiver realizando o procedimento, seja na estação do usuário ou no servidor.

<div id="yellow">***OBSERVAÇÃO:***	Caso o seu usuário tenha acesso a várias filiais na mesma tela (múltiplas filiais no browse), é necessário estar com a FILIAL a ser atualizada filtrada no browse para que o certificado seja vinculado corretamente a filial!</div>

### Passo 01

Com usuário admin, abra a tela do FACILE XML-e.

![Figura 1: Tela do FACILE XML-e](../../assets/att-cd/tela-facile-xmle.png "Tela do FACILE XML-e")
<br>*Figura 1: Tela do FACILE XML-e*<br>{: .center-img }
<br>

### Passo 02

Vá na opção em Outras Ações > Manutenção TI > Wiz. Config.

![Figura 2: Opção Wiz. Config.](../../assets/att-cd/wiz-config.jpg "Opção Wiz. Config.")
<br>*Figura 2: Opção Wiz. Config.*<br>{: .center-img }
<br>

### Passo 03

Avance até a tela abaixo.

![Figura 3: Assistente de configuração](../../assets/att-cd/config-cert.png "Assistente de configuração")
<br>*Figura 3: Assistente de configuração*<br>{: .center-img }
<br>

Informe o caminho do arquivo do certificado digital (.PFX) e a sua senha de autenticação, processo parecido com o realizado na configuração do TSS.

Caso não possua o .PFX ou tenha alguma dificuldade na importação do certificado digital, poderá ser utilizado os arquivo “.PEM” gerados pelo TSS, bastando informar o caminho dos arquivos nos seguintes parâmetros:

**ZZ_CERTKEY:** caminho para o arquivo “key.pem” no Protheus_Data.
    Exemplo: \FACILE\9901_key.pem 

**ZZ_CERTPRI:** caminho para o arquivo “cert.pem” no Protheus_Data.
    Exemplo:\FACILE\9901_cert.pem                                                                                     
                                                                                   
**ZZ_CERTKEY:** caminho para o arquivo “ca.pem” no Protheus_Data.
	Exemplo: \FACILE\9901_ca.pem 

<div style="text-align: center; font-weight: bold;">-FIM-</div>