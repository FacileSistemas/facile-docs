# 🔵Pontos de Entrada

Para o melhor aproveitamento da ferramenta utilizamos pontos de entrada disponibilizados pelo ERP, possibilitando interações e automações em diferentes momentos do documento de entrada.

**ATENÇÃO**: Caso seu ERP esteja no T-Cloud do fabricante (não permite compilação), solicitar à FACILE um patch com os principais pontos de entrada para aplicação!

## MT100TOK

<mark>Uso necessário para o correto funcionamento da ferramenta</mark>

Utilizamos esse ponto de entrada para realizar a validação dos impostos no momento da classificação do documento de entrada.

Sugerimos incluir o código abaixo no final do fonte, logo antes do RETURN (caso tenha o P.E. já aplicado no ERP).

```C
If lValido .And. AllTrim( FunName() ) $ "MATA103/PTX0007/PTX0018/PTX0008/PTX0001"
    lValido := U_PTX0010()
EndIf
```

Segue exemplo do ponto de entrada completo que poderá ser utilizado (caso **NÃO ** tenha o P.E. já aplicado ERP).

```c
User Function MT100TOK()

    Local aArea   := GetArea()
    local lValido := ParamIxb[1]

    If lValido .And. AllTrim( FunName() ) $ "MATA103/PTX0007/PTX0018/PTX0008/PTX0001"

        lValido := U_PTX0010()

    EndIf

    RestArea(aArea)

Return lValido
```

## MT103PN

<mark>Uso necessário para o correto funcionamento da ferramenta</mark>

Utilizamos esse ponto de entrada para realizar a checagem da TES e do pedido de compra nos itens do documento de entrada.

Sugerimos incluir o código abaixo no final do fonte, logo antes do RETURN (caso tenha o P.E. já aplicado no ERP).

```c
If FwIsInCallStack("U_PTX0001")
    FWMsgRun(, {|| U_PTX0015(.T.) }, "Processando!", "Calculando impostos, aguarde...")			
EndIf
```

Segue exemplo do ponto de entrada completo que poderá ser utilizado (caso **NÃO ** tenha o P.E. já aplicado no ERP).

```c
User Function MT103PN()
	
	If FwIsInCallStack("U_PTX0001")
		FWMsgRun(, {|| U_PTX0015(.T.) }, "Processando!", "Calculando impostos, aguarde...")			
	EndIf
	
Return .T.
```

## MT140PC

<mark>Esse ponto de entrada deverá ser utilizado exclusivamente na situação em que a empresa utilize o parâmetro **MV_PCNFE ** ativo.</mark>

Utilizamos o ponto de entrada para informar ao sistema que naquele momento da inclusão da Pré-Nota pela ferramenta não será necessário realizar a validação do pedido de compra.

**Obs.:** A utilização desse ponto de entrada não atrapalha no processo padrão adotado pelo MV_PCNFE.

Segue exemplo do ponto de entrada que poderá ser utilizado:

```
User Function MT140PC()

    //|Apenas na rotina Facile XML-e |
    If !FwIsInCallStack("U_PTX0001")
        Return Nil
    EndIf

Return .F.
```
