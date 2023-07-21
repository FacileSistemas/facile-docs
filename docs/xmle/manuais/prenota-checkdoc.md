<style>
    p{
        text-align: justify;
    }
</style>

# Checkdoc – Gerar Pré Nota de Entrada

## Resumo dos serviços / Resultado esperado

1.	Gerar pré-nota automaticamente se não houver divergência na avaliação do Checkdoc
2.	Criar parâmetro para ativar/desativar a funcionalidade


## Detalhamento dos Serviços / Observações

1.	Atividades incluídas
    - Automação e agilidade na inclusão das pré-notas


## Informações técnicas / Relevantes

1.	Parâmetros envolvidos na adequação:
    - **ZZ_CHKNOTA:** Parâmetro lógico informando se a geração automática da pré-nota pelo CheckDoc está ativa.
        <span style="color: red">Exemplo: .T.</span>


## Passo a passo

A aplicação do patch com a melhoria e a criação do parâmetro com o valor “.T.” são suficientes para ativar a nova funcionalidade.

Sempre que o CheckDoc verificar o XML e não encontrar divergências, será gerado a pré-nota automaticamente via JOB.
