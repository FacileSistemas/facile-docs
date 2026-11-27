# SAVEZZZ

O SAVEZZZ é um ponto de entrada para manipular a ZZZ após gravação. 

O presente ponto de entrada é executado tanto em job, quanto em tela. É necessário tomar cuidado com as funções visuais a serem utilizadas.

Nesse momento a ZZZ já está gravada e após o MsUnLock, ela ainda segue posicionada no registro que acabou de criar ou alterar. 

O SAVEZZZ pode servir para excluir registros, exportar o XML logo após a gravação dele na ZZZ ou para gravar o conteúdo de campos personalizados. 


## Parâmetros

* **Paramixb[1]:** logical, .T. se é uma alteração de status no documento já gravado; .F. quando o documento está sendo salvo pela primeira vez.


## Exclusão de documento

Após a exclusão do registro na ZZZ usando esse ponto de entrada, ele é desconsiderado nos relatórios e na tela do Central XML-e. Ele ainda consta nas tabelas de log, para facilitar a análise de documentos faltantes.

Salientamos que a exclusão de qualquer registro da ZZZ via ponto de entrada é de responsabilidade do cliente e não possui exemplo nesta documentação.

## Exemplo de utilização

O exemplo abaixo é ilustrativo e não deve ser utilizado em produção sem revisão e adaptação à regra de negócio do cliente.

```AdvPL
User Function SAVEZZZ()

	Local cTipoDocumento := ""
	Local cError         := ""
	Local cTipoCTE			 := ""
	Local oError         := Nil
    Local bError         := ErrorBlock({|oError| cError := oError:Description})

	Begin Sequence

	If !Empty(ZZZ->ZZZ_XML)	//|Em alguns casos (NF-e resumida) o XML chega depois |

		If AllTrim(ZZZ->ZZZ_TIPO) == "2" .And. ZZZ->ZZZ_SITDOC == "1"	//|CT-E autorizado |

			cTipoDocumento := U_PTXTipoDocumento()

			cTipoCTE	:= SuperGetMV("MC_YTPCTE", .F., "CTEV/CTEC")

			If cTipoDocumento $ cTipoCTE	//|CTEV = CTE de Venda / CTEC = CTE de compra |

				//|Grava o XML em arquivo |
				Exporta_XML_Disco(cTipoDocumento)

			EndIf

		EndIf
	
	EndIf

	End Sequence

  ErrorBlock(bError)

  If !Empty(cError)
    ConOut( "### ERRO PONTO DE ENTRADA SAVEZZZ " + CRLF + CRLF + cError )
  EndIf

Return



Static Function Exporta_XML_Disco(cTipoDocumento)

	Local cDiretorio   as Character
	Local cNomeArquivo as Character

	cDiretorio	:= SuperGetMV( "MC_YXMLDIR", .F., "\facile\cte\" )

	If !Empty( cDiretorio )

		If Right(cDiretorio,1) != "\"
			cDiretorio += "\"
		EndIf

		If !ExistDir(cDiretorio)
			FWMakeDir( cDiretorio )
		EndIf

		cNomeArquivo	:= AllTrim(ZZZ->ZZZ_CHAVE) + "-" + "prot" + cTipoDocumento + ".xml"

		If File( cDiretorio + cNomeArquivo )
			fErase(cDiretorio + cNomeArquivo)
		EndIf
		
		nHandle  := FCreate( cDiretorio + cNomeArquivo )
		
		If nHandle > 0

			FWrite( nHandle, AllTrim(ZZZ->ZZZ_XML) )
			FClose(nHandle)

		EndIf

	Else

		ConOut( "FACILE - PE SAVEZZZ -> Parametro MC_YXMLDIR nao existe ou esta vazio, nao foi possivel salvar o XML no disco" )

	EndIf

Return
```


## Como testar

O SAVEZZZ é executado em qualquer fluxo de gravação de XML da ferramenta, sendo assim, a função "Importar XML do Computador" presente no PTX0001 (Central XML), é a forma ideal de realizar os testes dessa função, verificando se o processo foi devidamente adaptado para o fluxo de importação ou se foi quebrado durante a execução.


## Consequências

O fluxo de personalização do SAVEZZZ pode interferir em toda recepção de documentos pelo Facile XML-e. É necessário extrema cautela na personalização deste fluxo. Diferentemente do XCarregDados, os erros não interferem na tabela de log FACX002, ou sequer na gravação, mas eventuais erros podem interferir no fluxo de download dos XMLs, interrompendo os serviços de download ou até impedindo o processo de ser finalizado.

Com isso em mente, a personalização desse fluxo foge do suporte usual do Facile XML-e, necessitando de um consultor para apoio ou análise de qualquer eventual problema, sendo necessário acionar o comercial da Facile Soluções em Sistemas.
