# BSCEMPFL

O BSCEMPFL é um ponto de entrada para manipular a filial tomadora durante o processamento dos atributos das classes de domínio de CT-e e NFS-e.

O presente ponto de entrada é executado tanto em job, quanto em tela. É necessário tomar cuidado com as funções visuais a serem utilizadas.

No download, ainda não há gravação da ZZZ e o BSCEMPFL define a filial em que o documento será gravado. Na geração do documento de entrada, o XML permanece na filial corrente e o usuário é direcionado para a filial retornada para dar entrada na nota.


## Parâmetros

* **Paramixb[1]:** Caracter, armazena somente os dígitos númericos do CPF/CNPJ do tomador do documento.

* **Paramixb[2]:** Objeto, armazena o XML do CT-e/Json da NFS-e do documento em questão.


## Retorno

* **aEmpresaFilial:** Array de 3 posições, onde:
    * aEmpresaFilial[1]: Código da empresa do documento.
    * aEmpresaFilial[2]: Código da filial do documento.
    * aEmpresaFilial[3]: CPF/CNPJ da Empresa do documento.

Em caso de retornar um array vazio, com menos posições ou com as posições em branco, o download do XML específico é interrompido e a ferramenta segue para o próximo da fila de download, dessa forma, o documento pulado não é baixado novamente de forma automática.


## Exemplo de utilização

O exemplo abaixo é ilustrativo e não deve ser utilizado em produção sem revisão e adaptação à regra de negócio do cliente.

```AdvPL
User Function BSCEMPFL()

    Local cCGC           := ParamIxb[1]
    Local oDoc           := ParamIxb[2]

    Local nPos           := 0
    Local aSM0           := {}
    Local aEmpresaFilial := {"", "", ""}

    aSM0 := FWLoadSM0()

    If XmlChildEx(oDoc, "_CTEPROC") != Nil

        oDoc := oDoc:_CTEPROC:_CTE

        If( XmlChildEx(oDoc:_INFCTE:_REM, "_IE") != Nil)

            nPos := Ascan( aSM0, { |x| Alltrim(x[18]) == Alltrim(cCGC) .And. oDoc:_INFCTE:_REM:_IE:TEXT $ AllTrim(x[22]) } )
            
            If nPos > 0
                
                aEmpresaFilial[1] := aSM0[nPos][01]
                aEmpresaFilial[2] := aSM0[nPos][02]
                aEmpresaFilial[3] := cCGC

            Endif

        Endif

    Endif

Return aEmpresaFilial
```

## Como testar

O BSCEMPFL é executado no fluxo de gravação de XML de CT-e ou NFS-e da ferramenta, sendo assim, a função "Importar XML do Computador" presente no PTX0001 (Central XML), é a forma ideal de realizar os testes dessa função, verificando se o processo foi devidamente adaptado para o fluxo de importação ou se foi quebrado durante a execução.


## Consequências

O fluxo de personalização do BSCEMPFL pode interferir em toda recepção de documentos pelo Facile XML-e. É necessário extrema cautela na personalização deste fluxo. Diferentemente do XCarregDados, os erros não interferem na tabela de log FACX002. Porém, um retorno inválido interrompe o download do XML, e um retorno com a filial indesejada faz com que o documento seja gravado na filial incorreta.

Com isso em mente, a personalização desse fluxo foge do suporte usual do Facile XML-e, necessitando de um consultor para apoio ou análise de qualquer eventual problema, sendo necessário acionar o comercial da Facile Soluções em Sistemas.