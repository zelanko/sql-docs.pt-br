---
title: Realçar exceções (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- highlight exceptions
ms.assetid: d90a12f8-7bc3-4fdb-95a1-7c89058f0d9a
author: minewiskan
ms.author: owend
ms.openlocfilehash: ab9289705bbea8d1e2c21d5f5820746e58b48cc5
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544278"
---
# <a name="highlight-exceptions-table-analysis-tools-for-excel"></a>Realçar Exceções (Ferramentas de Análise de Tabela para Excel)
  ![Botão Realçar Exceções na faixa de opções](media/tat-highlightex.gif "Botão Realçar Exceções na faixa de opções")  
  
 Às vezes, seus dados podem conter valores peculiares. Por exemplo, a idade de um proprietário de imóvel talvez seja listada como cinco anos. Esses valores, geralmente chamados de *exceções*, podem estar errados devido a um erro de entrada de dados ou podem indicar tendências incomuns. De qualquer forma, as exceções podem afetar a qualidade da sua análise. A ferramenta **realçar exceções** ajuda a encontrar esses valores e analisá-los para uma ação adicional.  
  
 A ferramenta **realçar exceções** pode trabalhar com todo o intervalo de dados em uma tabela de dados do Excel ou você pode selecionar apenas algumas colunas. Também é possível ajustar um limite que controla a variação dos dados, para obter mais ou menos exceções.  
  
 Quando a ferramenta conclui sua análise, ela cria uma nova planilha que contém um relatório resumido da quantidade de exceções encontradas em cada coluna analisada. A ferramenta também realça as exceções na tabela de dados original. Como a ferramenta analisa as tendências gerais, talvez descubra que a maioria dos valores em uma linha são normais e realce apenas uma célula nessa linha. No exemplo de proprietários acima, somente a coluna **idade** pode ser realçada.  
  
 Você também pode alterar o valor de **limite de exceção** no **relatório de resumo**. Esse valor indica a probabilidade de uma determinada célula conter um valor anormal. Em virtude disso, se você aumentar o valor, menos valores serão realçados como exceções. Por outro lado, quando diminuir o valor, você verá mais células realçadas.  
  
## <a name="using-the-highlight-exceptions-tool"></a>Usando a ferramenta Realçar Exceções  
  
1.  Abra uma tabela do Excel e clique em **realçar exceções**.  
  
2.  Especifique as colunas a serem analisadas.  
  
3.  Clique em **Executar**.  
  
4.  Abra a planilha intitulada \<table name> exceções para exibir um resumo das exceções que foram encontradas.  
  
5.  Para alterar o número de realces, clique nas setas para cima e para baixo na linha **limite de exceção** do **relatório de realce de exceções**.  
  
### <a name="requirements"></a>Requisitos  
 Você poderá incluir colunas que não contenham valores inválidos se esses valores tiverem informações que possam ser úteis na previsão de outras linhas. No entanto, será necessário desmarcar as colunas que tenham muitos valores de zero ou ausentes.  
  
 Como todas as colunas selecionadas são usadas para criar um padrão geral, evite utilizar como entrada colunas que sabidamente têm informações inadequadas, como as seguintes:  
  
-   Colunas que contêm valores exclusivos, como IDs.  
  
-   Colunas que contêm uma alta porcentagem de valores incorretos.  
  
-   Colunas com muitos valores ausentes.  
  
     Observe que em alguns casos, é útil incluir colunas de entrada que têm muitos valores ausentes. Por exemplo, se o valor do campo de endereço está sempre ausente quando o cliente compra por meio de um fornecedor, o algoritmo de mineração de dados pode usar essas informações para identificar outros clientes semelhantes. Você deve determinar caso a caso se dados estão ausentes por omissão ou porque o estado Ausente é significativo.  
  
-   As colunas que provavelmente não serão úteis na criação de um padrão. Por exemplo, uma coluna que tenha o mesmo valor a cada linha não adiciona informações que seriam úteis na criação de padrões.  
  
## <a name="understanding-the-highlight-exceptions-report"></a>Entendendo o Relatório de Realçar Exceções  
 Quando você clica em **executar**, a ferramenta faz três coisas:  
  
-   Cria uma estrutura de mineração de dados com base nos dados atuais da tabela.  
  
-   Cria um novo modelo de mineração de dados usando o algoritmo de Clustering da [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   Cria uma consulta de previsão com base nos padrões para determinar se os valores na planilha são improváveis.  
  
 O valor inicial do limite de exceção é sempre 75, o que significa que o algoritmo calculou que há uma possibilidade de 75% de os dados realçados estarem errados. A ferramenta define automaticamente esse limite para a passagem da análise inicial, mas você pode alterar o valor no relatório.  
  
 A ferramenta **realçar exceções** realça as células na tabela de dados original que são suspeitas. Um realce escuro indica que a linha precisa de atenção. Um realce brilhante indica que o valor nessa célula em particular foi identificado como suspeito. Se você alterar o limite de exceções, os valores realçados serão devidamente alterados.  
  
 O gráfico de resumo mostra o número de células em cada coluna que ficaram acima do limite de exceção.  
  
## <a name="related-tools"></a>Ferramentas relacionadas  
 Quando você estiver limpando ou examinando dados em preparação para mineração de dados, também poderá tentar os recursos de exploração de dados no Cliente de Mineração de Dados para Excel. Esse suplemento fornece mais ferramentas avançadas para ajudá-lo a encontrar exceções, rotular dados novamente ou exibir a distribuição dos dados. Para obter mais informações sobre ferramentas de exploração de dados no cliente de mineração de dados para Excel, consulte [explorando e limpando dados](exploring-and-cleaning-data.md).  
  
 A ferramenta **realçar exceções** usa o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo clustering. Um modelo de clustering detecta grupos de linhas que compartilham características semelhantes. O cliente de mineração de dados para Excel fornece uma janela de **procura** que usa grafos e perfis de características para permitir que você explore Data Mining modelos criados pelo clustering. Para obter informações sobre como procurar o modelo de clustering criado pela ferramenta **realçar exceções** , consulte [procurar modelos (cliente de mineração de dados para Excel)](highlight-exceptions-table-analysis-tools-for-excel.md).  
  
 Para obter mais informações sobre o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering, consulte o tópico "Algoritmo Microsoft Clustering" nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
