---
title: Analisar os influenciadores principais (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- key influencers
- factor analysis
ms.assetid: 54d7b4ce-7b79-407a-985c-aa655ad19280
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2a349ea881e463043aea5bb069d3ed34be74a78b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527982"
---
# <a name="analyze-key-influencers-table-analysis-tools-for-excel"></a>Analisar os Influenciadores Principais (Ferramentas de Análise de Tabela para Excel)
  ![Botão Analisar os Influenciadores Principais na faixa de opções](media/tat-aki.gif "Botão Analisar os Influenciadores Principais na faixa de opções")  
  
 Com a ferramenta **analisar influenciadores principais** , você escolhe uma coluna que contém um resultado de destino e o algoritmo determina quais fatores tinham a influência mais forte sobre o resultado.  
  
 A ferramenta cria novas tabelas de dados que reportam os fatores associados a cada resultado e exibe graficamente a probabilidade de relação. Você pode filtrar as tabelas por fatores e resultados diferentes para explorar os resultados com mais profundidade.  
  
 Você também pode selecionar um par de resultados possíveis e compará-los. Por exemplo, você pode comparar grupos diferentes de consumidores para determinar possíveis fatores de tomada de decisão.  
  
## <a name="using-the-analyze-key-influencers-tool"></a>Usando a ferramenta Analisar os Influenciadores Principais  
  
1.  Abra uma tabela de dados do Excel.  
  
2.  Em **ferramentas de tabela**, na faixa de quadro **analisar** , clique em **analisar influenciadores-chave.**  
  
3.  Selecione a coluna única que é o destino da análise.  
  
4.  Opcionalmente, clique em **escolher colunas a serem usadas para análise**. Na caixa de diálogo **seleção de colunas avançadas** , escolha as colunas que têm mais probabilidade de conter dados relevantes. Para melhorar o desempenho e a precisão, desmarque colunas como ID ou nome que não são importantes para análise de padrão. Clique em **OK** para fechar a caixa de diálogo **seleção de colunas avançadas** .  
  
5.  Clique em **Executar**.  
  
     A ferramenta **analisar influenciadores principais** conduz uma análise dos dados para determinar as configurações ideais e define todos os parâmetros automaticamente.  
  
6.  Se nenhum padrão for detectado, o assistente criará uma nova planilha contendo uma descrição do problema.  
  
7.  Se forem detectados padrões, o assistente criará um relatório em uma nova planilha mostrando esses padrões. O relatório é nomeado **como influenciadores- \<column> chave para **. Você pode personalizar o relatório conforme descrito no procedimento a seguir.  
  
#### <a name="create-a-custom-report"></a>Criar um relatório personalizado  
  
1.  Na caixa de diálogo **discriminação baseada em influenciadores de chave** , escolha os dois valores que você deseja comparar selecionando-os nas listas suspensas **valor 1** e **valor 2** . Por exemplo, você pode comparar compradores a não compradores.  
  
2.  Clique em **Adicionar relatório**.  
  
     O assistente cria uma nova planilha e adiciona uma tabela para cada par de comparações de fatores chave.  
  
3.  Quando terminar de fazer comparações, clique em **fechar**.  
  
## <a name="understanding-the-key-influencers-report"></a>Compreendendo o relatório Influenciadores Principais  
 Após a criação do modelo de dados, a ferramenta **analisar influenciadores principais** cria relatórios que ajudam você a explorar e comparar os influenciadores principais.  
  
-   O relatório no lado esquerdo é gerado por padrão. Ele mostra os preditores mais fortes da coluna de resultado (a variável dependente).  
  
-   O relatório no lado direito é opcional, que você pode criar comparando dois valores de resultado específicos. Esse relatório compara compradores e não compradores.  
  
-   Observe que uma nova planilha será adicionada para cada relatório que você cria. Você pode mover as tabelas depois que elas forem criadas; nós as colocamos lado a lado para comparação.  
  
 ![DM13](media/dm13-tat-aki-report.gif "DM13")  
  
 **Impacto relativo**  
 A barra sombreada no primeiro relatório indica a intensidade da associação desse atributo com o resultado.  
  
 O comprimento da barra indica a probabilidade de o fator colaborar para o resultado; portanto, quanto maior a barra sombreada, mais intensa a associação.  
  
 **Favorece**  
 No segundo relatório, os valores de destino que você compara são listados em duas colunas, com os fatores relacionados listados em ordem decrescente de confiança.  
  
-   A barra **azul** mostra atributos que contribuem para o resultado, "não" (= não adquiriu).  
  
-   A barra **vermelha** mostra atributos que contribuem para o resultado "Sim" (= comprou uma bicicleta).  
  
 As cores na barra de matização são arbitrárias. Você pode alterar estas cores definindo as opções para design de tabela no Excel.  
  
 Em um relatório que compara dois valores, o segundo relatório classificará os influenciadores principais pelo grau de impacto nos valores de destino.  
  
 Como todos os gráficos são baseados nas tabelas do Excel, você pode filtrar e classificar para enfatizar fatores ou resultados específicos.  
  
## <a name="more-about-the-analyze-key-influencers-tool"></a>Mais informações sobre a ferramenta Analisar os Influenciadores Principais  
 Quando a ferramenta **analisar influenciadores principais** analisa seus dados, ela faz o seguinte:  
  
-   Cria uma estrutura de dados que armazena as principais informações sobre a distribuição dos dados.  
  
-   Cria um modelo usando o algoritmo Naïve Bayes da Microsoft.  
  
-   Cria previsões que correlacionam cada coluna de dados com o resultado especificado.  
  
-   Usa a pontuação de confiança para cada uma das previsões para identificar os fatores que são mais influentes na geração do resultado desejado.  
  
-   Cria um relatório que descreve os influenciadores principais, ordenados por pontuações de confiança.  
  
### <a name="requirements"></a>Requisitos  
 Se a coluna de destino contiver valores numéricos contínuos, a ferramenta segmentará automaticamente os valores numéricos em grupos. Esses agrupamentos representam clusters de casos com características semelhantes. No entanto, talvez os valores numéricos não sejam divididos em grupos amigáveis com o usuário. Por exemplo, o relatório pode conter um agrupamento como " \< 12,85701", enquanto os usuários de relatório normalmente gostam de ver agrupamentos que usam números inteiros, como 10-19, 20-29 e assim por diante.  
  
 Se você quiser agrupar dados numéricos de um modo diferente, será necessário segmentar os dados da maneira desejada antes de criar a análise. Por exemplo, você pode usar a ferramenta de [rerotulação](relabel-sql-server-data-mining-add-ins.md) no cliente de mineração de dados para Excel para criar um novo rótulo de agrupamento em uma coluna separada e, em seguida, usar apenas essa nova coluna na análise.  
  
### <a name="related-tools"></a>Ferramentas relacionadas  
 A faixa de informações de **mineração de dados** fornece ferramentas mais avançadas, incluindo a capacidade de personalizar modelos de Data Mining  
  
 Se você salvar seu modelo usando a ferramenta **analisar influenciadores principais** , poderá usar o cliente de mineração de dados para procurar o modelo e explorar relações com mais detalhes. Para obter informações, consulte [procurando modelos no Excel &#40;SQL Server suplementos de mineração de dados&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md). Também é possível usar o Microsoft Office Visio para criar gráficos e diagramas que exibem as relações como cluster ou redes de dependências. Para obter mais informações, consulte [solução de problemas de diagramas de mineração de dados do Visio &#40;SQL Server suplementos de mineração de dados&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md).  
  
> [!NOTE]  
>  Os modelos criados quando você usa as Ferramentas de Análise de Tabela são excluídas quando você fecha a planilha ou encerra a conexão com o servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Portanto, você pode procurar os modelos contanto que a conexão permaneça aberta. Você não pode renderizar os modelos no Visio se fechar a conexão ou a planilha.  
  
 Para obter mais informações sobre o algoritmo usado pela ferramenta **analisar influenciadores de chave** , consulte "algoritmo Bayes do Microsoft ingênua" em manuais online do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de análise de tabela para Excel](table-analysis-tools-for-excel.md)   
 [Criar um modelo de mineração de dados](creating-a-data-mining-model.md)  
  
  
