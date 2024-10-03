# 🔵Pontos de Entrada da Central XML

Assim como o Protheus, o Facile XML-e tem seus próprios Pontos de Entrada que disponibilizamos para personalizações. Segue abaixo cada um e seus exemplos de utilização.

## CHKDOCOK

Ponto de entrada para validar se o XML será analisado pelo CheckDoc.

Parâmetros:

* **ParamIxb[1]:**  Object, Objeto com o XML a ser analisado pelo checkdoc

Retorno:

* **lRet:** Logical, permite processar o XML.

Segue exemplo de utilização.

```C
User Function CHKDOCOK()

	Local lRet	  := .T.
	Local oXml		:= ParamIxb[1]
	
	If XmlChildEx(oXML:_NFE:_INFNFE:_IDE,"_FINNFE") <> NIL
    If oXML:_NFE:_INFNFE:_IDE:_FINNFE:TEXT == "2" //|NF-e complementar |
      lRet  := .F.
    EndIf
  EndIf

Return lRet
```

_______

## P007CTE

Ponto de entrada para analisar se o CTE deve entrar via rotina de CTE MATA116 ou via documento de entrada MATA103.

Parâmetros:

* **ParamIxb[1]:**  Object, Objeto XML do CTE

Retorno:

* **lRet:** Logical, True para MATA116 e false para MATA103.

Segue exemplo de utilização.

```C
User Function P007CTE()

  Local oObj           := ParamIxb[1]
  Local aArea          := GetArea()
  Local lCteCompra     := .F.
  Local cCnpjDest      := ""
  Local cTipoDocumento := ""

  If !IsBlind()

    lCteCompra := ( fTipoCTE(oObj) == "CTEC" )
  
  Else

    If XmlChildEx(oObj:_CTEPROC:_CTE:_INFCTE:_DEST, "_CNPJ") != Nil
      cCnpjDest    := oObj:_CTEPROC:_CTE:_INFCTE:_DEST:_CNPJ:TEXT
    EndIf

    If Empty(cCnpjDest) .And. XmlChildEx(oObj:_CTEPROC:_CTE:_INFCTE:_DEST, "_CPF") != Nil
      cCnpjDest    := oObj:_CTEPROC:_CTE:_INFCTE:_DEST:_CPF:TEXT
    EndIf

    If cCnpjDest == AllTrim(SM0->M0_CGC)
      cTipoDocumento := "CTEC"
    Else
      cTipoDocumento := "CTEV"
    EndIf

    lCteCompra  := (cTipoDocumento == "CTEC")

  EndIf

  RestArea(aArea)

Return lCteCompra



Static Function fTipoCTE(oObj)

	Local cEstilo1   := ""
	Local cEstBtn1   := ""
	Local cEstSay2   := ""
	Local cTipoCTE   := ""
	Local cNatureza  := ""
	Local cCfops     := ""
	Local nAux       := 0
	Local aCombo1    := {}
	Local aAuxCombo1 := {}
	Local aDados     := {}
	Local cRetPE     := "CTEV"
  Local oSay3      := Nil
  Local oSay4      := Nil
  Local oSay5      := Nil

	Private oBox1
	Private oBox2
	Private oSay1
	Private oSay2

	aCombo1    := {"Frete Despesa (Cte Venda)","Frete Custo Produto (Cte Compra)"}
	aAuxCombo1 := {"CTEV","CTEC"}
	nAux       := aScan(aAuxCombo1,cRetPE)

	If !Empty(cRetPE) .And. nAux != 0
		cTipoCTE := aCombo1[nAux]
	EndIf

  aDados := fDadosDocumento(oObj)

  cNatureza := SubStr( aDados[1], 1, 52 ) + IIf( Len( aDados[1] ) > 60, "...", "" )
  cCfops    := SubStr( aDados[2], 1, 52 ) + IIf( Len( aDados[2] ) > 60, "...", "" )

	oFont1    := TFont():New( "Courier New",0,-16,,.T.,0,,700,.F.,.F.,,,,,, )

	oDlg1     := MSDialog():New( 091,243,380,650,"XML-e - Tipo Documento de Transporte",,,.F.,,,,,,.T.,,,.T. )

	oPanel1   := TPanel():New( 000,000,"",oDlg1,,.F.,.F.,,,280,085,.T.,.F. )
	oPanel1:align:= CONTROL_ALIGN_ALLCLIENT
  cEstilo1 := "	QLabel {"
  cEstilo1 += " background-color: #3D86AB;"
  cEstilo1 += "}"
  oPanel1:SetCss(cEstilo1)

  oSay3      := TSay():New( 005,005,{||"Nat. Operação: " + cNatureza },oPanel1,,,.F.,.F.,.F.,.T.,CLR_WHITE,CLR_WHITE,300,012)
  oSay3:SetCss( " QLabel { color: #FFFFFF; }")

  oSay4      := TSay():New( 015,005,{||"Cfop: " + cCfops },oPanel1,,,.F.,.F.,.F.,.T.,CLR_WHITE,CLR_WHITE,300,012)
  oSay4:SetCss( " QLabel { color: #FFFFFF; }")

  oSay5      := TSay():New( 022,000,{||Replicate("-",120) },oPanel1,,,.F.,.F.,.F.,.T.,CLR_WHITE,CLR_WHITE,300,012)

	oSay1      := TSay():New( 030,016,{||"Tipo de CT-e"},oPanel1,,oFont1,.F.,.F.,.F.,.T.,CLR_WHITE,CLR_WHITE,072,012)
  cEstSay2 	:= "	QLabel { "
  cEstSay2 	+= "	font-family: cursive; "
  cEstSay2 	+= "	font-weight: bold; "
  cEstSay2 	+= "	font-size: large; "
  cEstSay2 	+= "	line-height: 100%; "
  cEstSay2 	+= "	word-spacing: 1ex; "
  cEstSay2 	+= "	letter-spacing: normal; "
  cEstSay2 	+= "	text-decoration: none; "
  cEstSay2 	+= "	text-transform: none; "
  cEstSay2 	+= "	text-align: left; "
  cEstSay2 	+= "	color: #FFFFFF; "
  cEstSay2 	+= "	text-indent: 0ex; "
  cEstSay2 	+= "	} "
  oSay1:SetCss(cEstSay2)

	@ 048,016 MSCOMBOBOX oBox1 VAR cTipoCTE ITEMS aCombo1 SIZE 150,100 OF oDlg1 PIXEL

	oBtn1      := TButton():New( 108,068,"Confirmar",oPanel1,{|| TipoCombo(@cRetPE,aCombo1,cTipoCTE,aAuxCombo1,"1") },056,012,,,,.T.,,"",,,,.F. )
	cEstBtn1 := "QPushButton {"
  cEstBtn1 += " background-image: url(rpo:PTX_Refresh.png);"
  cEstBtn1 += " background-repeat: none; "
  cEstBtn1 += " background-attachment: fixed; "
  cEstBtn1 += " background-position: left center; "
  cEstBtn1 += " border-style: outset;"
  cEstBtn1 += " border-width: 2px;"
  cEstBtn1 += " border: 1px solid #C0C0C0;"
  cEstBtn1 += " border-radius: 5px;"
  cEstBtn1 += " border-color: #C0C0C0;"
  cEstBtn1 += " font: bold 12px Arial;"
  cEstBtn1 	+= "	color: #ffffff; "
  cEstBtn1 += " padding: 6px;"
  cEstBtn1 += "} "

  cEstBtn1 += "QPushButton:hover { "
  cEstBtn1 += " background-color: #cecef6;"
  cEstBtn1 += " border-style: inset;"
  cEstBtn1 += " opacity: 0.2; "
  cEstBtn1 += "} "

  cEstBtn1 += "QPushButton:pressed {"
  cEstBtn1 += " background-color: #e6e6f9;"
  cEstBtn1 += " border-style: inset;"
  cEstBtn1 += "} "
  oBtn1:SetCss(cEstBtn1)

	oDlg1:Activate(,,,.T.)

Return cRetPE


Static Function TipoCombo(cVariavel,aCombo,cCombo,aReferencia,cIdent)

	Local nPos	:= aScan(aCombo,cCombo)
	Local lRet  := (nPos > 0)

	If nPos > 0
		cVariavel := aReferencia[nPos]
	EndIf

	oDlg1:End()

Return (lRet)


Static Function fDadosDocumento(oObj)

  Local cCfops    := ""
  Local cNatureza := ""

  If oObj != Nil

    //|Pega a natureza da operação |
    cNatureza := U_PTX_GetTagValue( oObj, "oObj:_CTEPROC:_CTE:_INFCTE:_IDE:_NATOP" )
    cCfops    := U_PTX_GetTagValue( oObj, "oObj:_CTEPROC:_CTE:_INFCTE:_IDE:_CFOP" )

  EndIf

Return { cNatureza, cCfops }

```

_______

## P07GERAENT

Ponto de entrada chamado ao clicar no botão "Gerar Entrada" para tratamentos diversos está posicionado no XML selecionado (tabela ZZZ).

Segue exemplo de utilização.

```C
User Function P07GERAENT()

  If ZZZ->ZZZ_TIPO == "1" //|NFE |

    If MsgYesNo("Deseja alterar a data do recebimento (D1_DTDIGIT) ?", "P07GERAENT")

      dDataBase := CtoD( FWInputBox("Digite a data do recebimento (dd/mm/aaaa)") )

    EndIf

  EndIf

Return
```

_______

## P09ALTPN

Ponto de entrada após o execauto do MATA140 e quando não estiver para abrir pra classificação.

Retorno:

* **lClassifica:** Logical, True abre a tela de classificação.

Segue exemplo de utilização.

```C
User Function P09ALTPN()

  Local lClassifica := .F.
  Local cSitua      := U_VerifNF()
        
  //|Altera a Legenda |
  RecLock("ZZZ",.F.)
  ZZZ->ZZZ_OK		:= cSitua
  ZZZ->(MsUnLock())

  //lClassifica => se for = .T. ele abre tela de classificação
  
  If !lClassifica

    //|Abre a pré-nota em modo de alteração |
    U_PTX0057( 'PRE' , 'ALTERA' )

  Else

    lClassifica := .T.

  EndIf


Return lClassifica

```

_______

## P011ITEM

Ponto de entrada para manipular o array de itens do CTE de Vendas antes do execauto.

Retorno:

* **_aItensCols:** array, array de itens para o execauto.

Segue exemplo de utilização.

```C
User Function P011ITEM()

	Local _aItensCols   := ParamIxb[1] as Array
	// Local _aCabececalho := ParamIxb[2] as Array
	Local _oXml         := ParamIxb[3] as Object
	Local _nCont       := 0           as Integer
	Local _nI		       := 0           as Integer
	Local _oCTE        := _oXml       as Object
	Local _oIcms       := Nil         as Object
	Local _oIpi        := Nil         as Object
	Local _oPis        := Nil         as Object
	Local _oCofins     := Nil         as Object
	Local _oST         := Nil         as Object

	Local c_FSBICM     := ""          as Character // BASE ICMS
  Local c_FSVICM     := ""          as Character // VALOR ICMS
  Local c_FSBIPI     := ""          as Character // BASE IPI
  Local c_FSVIPI     := ""          as Character // VALOR IPI
  Local c_FSBPIS     := ""          as Character // BASE PIS
  Local c_FSVPIS     := ""          as Character // VALOR POS
  Local c_FSBCOF     := ""          as Character // BASE COFINS
  Local c_FSVCOF     := ""          as Character // VALOR COFINS
  Local c_FSBIST     := ""          as Character // BASE ICMS ST
  Local c_FSVIST     := ""          as Character // VALOR ICMS ST
  Local c_FSCSTIC    := ""          as Character //- F4_SITTRIB <> CSTICMS - CST CLASSIFICAÇÃO FISCAL  
  Local c_FSCSTIP    := ""          as Character //- F4_CTIPI  <>  CST CLASSIFICAÇÃO FISCAL IPI

	Local cExcept      := ""          as Character
  Local bError                      as CodeBlock

	bError    := ErrorBlock({|e| cExcept := "<h3>"+e:Description+"</h3>"+e:ERRORSTACK})

	BEGIN SEQUENCE
	
		_nCont	:= Len( _aItensCols )

		For _nI := 1 To _nCont
			
			If XmlChildEx(_oCTE:_CTEPROC:_CTE, "_INFCTE") != Nil
				_oCTE := _oCTE:_CTEPROC:_CTE:_INFCTE
			EndIf

			If XmlChildEx(_oCTE, "_IMP") != Nil

				//|ICMS |
				If XmlChildEx(_oCTE:_Imp, "_ICMS") != Nil

					_oIcms		:= fBuscaIcms( _oCTE )
					c_FSBICM  := U_PTX_GetTagValue( _oIcms, "_oIcms:_VBC" ) 			// BASE ICMS 
					c_FSVICM  := U_PTX_GetTagValue( _oIcms, "_oIcms:_VICMS" )			// VALOR ICMS
					c_FSORIG  := U_PTX_GetTagValue( _oIcms, "_oIcms:_ORIG" ) 			// B1_ORIGEM -- CST CLASSIFICAÇÃO FISCAL ICMS
					c_FSCSTIC := U_PTX_GetTagValue( _oIcms, "_oIcms:_CST" ) 			//- F4_SITTRIB <> CSTICMS - CST CLASSIFICAÇÃO FISCAL  
				
				EndIf

				//|IPI |
				If XmlChildEx(_oCTE:_Imp, "_IPI") != Nil
				
					_oIpi			:= fBuscaIpi( _oCTE )
					c_FSBIPI  := U_PTX_GetTagValue( _oIpi, "_oIpi:_VBC" )   			// BASE IPI
					c_FSVIPI  := U_PTX_GetTagValue( _oIpi, "_oIpi:_VIPI" ) 				// VALOR IPI
					c_FSCSTIP := U_PTX_GetTagValue( _oIpi, "_oIpi:_CST" ) 			  //- F4_CTIPI  <>  CST CLASSIFICAÇÃO FISCAL IPI

				EndIf

				//|PIS |
				If XmlChildEx(_oCTE:_Imp, "_PIS") != Nil

					_oPis			:= fBuscaPis( _oCTE )
					c_FSBPIS  := U_PTX_GetTagValue( _oPis, "_oPis:_VBC" ) 				// BASE PIS
					c_FSVPIS  := U_PTX_GetTagValue( _oPis, "_oPis:_VPIS" ) 				// VALOR PIS
			
				EndIf

				//|COFINS |
				If XmlChildEx(_oCTE:_Imp, "_COFINS") != Nil

					_oCofins	:= fBuscaCofins( _oCTE )
					c_FSBCOF  := U_PTX_GetTagValue( _oCofins, "_oCofins:_VBC" )  			// BASE COFINS
					c_FSVCOF  := U_PTX_GetTagValue( _oCofins, "_oCofins:_VCOFINS" )  	// VALOR COFINS
				
				EndIf

				//|ICMS ST |
				If XmlChildEx(_oCTE:_Imp, "_ICMS") != Nil

					_oST			:= fBuscaIcms( _oCTE )
					c_FSBIST  := U_PTX_GetTagValue( _oST, "_oST:_VBCST" ) 						// BASE ICMS ST
					c_FSVIST  := U_PTX_GetTagValue( _oST, "_oST:_VICMSST" ) 					// VALOR ICMS ST
					
				EndIf

			EndIf

			//|Adiciona ao aCols |
			aadd(_aItensCols[_nI], {"D1_FSBICM ", Val(c_FSBICM), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSVICM ", Val(c_FSVICM), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSBIPI ", Val(c_FSBIPI), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSVIPI ", Val(c_FSVIPI), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSBPIS ", Val(c_FSBPIS), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSVPIS ", Val(c_FSVPIS), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSBCOF ", Val(c_FSBCOF), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSVCOF ", Val(c_FSVCOF), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSBIST ", Val(c_FSBIST), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSVIST ", Val(c_FSVIST), Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSCSTIC", c_FSCSTIC    , Nil, Nil})
			aadd(_aItensCols[_nI], {"D1_FSCSTIP", c_FSCSTIP    , Nil, Nil})

		Next _nI
	
	END SEQUENCE

	ErrorBlock(bError)

	If !Empty(cExcept)
		ConOut(cExcept)
	EndIf

Return _aItensCols



Static Function fBuscaIcms( _oCTE )

	Local _oIcms as Object

	Do Case

		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS00") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS00
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS10") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS10
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS20") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS20
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS30") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS30
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS40") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS40
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS41") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS41
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS45") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS45
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS50") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS50
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS51") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS51
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS60") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS60
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS70") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS70
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMS90") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMS90
		Case XmlChildEx(_oCTE:_Imp:_ICMS, "_ICMSST") != Nil
			_oIcms := _oCTE:_Imp:_ICMS:_ICMSST

	EndCase

Return _oIcms




Static Function fBuscaIpi( __oCTE )

	Local _oImp as Object

	Do Case

		Case XmlChildEx(_oCTE:_Imp:_IPI, "_IPITRIB") != Nil
			_oImp := _oCTE:_Imp:_IPI:_IPITRIB
		Case XmlChildEx(_oCTE:_Imp:_IPI, "_IPINT") != Nil
			_oImp := _oCTE:_Imp:_IPI:_IPINT

	EndCase

Return _oImp



Static Function fBuscaPis( __oCTE )

	Local _oImp as Object

	Do Case

		Case XmlChildEx(_oCTE:_Imp:_PIS, "_PISALIQ") != Nil
			_oImp := _oCTE:_Imp:_PIS:_PISALIQ

	EndCase

Return _oImp



Static Function fBuscaCofins( __oCTE )

	Local _oImp as Object

	Do Case

		Case XmlChildEx(_oCTE:_Imp:_COFINS, "_COFINSALIQ") != Nil
			_oImp := _oCTE:_Imp:_COFINS:_COFINSALIQ

	EndCase

Return _oImp
```

_______

## P018COLS

Ponto de entrada para manipular o array de itens do documento de entrada antes do execauto.

Retorno:

* **_aItensCols:** array, array de itens para o execauto

Segue exemplo de utilização.

```C
User Function P018COLS()

	Local _aItensCols  := ParamIxb[1] as Array
	// Local _aCabecalho 	:= ParamIxb[2] as Array
	Local _oXml        := ParamIxb[3] as Object
  Local aProcessados := {}          as Array
	// Local _cProduto     := ""          as Character
	// Local _cDocumento   := ""          as Character
	Local _cItemXml    := ""          as Character
	Local _nZ          := 0           as Integer
	Local _nI          := 0           as Integer
	Local _nPos        := 0           as Integer
	Local _nPosIemXml  := 0           as Integer
	Local _nCont       := 0           as Integer
	Local _oItem       := Nil         as Object
	Local oDetXml      := Nil         as Variant
	Local _oIcms       := Nil         as Object
	Local _oIpi        := Nil         as Object
	Local _oPis        := Nil         as Object
	Local _oCofins     := Nil         as Object
	Local _oST         := Nil         as Object

	Local c_FSBICM     := ""          as Character // BASE ICMS
  Local c_FSVICM     := ""          as Character // VALOR ICMS
  Local c_FSBIPI     := ""          as Character // BASE IPI
  Local c_FSVIPI     := ""          as Character // VALOR IPI
  Local c_FSBPIS     := ""          as Character // BASE PIS
  Local c_FSVPIS     := ""          as Character // VALOR POS
  Local c_FSBCOF     := ""          as Character // BASE COFINS
  Local c_FSVCOF     := ""          as Character // VALOR COFINS
  Local c_FSBIST     := ""          as Character // BASE ICMS ST
  Local c_FSVIST     := ""          as Character // VALOR ICMS ST
  Local c_FSCEST     := ""          as Character // B1_CEST <> cest -- CÓDIGO CEST
  Local c_FSORIG     := ""          as Character // B1_ORIGEM <> -- CST CLASSIFICAÇÃO FISCAL ICMS
  Local c_FSCSTIC    := ""          as Character //- F4_SITTRIB <> CSTICMS - CST CLASSIFICAÇÃO FISCAL  
  Local c_FSCSTIP    := ""          as Character //- F4_CTIPI  <>  CST CLASSIFICAÇÃO FISCAL IPI

	Local cExcept      := ""          as Character
  Local bError                      as CodeBlock

  bError    := ErrorBlock({|e| cExcept := "<h3>"+e:Description+"</h3>"+e:ERRORSTACK})

	BEGIN SEQUENCE
  
		If ZZZ->ZZZ_TIPO == "1"

			//|Pega campos necessários |
			// If ( _nPos := aScan(_aCabecalho, { |x| Alltrim(x[1]) == "F1_DOC" }) ) > 0
			// 	_cDocumento	:= _aCabecalho[ _nPos, 2 ]
			// EndIf

			// If ( _nPos := aScan(_aItensCols[1], { |x| Alltrim(x[1]) == "D1_COD" }) ) > 0
			// 	_cProduto	:= _aItensCols[ 1, _nPos, 2 ]
			// EndIf

			oDetXml		:= _oXml:_InfNfe:_Det
			oDetXml 	:= IIf( ValType(oDetXml) == "O", {oDetXml}, oDetXml )

			_nCont	:= Len( _aItensCols )
			
			//|Percorre todos os itens do aCols SD1 |
			For _nI := 1 To _nCont

				_nPosIemXml	:= aScan( _aItensCols[_nI], { |x| Alltrim(x[1]) == "D1_ZITEXML" } )
				_cItemXml		:= _aItensCols[_nI, _nPosIemXml, 2]
				
				//|Variavel de controle para processar itens fracionados apenas uma vez |
				If ( _nPos := aScan( aProcessados, _cItemXml ) ) > 0
					Loop
				Else
					aAdd( aProcessados, _cItemXml )
				EndIf

				//|Encontra o respectivo item no XML |
				For _nZ := 1 To Len( oDetXml )

					If cValToChar( oDetXml[_nZ]:_NITEM:TEXT ) == cValToChar( _cItemXml )
						_oItem	:= oDetXml[_nZ]
						Exit
					EndIf

				Next _nZ
				
				If XmlChildEx(_oItem, "_IMPOSTO") != Nil

					//|ICMS |
					If XmlChildEx(_oItem:_Imposto, "_ICMS") != Nil

						_oIcms		:= fBuscaIcms( _oItem )
						c_FSBICM  := U_PTX_GetTagValue( _oIcms, "_oIcms:_VBC" ) 			// BASE ICMS 
						c_FSVICM  := U_PTX_GetTagValue( _oIcms, "_oIcms:_VICMS" )			// VALOR ICMS
						c_FSORIG  := U_PTX_GetTagValue( _oIcms, "_oIcms:_ORIG" ) 			// B1_ORIGEM -- CST CLASSIFICAÇÃO FISCAL ICMS
						c_FSCSTIC := U_PTX_GetTagValue( _oIcms, "_oIcms:_CST" ) 			//- F4_SITTRIB <> CSTICMS - CST CLASSIFICAÇÃO FISCAL  
					
					EndIf

					//|IPI |
					If XmlChildEx(_oItem:_Imposto, "_IPI") != Nil
					
						_oIpi			:= fBuscaIpi( _oItem )
						c_FSBIPI  := U_PTX_GetTagValue( _oIpi, "_oIpi:_VBC" )   			// BASE IPI
						c_FSVIPI  := U_PTX_GetTagValue( _oIpi, "_oIpi:_VIPI" ) 				// VALOR IPI
						c_FSCSTIP := U_PTX_GetTagValue( _oIpi, "_oIpi:_CST" ) 			  //- F4_CTIPI  <>  CST CLASSIFICAÇÃO FISCAL IPI

					EndIf

					//|PIS |
					If XmlChildEx(_oItem:_Imposto, "_PIS") != Nil

						_oPis			:= fBuscaPis( _oItem )
						c_FSBPIS  := U_PTX_GetTagValue( _oPis, "_oPis:_VBC" ) 				// BASE PIS
						c_FSVPIS  := U_PTX_GetTagValue( _oPis, "_oPis:_VPIS" ) 				// VALOR PIS
				
					EndIf

					//|COFINS |
					If XmlChildEx(_oItem:_Imposto, "_COFINS") != Nil

						_oCofins	:= fBuscaCofins( _oItem )
						c_FSBCOF  := U_PTX_GetTagValue( _oCofins, "_oCofins:_VBC" )  			// BASE COFINS
						c_FSVCOF  := U_PTX_GetTagValue( _oCofins, "_oCofins:_VCOFINS" )  	// VALOR COFINS
					
					EndIf

					//|ICMS ST |
					If XmlChildEx(_oItem:_Imposto, "_ICMS") != Nil

						_oST			:= fBuscaIcms( _oItem )
						c_FSBIST  := U_PTX_GetTagValue( _oST, "_oST:_VBCST" ) 						// BASE ICMS ST
						c_FSVIST  := U_PTX_GetTagValue( _oST, "_oST:_VICMSST" ) 					// VALOR ICMS ST
						
					EndIf

				EndIf

				c_FSCEST	:= U_PTX_GetTagValue( _oItem, "_oItem:_PROD:_CEST" ) // CÓDIGO CEST

				//|Adiciona ao aCols |
				aadd(_aItensCols[_nI], {"D1_FSBICM ", Val(c_FSBICM), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSVICM ", Val(c_FSVICM), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSBIPI ", Val(c_FSBIPI), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSVIPI ", Val(c_FSVIPI), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSBPIS ", Val(c_FSBPIS), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSVPIS ", Val(c_FSVPIS), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSBCOF ", Val(c_FSBCOF), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSVCOF ", Val(c_FSVCOF), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSBIST ", Val(c_FSBIST), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSVIST ", Val(c_FSVIST), Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSCEST ", c_FSCEST     , Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSORIG ", c_FSORIG     , Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSCSTIC", c_FSCSTIC    , Nil, Nil})
				aadd(_aItensCols[_nI], {"D1_FSCSTIP", c_FSCSTIP    , Nil, Nil})

			Next _nI

		EndIf

	END SEQUENCE

	ErrorBlock(bError)

	If !Empty(cExcept)
		ConOut(cExcept)
	EndIf

Return _aItensCols



Static Function fBuscaIcms( _oItem )

	Local _oIcms as Object

	Do Case

		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS00") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS00
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS10") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS10
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS20") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS20
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS30") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS30
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS40") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS40
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS41") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS41
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS50") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS50
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS51") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS51
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS60") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS60
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS70") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS70
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMS90") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMS90
		Case XmlChildEx(_oItem:_Imposto:_ICMS, "_ICMSST") != Nil
			_oIcms := _oItem:_Imposto:_ICMS:_ICMSST

	EndCase

Return _oIcms



Static Function fBuscaIpi( _oItem )

	Local _oImp as Object

	Do Case

		Case XmlChildEx(_oItem:_Imposto:_IPI, "_IPITRIB") != Nil
			_oImp := _oItem:_Imposto:_IPI:_IPITRIB
		Case XmlChildEx(_oItem:_Imposto:_IPI, "_IPINT") != Nil
			_oImp := _oItem:_Imposto:_IPI:_IPINT

	EndCase

Return _oImp



Static Function fBuscaPis( _oItem )

	Local _oImp as Object

	Do Case

		Case XmlChildEx(_oItem:_Imposto:_PIS, "_PISALIQ") != Nil
			_oImp := _oItem:_Imposto:_PIS:_PISALIQ

	EndCase

Return _oImp



Static Function fBuscaCofins( _oItem )

	Local _oImp as Object

	Do Case

		Case XmlChildEx(_oItem:_Imposto:_COFINS, "_COFINSALIQ") != Nil
			_oImp := _oItem:_Imposto:_COFINS:_COFINSALIQ

	EndCase

Return _oImp
```

_______

## P018CPO

Ponto de entrada para adicionar campos extras na SD1 antes do execauto. **Esse ponto de entrada será chamado para cada item do documento de entrada.**

Parâmetros:

* **ParamIxb[1]:**  Array com os campos do item a ser gerado no Protheus.
* **ParamIxb[2]:**  Array com o item do XML.
* **ParamIxb[3]:**  Array com o cabeçalho do XML.

Retorno:

* **aCpos:** array, array com os campos extras na SD1 antes do execauto.

Segue exemplo de utilização.

```C
User Function P018CPO()

  Local aCpos       := {}
  Local _nPos       := 0
  Local _cProduto   := ""
  Local _cTipo      := ""
  Local aItProtheus := ParamIxb[1]
  Local aItXml      := ParamIxb[2]
  Local aCabecXml   := ParamIxb[3]

  //|Pega o produto |
  If ( _nPos := aScan(aItProtheus, { |x| Alltrim(x[1]) == "D1_COD" }) ) > 0
		_cProduto	:= aItProtheus[ _nPos, 2 ]
	EndIf

  //|Pega o Tipo de NF |
  If ( _nPos := aScan(aCabecXml, { |x| Alltrim(x[1]) == "F1_TIPO" }) ) > 0
		_cTipo	:= aCabecXml[ _nPos, 2 ]
	EndIf

  aadd(aCpos, {"D1_XUMXML" , aItXml:_Prod:_uCom:TEXT     , Nil, Nil})
  aadd(aCpos, {"D1_XQTDXML", Val(aItXml:_Prod:_qCom:TEXT), Nil, Nil})
  aadd(aCpos, {"D1_XDESXML", aItXml:_Prod:_XPROD:TEXT    , Nil, Nil})
  aadd(aCpos, {"D1_UM"     , SB1->B1_UM                  , Nil, Nil})

Return aCpos
```

_______

## P018FIM

Ponto de entrada para manutenções diversas ao final da geração do documento, devido a isso, já se encontra posicionado na ZZZ e na SF1.

Segue exemplo de utilização.

```C
User Function P018FIM()

  MsgInfo("Nota Fiscal gerada: " + AllTrim(SF1->F1_DOC) + " / " + AllTrim(SF1->F1_SERIE))

Return
```

_______

## P018ITEM

Ponto de entrada para alterar informações do item antes do execauto.

Parâmetros:

* **ParamIxb[1]:**  Array com os campos do item a ser gerado no Protheus.
* **ParamIxb[2]:**  Array com o item do XML.
* **ParamIxb[3]:**  Array com o cabeçalho do XML.

Retorno:

* **aItemCols:** array, array com a nova linha do item a ser gerado no Protheus.

Segue exemplo de utilização.

```C
User Function P018ITEM()

	Local aItemCols		:= ParamIxb[1]
	Local _aCabec			:= ParamIxb[3]
	Local aItemXML		:= ParamIxb[2]
	Local nI					:= 0
	Local nPos				:= 0
	Local lDevolucao	:= .F.
	
	If ( nPos := aScan( _aCabec, { |x| AllTrim( x[1] ) == "F1_TIPO" } ) )

		lDevolucao	:= ( _aCabec[nPos, 2] == "D" )
	
	EndIf

	If lDevolucao

		For nI := 1 To Len(aItemCols)

			//|Nota de devolução? |
			If AllTrim( aItemCols[nI,1] ) == "D1_UM"

				Alert( "Devolução com o D1_UM = " + aItemCols[nI,2] )

				aItemCols[nI,2] := "CX"

			EndIf

		Next nI
	
	EndIf

Return aItemCols
```

_______

## P018PROD

Ponto de entrada para analisar os itens do XML no momento da entrada.

Parâmetros:

* **ParamIxb[1]:**  Array com o objeto XML dos produtos da nota fiscal eletronica.
* **ParamIxb[2]:**  Se .T. indica que é uma devolução de venda.
* **ParamIxb[3]:**  Código do fornecedor no Protheus.
* **ParamIxb[4]:**  Loja do fornecedor no Protheus.

Segue exemplo de utilização.

```C
User Function P018PROD()

  Local nCont       := 0
  Local aItensXml   := ParamIxb[1]
  Local lDevoluc    := ParamIxb[2]
  Local cFornece    := ParamIxb[3]
  Local cLoja       := ParamIxb[4]
  Local aArea       := GetArea()
  Local aAreaZZW    := ZZW->( GetArea() )

  //|Não processa para devolução |
  If lDevoluc
    Return
  EndIf

  dbselectarea('ZZW')
  ZZW->(dbsetorder(1))

  For nCont := 1 To Len(aItensXml)

    cProdFornec     := aItensXml[nCont]:_PROD:_CPROD:TEXT
    cCodBarras		  := IIf( XmlChildEx(aItensXml[nCont]:_PROD, "_CEAN") <> NIL,aItensXml[nCont]:_PROD:_CEAN:TEXT,space(12) )

    //|Nesse ponto procura o produto na SB1 |
    //...
    //...
    //...

    //|Deve adicionar o produto na ZZW quando não existir |
    If !ZZW->( dbSeek( xFilial('ZZW') + cfornece + cLoja + PADR(AllTrim(cProdFornec),TamSX3("ZZW_CODPRF")[1]) + SB1->B1_COD) )

      Reclock('ZZW',.T.)
      ZZW->ZZW_FILIAL		:= xFilial('ZZW')
      ZZW->ZZW_PRODUT		:= SB1->B1_COD
      ZZW->ZZW_FORNEC		:= cfornece
      ZZW->ZZW_LOJA		  := cLoja
      ZZW->ZZW_CODPRF 	:= cProdFornec

      If ZZW->( FieldPos("ZZW_DPRODF") ) > 0
        ZZW->ZZW_DPRODF	:= aItensXml[nCont]:_PROD:_XPROD:TEXT
      EndIf

      ZZW->(MsUnlock())

    EndIf

  Next nCont


  RestArea(aAreaZZW)
  RestArea(aArea)

Return
```

_______

## P018PROPRIO

Ponto de entrada para indicar formulário próprio na entrada.

Parâmetros:

* **ParamIxb[1]:**  Se é formulário próprio. Identificado com "S" ou "N".
* **ParamIxb[2]:**  Número da NF que está entrando no sistema.
* **ParamIxb[3]:**  Série da NF que está entrando no sistema.

Retorno:

* **aRetorno:** array, array com dados para a NF-e.

Segue exemplo de utilização.

```C
User Function P018PROPRIO()

	Local cFormProprio 	:= ParamIxb[1]
	Local cNumNFe			 	:= ParamIxb[2]
	Local cNumSerie 	 	:= ParamIxb[3]
	Local cSerieNF 			:= ""
	Local aRetorno			:= {}

	cFormProprio	:= fFormProrio()

	If cFormProprio	== "S"

		cNumero	:= ""
		Sx5NumNota( @cSerieNF, SuperGetMV("MV_TPNRNFS") )

		cNumNFe		:= cNumero
		cNumSerie	:= cSerieNF

	EndIf

	aAdd(aRetorno, cFormProprio	)
	aAdd(aRetorno, cNumNFe			)
	aAdd(aRetorno, cNumSerie 		)

Return aRetorno



Static Function fFormProrio()

	Local cRetorno	 := "N"
	Local aCombo1    := {"Não","Sim"}
	Local aAuxCombo1 := {"N","S"}

	oDlg1     := MSDialog():New( 091,243,300,650,"XML-e - Formulário Próprio",,,.F.,,,,,,.T.,,,.T. )

	oSay1      := TSay():New( 030,016,{||"Formulário Próprio?"},oDlg1,,,.F.,.F.,.F.,.T.,CLR_BLACK,CLR_WHITE,072,012)

	@ 048,016 MSCOMBOBOX oBox1 VAR cRetorno ITEMS aCombo1 SIZE 150,100 OF oDlg1 PIXEL

	oBtn1      := TButton():New( 088,068,"Confirmar",oDlg1,{|| TipoCombo(aCombo1,cRetorno,aAuxCombo1) },056,012,,,,.T.,,"",,,,.F. )

	oDlg1:Activate(,,,.T.)

	If Empty(cRetorno)
		cRetorno	:= "N"
	EndIf

  cRetorno := SubStr(cRetorno, 1, 1)

Return cRetorno


Static Function TipoCombo(aCombo,cCombo,aReferencia)

	Local nPos	:= aScan(aCombo,cCombo)
	Local lRet  := (nPos > 0)

	If nPos > 0
		cCombo := aReferencia[nPos]
	EndIf

	oDlg1:End()

Return (lRet)

```

_______

## P018SF1

Ponto de entrada para manipular o array de cabeçalho (SF1) do documento de entrada antes do execauto.

Parâmetros:

* **ParamIxb[1]:**  Array com os campos do item a ser gerado no Protheus.
* **ParamIxb[2]:**  Array com o cabeçalho do XML.
* **ParamIxb[3]:**  Objeto do XML.

Retorno:

* **_aCabecalho:** array, novo array do cabeçalho.

Segue exemplo de utilização.

```C
User Function P018SF1()

	// Local _aItensCols := ParamIxb[1] as Array
	Local _aCabecalho := ParamIxb[2] as Array
	Local _oXml       := ParamIxb[3] as Object
	Local oTransp     := Nil         as Object
	Local cVolume     := ""          as Character

	Local cExcept      := ""          as Character
  Local bError                      as CodeBlock

  bError    := ErrorBlock({|e| cExcept := "<h3>"+e:Description+"</h3>"+e:ERRORSTACK})

	BEGIN SEQUENCE
  
		If ZZZ->ZZZ_TIPO == "1"	//|NF-e |

			oTransp    	:= _oXml:_InfNfe:_Transp

			If XmlChildEx(oTransp, "_VOL") != Nil

				cVolume	:= U_PTX_GetTagValue( oTransp, "oTransp:_VOL:_QVOL" )

				If !Empty(cVolume)

					aAdd(_aCabecalho,{"F1_VOLUME1", Val(cVolume), Nil, Nil})

				EndIf

			EndIf

		EndIf

	END SEQUENCE

	ErrorBlock(bError)

	If !Empty(cExcept)
		ConOut(cExcept)
	EndIf

Return _aCabecalho
```

_______

## P018TIPO

Ponto de entrada para modificar o tipo de nota fiscal.

Retorno:

* **cRetPE:** caracter, novo tipo do documento fiscal.

Segue exemplo de utilização.

```C
User Function _P018TIPO()

	Local cEstilo1	:= ""
	Local cEstBtn1	:= ""
	Local cEstSay2	:= ""
	Local c103Tipo	:= ""
	Local nAux		:= 0
	Local aCombo1	:= {}
	Local aAuxCombo1:= {}
	Local cRetPE	:= "N"

	Private oBox1
	Private oSay1

	aCombo1    := {"Normal","Devolução","Beneficiamento","Compl.  ICMS","Compl.  IPI","Compl. Preco/Frete"}
	aAuxCombo1 := {"N","D","B","I","P","C"}
	nAux       := aScan(aAuxCombo1,cRetPE)

	If !Empty(cRetPE) .And. nAux <> 0
		c103Tipo := aCombo1[nAux]
	EndIf

	oFont1     := TFont():New( "Courier New",0,-16,,.T.,0,,700,.F.,.F.,,,,,, )

	oDlg1      := MSDialog():New( 091,243,270,650,"XML-e - Tipo de Documento de Entrada",,,.F.,,,,,,.T.,,,.T. )

	oPanel1    := TPanel():New( 000,000,"",oDlg1,,.F.,.F.,,,280,085,.T.,.F. )
	oPanel1:align:= CONTROL_ALIGN_ALLCLIENT
		cEstilo1 := "	QLabel {"
		cEstilo1 += " background-color: #3D86AB;"
		cEstilo1 += "}"
		oPanel1:SetCss(cEstilo1)

	oSay1      := TSay():New( 012,016,{||"Tipo da Nota"},oPanel1,,oFont1,.F.,.F.,.F.,.T.,CLR_WHITE,CLR_WHITE,072,012)
		cEstSay2 	:= "	QLabel { "
		cEstSay2 	+= "	font-family: cursive; "
		cEstSay2 	+= "	font-weight: bold; "
		cEstSay2 	+= "	font-size: large; "
		cEstSay2 	+= "	line-height: 100%; "
		cEstSay2 	+= "	word-spacing: 1ex; "
		cEstSay2 	+= "	letter-spacing: normal; "
		cEstSay2 	+= "	text-decoration: none; "
		cEstSay2 	+= "	text-transform: none; "
		cEstSay2 	+= "	text-align: left; "
		cEstSay2 	+= "	color: #FFFFFF; "
		cEstSay2 	+= "	text-indent: 0ex; "
		cEstSay2 	+= "	} "
		oSay1:SetCss(cEstSay2)

	//oGet1      := TGet():New( 024,016,{|u| If(PCount()>0,cChvNfe:=u,cChvNfe)},oPanel1,240,008,'',,CLR_BLACK,CLR_WHITE,,,,.T.,"",,,.F.,.F.,,.F.,.F.,"","cChvNfe",,)
	@ 032,016 MSCOMBOBOX oBox1 VAR c103Tipo ITEMS aCombo1 SIZE 150,100 OF oDlg1 PIXEL

	oBtn1      := TButton():New( 056,068,"Confirmar",oPanel1,{|| TipoCombo(@cRetPE,aCombo1,c103Tipo,aAuxCombo1,"1") },056,012,,,,.T.,,"",,,,.F. )
	cEstBtn1 := "QPushButton {"
	    	cEstBtn1 += " background-image: url(rpo:PTX_Refresh.png);"
	    	cEstBtn1 += " background-repeat: none; "
	    	cEstBtn1 += " background-attachment: fixed; "
	    	cEstBtn1 += " background-position: left center; "
	    	cEstBtn1 += " border-style: outset;"
	    	cEstBtn1 += " border-width: 2px;"
	    	cEstBtn1 += " border: 1px solid #C0C0C0;"
	    	cEstBtn1 += " border-radius: 5px;"
	    	cEstBtn1 += " border-color: #C0C0C0;"
	    	cEstBtn1 += " font: bold 12px Arial;"
	    	cEstBtn1 	+= "	color: #ffffff; "
	    	cEstBtn1 += " padding: 6px;"
	    	cEstBtn1 += "} "

	    	cEstBtn1 += "QPushButton:hover { "
	    	cEstBtn1 += " background-color: #cecef6;"
	    	cEstBtn1 += " border-style: inset;"
	    	cEstBtn1 += " opacity: 0.2; "
	    	cEstBtn1 += "} "

	    	cEstBtn1 += "QPushButton:pressed {"
	    	cEstBtn1 += " background-color: #e6e6f9;"
	    	cEstBtn1 += " border-style: inset;"
	    	cEstBtn1 += "} "
	    	oBtn1:SetCss(cEstBtn1)

	oDlg1:Activate(,,,.T.)

	If Empty(cRetPE)
		cRetPE	:= "N"
	EndIf

Return cRetPE


Static Function TipoCombo(cVariavel,aCombo,cCombo,aReferencia,cIdent)

	Local nPos	:= aScan(aCombo,cCombo)
	Local lRet  := (nPos > 0)

	If nPos > 0
		cVariavel := aReferencia[nPos]
	EndIf

	oDlg1:End()

Return (lRet)
```

_______

## P018UM

Ponto de entrada que realiza a conversão de unidade de medida de acordo com a ZZW.

Parâmetros:

* **ParamIxb[1]:**  Unidade de medida do XML.
* **ParamIxb[2]:**  Quantidade do produto do XML.
* **ParamIxb[3]:**  Total do item do XML.
* **ParamIxb[4]:**  Valor unitário do item no XML.
* **ParamIxb[5]:**  Número do Pedido de Compra.
* **ParamIxb[6]:**  Item do Pedido de Compra.

Retorno:

O retorno é efetuado nas variáveis privadas abaixo.

* **cUnMed1:** caracter, Primeira Unidade de Medida D1_UM.
* **nQtdUM1:** caracter, Quantidade na primeira Unidade de Medida.
* **cUnMed2:** caracter, Segunda Unidade de Medida utilizada.
* **nQtdUM2:** caracter, Quantidade na Segunda Unidade de Medida utilizada.
* **nVlrUM1:** caracter, Valor Unitário na Primeira Unidade de Medida do Produto.

Segue exemplo de utilização.

```C
User Function P018UM()

  // Local cUmXml    := ParamIxb[1]
  Local nQtdXML   := ParamIxb[2]
  Local nTotalXml := ParamIxb[3]
  // Local nUnitXml  := ParamIxb[4]
  Local nQtConv   := 0

  dbSelectArea("ZZW")
  ZZW->(dbSetOrder(2))	//ZZW_FILIAL+ZZW_FORNEC+ZZW_LOJA+ZZW_PRODUT
  If ZZW->(dbSeek(xFilial("ZZW") + SA2->A2_COD + SA2->A2_LOJA + SB1->B1_COD ))

    If !Empty(ZZW->ZZW_SEGUM) .And. !Empty(ZZW->ZZW_CONV) .And. !Empty(ZZW->ZZW_TIPCON)

      nQtConv		:= U_PTXConvUm( SB1->B1_COD, 0, nQtdXML, 1 )

      If nQtConv > 0

        //|Retorno |
        cUnMed1		:= SB1->B1_UM		  //|Primeira Unidade de Medida D1_UM |
        nQtdUM1 	:= nQtConv				//|Qtd UM 1 D1_QUANT |

        cUnMed2	:= ZZW->ZZW_SEGUM
        nQtdUM2 := nQtdXML

        //IF SAH->(dbSeek(xFilial("SAH") + cUnidMed )) //AH_FILIAL, AH_UNIMED, R_E_C_N_O_, D_E_L_E_T_
        //  cUnMed2		:= cUnidMed				//|Segunda Unidade de Medida D1_SEGUM |
        //  nQtdUM2 	:= nQuant				//|Qtd UM 2 D1_QTSEGUM |
        //ENDIF

        nVlrUM1		:= nTotalXml / nQtConv	//|Valor Unit UM 1 D1_VUNIT |

      EndIf

    EndIf

  EndIf

Return
```

_______

## P018ZZW

Ponto de entrada para manutenções após inclusão da ZZW. Nesse momento já está posicionado na ZZW incluída.

Segue exemplo de utilização.

```C
User Function P018ZZW()

  Local aArea := GetArea()
  Local cQuery := ""

  cQuery += " SELECT A5_FORNECE "
  cQuery += " FROM " + RetSqlName("SA5") + " SA5 "
  cQuery += " WHERE A5_FILIAL = " + ValToSql( xFilial("SA5") )
  cQuery += "   AND A5_FORNECE = " + ValToSql( ZZW->ZZW_FORNEC )
  cQuery += "   AND A5_LOJA = " + ValToSql( ZZW->ZZW_LOJA )
  cQuery += "   AND A5_PRODUTO = " + ValToSql( ZZW->ZZW_PRODUT )
  cQuery += "   AND A5_CODPRF = " + ValToSql( ZZW->ZZW_CODPRF )
  cQuery += "   AND SA5.D_E_L_E_T_ = '' "

  If Select("__SA5") > 0
    __SA5->( dbCloseArea() )
  EndIf

  cQuery := ChangeQuery(cQuery)
  dbUseArea( .T., "TOPCONN", TCGenQry(,,cQuery), "__SA5", .T., .T. )

  __SA5->( dbGoTop() )

  //|Caso não exista cadastrado |
  If __SA5->( EoF() )

    RecLock("SA5", .T.)
    SA5->A5_FILIAL  := xFilial("SA5")
    SA5->A5_FORNECE := ZZW->ZZW_FORNEC
    SA5->A5_LOJA    := ZZW->ZZW_LOJA
    SA5->A5_PRODUTO := ZZW->ZZW_PRODUT
    SA5->A5_CODPRF  := ZZW->ZZW_CODPRF
    SA5->( MsUnLock() )

  EndIf

  RestArea( aArea )
  
Return
```

_______

## PT006XML

Ponto de Entrada para realizar ações após a importação do CTE.

Segue exemplo de utilização.

```C
user function PT006XML()

	Local aArea		:= GetArea()
	Local aAreaZZZ	:= ZZZ->(GetArea())
	
	dbSelectArea("ZZZ")
	ZZZ->(dbSetOrder(1))
	ZZZ->(dbSeek(xFilial("ZZZ") + "32171001928075005835550020000243931464892230"))
	

	
	If !Empty(ZZZ->ZZZ_XML)
		
		//|Chama rotina para gerar o documento de entrada |
		fClassDev()
	
	EndIf
	
	RestArea(aAreaZZZ)
	RestArea(aArea)
	
return


Static Function fClassDev()
	
	Local cError  		:= ""
	Local cWarning		:= ""
	Local cCliente		:= ""
	Local cLoja			:= ""
	Local cEmissao		:= ""
	Local cNumNf		:= ""
	Local cSerie		:= ""
	Local cCnpjEmi		:= ""
	Local cCfoDev		:= SuperGetMV("MV_YCFODEV",.F.,"201/411/410")
	Local aArea   		:= GetArea()
	Local aItTemp 		:= {}
	Local aItens 		:= {}
	Local nI	  		:= 0
	Local lDevol		:= .F.
	Local oXml    		:= NIL
	
	oXml := XmlParser( ZZZ->ZZZ_XML, "_", @cError, @cWarning )
				
	If !Empty(alltrim(cError))
		oXml := NIL
	EndIf
	
	If oXml <> NIL
		//Tratamento caso o xml possua a tag NFEPROC
		if XmlChildEx(oXml, "_NFEPROC") <> nil
			oXml := XmlChildEx(oXml, "_NFEPROC")
		endif
		if XmlChildEx(oXml, "_NFE") == nil
			oXml := NIL
		elseIf ValType(oXml:_NFE:_INFNFE:_DET) <> "A"
			XmlNode2Arr(oXml:_NFE:_INFNFE:_DET,"_DET")
		EndIf
	endif
	
	If oXml <> nil
	
		aItens	:= oXml:_NFE:_INFNFE:_DET
		
		For nI := 1 To Len(aItens)
			
			If XmlChildEx(aItens[1]:_PROD, "_CFOP") <> Nil
				
				If SubStr(aItens[nI]:_PROD:_CFOP:TEXT,2,3) $ cCfoDev
					lDevol	:= .T.
					Exit
				EndIf
			
			EndIf
		
		Next nI
		
		//|Nota Fiscal de Devolução |
		If lDevol
			
			//|Valida cliente emissor da devolução |
			cCnpjEmi	:= PadR(Alltrim(oXml:_NFE:_INFNFE:_EMIT:_CNPJ:TEXT),TamSX3("A1_CGC")[1])
		
			dbSelectArea("SA1")
			SA1->(dbSetOrder(3))
			If SA1->(dbSeek(xFilial("SA2") + cCnpjEmi))
				cCliente	:= SA2->A2_COD
				cLoja		:= SA2->A2_LOJA
			Else
				ConOut("###### ERRO -> CLIENTE NAO ENCONTRADO - CNPJ: " + cCnpjEmi)
				Return
			EndIf
			
			cEmissao	:= IIf(XmlChildEx(oXml:_NFE:_INFNFE:_IDE, "_DHEMI")<>nil,ConvDate(Substr(oXml:_NFE:_INFNFE:_IDE:_DHEMI:TEXT,1,10)),"")
			cNumNf		:= PadL(AllTrim(oXml:_NFE:_INFNFE:_IDE:_NNF:TEXT),TamSX3("F1_DOC")[1],"0")
			cSerie		:= AllTrim(oXml:_NFE:_INFNFE:_IDE:_SERIE:TEXT)
			
			dbSelectArea("SF1")
			SF1->(dbSetOrder(1))
			If SF1->(dbSeek(xFilial("SF1")+ PadL(Alltrim(cNumNf),TamSX3("F1_DOC")[1]) + PadR(cSerie,TamSX3("F1_SERIE")[1]) + ;
					PadR(Alltrim(cCliente),TamSX3("F1_FORNECE")[1]) + PadR(cLoja,TamSX3("F1_LOJA")[1])))
				
				ConOut("###### ERRO -> Nota No.: "+ Alltrim(SF1->F1_DOC)+"/"+SF1->F1_SERIE+" do Fornec. "+SF1->F1_FORNECE+"/"+SF1->F1_LOJA+" Ja Existe. A Importacao sera interrompida!!")
				Return
				
			EndIf
			
			If Type("oXml:_NfeProc")<> "U"
				oNF := oXml:_NFeProc:_NFe
			Else
				If Type("oXml:_NFe")<> "U"
					oNF := oXml:_NFe
				Else
					ConOut('O arquivo informado nao esta no formato XML ou esta corrompido.')
					Return
				EndIf
			EndIf
			
			//|Rotina para gerar o documento de entrada |
			SFP001()
			
		EndIf
	
	EndIf
	
	
Return



Static Function SFP001()

	Local aCabec 		:= {}
	Local aItens  		:= {}
	Local nX			:= 1
	
	Private aXML		:= {}
	Private oEmitente  	:= oNF:_InfNfe:_Emit
	Private oIdent     	:= oNF:_InfNfe:_IDE
	Private oDestino   	:= oNF:_InfNfe:_Dest
	Private oTotal     	:= oNF:_InfNfe:_Total
	Private oTransp    	:= oNF:_InfNfe:_Transp
	Private oDet       	:= oNF:_InfNfe:_Det
	
	If Type("oNF:_InfNfe:_ICMS")<> "U"
		Private oICM     	:= oNF:_InfNfe:_ICMS
	Else
		Private oICM		:= nil
	Endif
	
	Private oFatura    	:= IIf(Type("oNF:_InfNfe:_Cobr")=="U",Nil,oNF:_InfNfe:_Cobr)
	Private cEdit1		:= Space(15)
	Private _DESCdigit 	:= space(55)
	Private _NCMdigit  	:= space(8)
	Private cChave     	:= oNFe:_NFeProc:_protNFe:_infProt:_chNFe:TEXT
	
	oDet := IIf(ValType(oDet)=="O",{oDet},oDet)
	
	aAdd(aCabec,{"F1_TIPO"   ,"D" 									,Nil,Nil})
	aAdd(aCabec,{"F1_FORMUL" ,"N"									,Nil,Nil})
	aAdd(aCabec,{"F1_DOC"    ,Alltrim(oIdent:_nNF:TEXT)				,Nil,Nil})
	aAdd(aCabec,{"F1_SERIE"  ,oIdent:_serie:TEXT						,Nil,Nil})
	
	If(Type("oNF:_InfNfe:_infAdic:_infCpl:TEXT")<>"U")
		aAdd(aCabec,{"F1_MENNOTA",oNF:_InfNfe:_infAdic:_infCpl:TEXT 	,Nil,Nil})
	EndIf
	
	cCodTrans := Transp()
	Volumes()
	
	If AllTrim(cCodTrans) != ""
		aAdd(aCabec,{"F1_TRANSP", cCodTrans,Nil,Nil})
	EndIf
	
	If(Type("oTransp:_VeicTransp:_Placa:TEXT")<>"U")
		aAdd(aCabec,{"F1_PLACA", oTransp:_VeicTransp:_Placa:TEXT,Nil,Nil})
	Endif
	
	cCgc		:= StrTran(cCnpjEmi,',','')
	cCgc		:= StrTran(cCgc,'.','')
	cCgc		:= StrTran(cCgc,'/','')
	cCgc		:= StrTran(cCgc,'-','')
	
	dbSelectArea("SA1")
	SA1->(dbSetOrder(3))
	SA1->(dbSeek(xFilial("SA1") + cCgc))
	
	cData	:= ""
	If Type('oIdent:_dEmi:TEXT') <> "U"
		cData	:= Alltrim(oIdent:_dEmi:TEXT)
	EndIf
	
	If	cData == "" .And. Type('oIdent:_dhEmi:TEXT') <> "U"
		cData	:= SubStr(Alltrim(oIdent:_dhEmi:TEXT),1, 10)
	EndIf
	
	If Empty(cData)
		cData := DToS(dDatabase)
	EndIf
	
	dData	:= CtoD(Right(cData,2)+'/'+Substr(cData,6,2)+'/'+Left(cData,4))
	aAdd(aCabec,{"F1_EMISSAO",dData,Nil,Nil})
	aAdd(aCabec,{"F1_FORNECE",SA1->A1_COD,Nil,Nil})
	aAdd(aCabec,{"F1_LOJA"   ,SA1->A1_LOJA,Nil,Nil})
	aAdd(aCabec,{"F1_ESPECIE","SPED",Nil,Nil})
	aAdd(aCabec,{"F1_CHVNFE",cChave,Nil,Nil})
	
	For nX := 1 To Len(oDet)
	
		cItemXml	:= oDet[nZ]:_NITEM:TEXT
		aXML		:= {oDet[nZ]}	
		
		If Empty(aXML)
			ConOut("##### ERRO -> Falha na estrutura do array!!")
			Return .F.
		EndIf
		
		cProduto	:= PadR(AllTrim(aXML[nX]:_Prod:_cProd:TEXT),20)
		cUnidMed	:= Right(AllTrim(aXML[nX]:_Prod:_uCom:TEXT),2) 
		
		dbSelectArea("SB1")
		SB1->(dbSetOrder(1))
		SB1->(dbSeek(xFilial("SB1")+ PadR(cProduto,TamSX3("B1_COD")[1])))
		
		aLinha 	:= {}
		
		cNCM		:= IIf(Type("aXML[1]:_Prod:_NCM")=="U",space(12),aXML[1]:_Prod:_NCM:TEXT)
		Chkproc	:= .F.
		
		// DEFINIR AS QUANTIDADES / PREÇO UNITARIO / PRIMEIRA E SEGUNDA UM
		nQtdOri	:= 0
		If Val(aXML[nX]:_Prod:_qCom:TEXT) != 0
			nQtdOri	:= Val(aXML[nX]:_Prod:_qCom:TEXT)
		Else
			nQtdOri	:= Val(aXML[nX]:_Prod:_qTrib:TEXT)
		EndIf
		
		nQtdUM1 	:= 0	// Qtd UM 1
		nQtdUM2 	:= 0	// Qtd UM 2
		nVlrUM1		:= 0	// Valor Unit UM 1
		
		If cUnidMed == SB1->B1_UM
			nQtdUM1		:= nQtdOri
			nQtdUM2		:= 0
			nVlrUM1		:= Val(aXML[nX]:_Prod:_vProd:TEXT) / nQtdOri
		ElseIf SB1->B1_CONV > 0
			nQtdUM1 	:= ConvUM(SB1->B1_COD, 0, nQtdOri, 1)  // PRI UM
			nQtdUM2 	:= nQtdOri  // SEG UM
			nVlrUM1		:= Val(aXML[nX]:_Prod:_vProd:TEXT) / nQtdUM1 // nQtdUM2
			lSegUM		:= .T.
		Else
			nQtdUM1		:= nQtdOri
			nQtdUM2		:= 0
			nVlrUM1		:= Val(aXML[nX]:_Prod:_vProd:TEXT) / nQtdOri
		EndIf
		
		aAdd(aLinha,{"D1_COD"	,SB1->B1_COD,Nil,Nil})
		
		aAdd(aLinha,{"D1_QUANT"	,nQtdUM1,Nil,Nil})
		If nQtdUM2 > 0
			aAdd(aLinha,{"D1_QTSEGUM",nQtdUM2,Nil,Nil})
		EndIf
		aAdd(aLinha,{"D1_VUNIT",Round(nVlrUM1,6),Nil,Nil})
		nQdeOrig   := nQtdOri
		
		aAdd(aLinha,{"D1_TOTAL",Val(aXML[nX]:_Prod:_vProd:TEXT),Nil,Nil})
		
		If Type('aXML[nX]:_Prod:_vOutro:TEXT') != 'U'
			aadd(aLinha,{"D1_DESPESA",Val(aXML[nX]:_Prod:_vOutro:TEXT),Nil,Nil})
		EndIf
		
		If Type('aXML[nX]:_Prod:_vFrete:TEXT') != 'U'
			aadd(aLinha,{"D1_VALFRE",Val(aXML[nX]:_Prod:_vFrete:TEXT),Nil,Nil})
		EndIf
		
		If Type('aXML[nX]:_Prod:_vSeg:TEXT') != 'U'
			aadd(aLinha,{"D1_SEGURO",Val(aXML[nX]:_Prod:_vSeg:TEXT),Nil,Nil})
		EndIf
		
		If Type('aXML[nX]:_Prod:_vDesc:TEXT') != 'U'
			aadd(aLinha,{"D1_VALDESC",Val(aXML[nX]:_Prod:_vDesc:TEXT),Nil,Nil})
		EndIf
		
		cItem 		:= StrZero(nX, TamSX3("D1_ITEM"[1]))
		
		aadd(aLinha,{"D1_TIPO", "D",Nil,Nil})
		
		_cfop:=aXML[nX]:_Prod:_CFOP:TEXT
			
		If Left(Alltrim(_cfop),1)="5"
			_cfop:=Stuff(_cfop,1,1,"1")
		Else
			_cfop:=Stuff(_cfop,1,1,"2")
		EndIf
		
		If Type("oDet[nX]:_Prod:_vDesc")<> "U"
			aadd(aLinha,{"D1_VALDESC",Val(aXML[nX]:_Prod:_vDesc:TEXT),Nil,Nil})
		Else
			aadd(aLinha,{"D1_VALDESC",0,Nil,Nil})
		EndIf	
		
		If Type("aXML[nX]:_Imposto:_IPI:_IPITrib") != "U"
			oIPI	:= aXML[nX]:_Imposto:_IPI:_IPITrib
			aadd(aLinha,{"D1_VALIPI",VAL(oIPI:_vIPI:TEXT),,Nil})
			If Type("aXML[nX]:_Imposto:_IPI:_IPITrib:_pIPI") <> "U"  				                                 
				aadd(aLinha,{"D1_IPI"	,VAL(oIPI:_pIPI:TEXT),,Nil})
			EndIf		  
		EndIf
			
		Do Case
			Case Type("aXML[nX]:_Imposto:_ICMS:_ICMS00")<> "U"
			oICM:=aXML[nX]:_Imposto:_ICMS:_ICMS00
			Case Type("aXML[nX]:_Imposto:_ICMS:_ICMS10")<> "U"
			oICM:=aXML[nX]:_Imposto:_ICMS:_ICMS10
			Case Type("aXML[nX]:_Imposto:_ICMS:_ICMS20")<> "U"
			oICM:=aXML[nX]:_Imposto:_ICMS:_ICMS20
			Case Type("aXML[nX]:_Imposto:_ICMS:_ICMS30")<> "U"
			oICM:=aXML[nX]:_Imposto:_ICMS:_ICMS30
			Case Type("aXML[nX]:_Imposto:_ICMS:_ICMS40")<> "U"
			oICM:=aXML[nX]:_Imposto:_ICMS:_ICMS40
			Case Type("aXML[nX]:_Imposto:_ICMS:_ICMS51")<> "U"
			oICM:=aXML[nX]:_Imposto:_ICMS:_ICMS51
			Case Type("aXML[nX]:_Imposto:_ICMS:_ICMS60")<> "U"
			oICM:=aXML[nX]:_Imposto:_ICMS:_ICMS60
			Case Type("aXML[nX]:_Imposto:_ICMS:_ICMS70")<> "U"
			oICM:=aXML[nX]:_Imposto:_ICMS:_ICMS70
			Case Type("aXML[nX]:_Imposto:_ICMS:_ICMS90")<> "U"
			oICM:=aXML[nX]:_Imposto:_ICMS:_ICMS90
		EndCase
		If Type("oICM:_orig:TEXT")<> "U"
			cOrigProd := oICM:_orig:TEXT
		EndIf
		
		aAdd(aLinha,{"AUTDELETA"	,"N",,Nil})
		
		//|Vincula a NF de origem da devolução |
		dbSelectArea("SD2")
		SD2->(dbSetOrder(3))
		If SD2->(dbSeek(xFilial("SD2") + PADL(Alltrim(oIdent:_nNF:TEXT),TamSX3("F2_DOC")[1]) + PADL(Alltrim(oIdent:_serie:TEXT),TamSX3("F2_DOC")[1]) +; 
					SA1->A1_COD + SA1->A1_LOJA + SB1->B1_COD))
			
			aAdd(aLinha,{"D1_NFORI"		,SD2->D2_DOC,,Nil})
			aAdd(aLinha,{"D1_SERIORI"	,SD2->D2_SERIE,,Nil})
			aAdd(aLinha,{"D1_ITEMORI"	,SD2->D2_ITEM,,Nil})
		
		Else
		
			ConOut("##### ERRO -> NAO FOI POSSIVEL ENCONTRAR A NF ORIGINAL DA DEVOLUCAO NA SD2!")
			Return
			
		EndIf
		
		aAdd(aItens,aLinha)
		
	Next nX
	
	If Len(aItens) > 0
		
		Private lMsErroAuto := .F.
		Private lMsHelpAuto := .T.
		
		SB1->( dbSetOrder(1) )
		SA2->( dbSetOrder(1) )
		
		//|Gera o documento de entrada classificado |
		Begin Transaction
		
		nModulo := 4  //Estoque
		
		MSExecAuto({|x,y,Z| MATA103(x,y,z)},aCabec,aItens,3,.F.)
		
		If lMsErroAuto
			DisarmTransaction()
			ConOut(MostraErro())
		Else    
		
			ConOut("-----> GERADO DOCUMENTO DE ENTRADA DA DEVOLUCAO COM SUCESSO <-----")
			
			//|Altera o status para classificado |
			RecLock("ZZZ",.F.)
			ZZZ->ZZZ_OK	:= "C"
			ZZZ->(MsUnLock())
		
		EndIf
		
		End Transaction
		MsUnlockAll()
		
	EndIf
	
Return


/*
------------------------------------------------------------------------------------------------------------
Função		: Transp
Tipo			: Função de Usuário
Descrição		: Consulta o código da transportadora, caso a mesma esteja cadastrado
Parâmetros	:
Retorno		: Código da transportadora
------------------------------------------------------------------------------------------------------------
Atualizações:
- 20/07/2016 - Pontin - Construção inicial do fonte
------------------------------------------------------------------------------------------------------------
*/

Static Function Transp()
	
	Local cDoc 		:= ""
	Local cCodigo 	:= ""
	
	If Type("oTransp:_Transporta:_CNPJ:TEXT")<>"U"
		cDoc := oTransp:_Transporta:_CNPJ:TEXT
		
	ElseIf Type("oTransp:_Transporta:_CPF:TEXT")<>"U"
		cDoc := oTransp:_Transporta:_CPF:TEXT
		
	EndIf
	
	If AllTrim(cDoc) == ""
		Return()
	EndIf
	
	cCodigo := Posicione("SA4", 3, XFILIAL("SA4")+cDoc, "A4_COD")
	
Return cCodigo


/*
------------------------------------------------------------------------------------------------------------
Função		: Volumes
Tipo			: Função de Usuário
Descrição		: Cadastra os valores referentes ao volume da nota fiscal
Parâmetros	:
Retorno		:
------------------------------------------------------------------------------------------------------------
Atualizações:
- 30/07/2015 - Pontin - Construção inicial do fonte
------------------------------------------------------------------------------------------------------------
*/
Static Function Volumes()
	
	If Type("oTransp:_Vol:_PesoL"	)!="U"
		aadd(aCabec,{"F1_PESOL"  	,Val(oTransp:_Vol:_PesoL:TEXT)	,Nil,Nil})
	EndIf
	
	If Type("oTransp:_Vol:_PesoL"	)!="U"
		aadd(aCabec,{"F1_PLIQUI"  	,Val(oTransp:_Vol:_PesoL:TEXT) 	,Nil,Nil})
	EndIf
	
	If Type("oTransp:_Vol:_PesoB"	)!="U"
		aadd(aCabec,{"F1_PBRUTO"	,Val(oTransp:_Vol:_PesoB:TEXT) 	,Nil,Nil})
	EndIf
	
	If Type("oTransp:_Vol:_Esp"		)!="U"
		aadd(aCabec,{"F1_ESPECI1"  	,oTransp:_Vol:_Esp:TEXT			,Nil,Nil})
	EndIf
	
	If Type("oTransp:_Vol:_nVol"	)!="U" .And. val(oTransp:_Vol:_nVol:TEXT) <= 999999
		aadd(aCabec,{"F1_VOLUME1"	,val(oTransp:_Vol:_nVol:TEXT)	,Nil,Nil})
	EndIf
	
Return
```

_______

## PT015ITE

_______

## PT024CTE

_______

## PTCLIFOR

_______

## PTCTEDAD

_______

## PTX01FIL

_______

## PTX0001MNU

_______

## PTXF1DOC

_______

## PTXF1SER

_______

## PTXJOBSA5

_______

## PX011CTE

_______

## PX041VLD

_______

## SAVEZZZ

_______

## SF1140I

_______

## XCarregDados

