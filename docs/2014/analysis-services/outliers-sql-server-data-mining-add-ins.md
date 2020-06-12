---
title: Exceções (SQL Server suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- exceptions [data mining]
- data preparation
- outliers [data mining]
- data cleaning
ms.assetid: e6fa7c62-4005-4792-9211-3b699377a517
author: minewiskan
ms.author: owend
ms.openlocfilehash: ecc7cba81a394664b2bdb6a60b6c5f8110760f44
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547273"
---
# <a name="outliers-sql-server-data-mining-add-ins"></a>Exceções (Suplementos de Mineração de Dados do SQL Server)
  ![Assistente de Exceções na faixa de opções Mineração de Dados](media/dmc-outliers.gif "Assistente de Exceções na faixa de opções Mineração de Dados")  
  
 Uma *exceção* significa um valor de dados que é problemático por qualquer um dos seguintes motivos:  
  
-   O valor está fora do intervalo esperado.  
  
-   Os dados talvez tenham sido inseridos incorretamente.  
  
-   O valor está faltando.  
  
-   Os dados consistem em um espaço ou outra cadeia de caracteres nula.  
  
-   O valor é preciso, mas até agora está fora da distribuição, o que pode afetar significativamente o modelo.  
  
 O Cliente de Mineração de Dados para Excel o ajuda a detectar esses dados e atualiza ou elimina os valores. Por exemplo, você pode substituir exceções por uma média aritmética ou excluir linhas que contenham valores potencialmente errados.  
  
## <a name="handling-outliers"></a>Manipulando exceções  
 O assistente para **remover exceções** oferece várias ferramentas para lidar com exceções adequadamente:  
  
-   Primeiro, você pode explorar os dados para entender melhor a distribuição dos valores e a relação das exceções para outros dados.  
  
     Por exemplo, você pode usar a tarefa **explorar dados** para revisar e corrigir os valores. O assistente para **remover exceções** também exibe um gráfico, uma linha ou um gráfico de barras, para ajudá-lo a entender a distribuição de todos os valores.  
  
-   Em seguida, você pode usar o assistente de **exceções** para remover ou alterar exceções. O método usado depende se os valores são discretos ou contínuos.  
  
     O assistente exibe valores discretos em um gráfico de barras, no qual cada barra representa um valor específico, e a altura da barra indica o número de casos de cada valor. Ao deslizar o controle de limite no gráfico, você pode remover barras que representam grupos de valores potencial ou extremamente incorretos.  
  
-   O assistente exibe valores contínuos em um gráfico de barras ou linha. No gráfico de linha, o valor é representado no eixo x e a contagem de valores no eixo y.  
  
     Você pode controlar se deseja remover ou manter os valores nas extremidades inferior e superior do gráfico, alterando os valores **mínimo** e **máximo** , ou deslizando as barras. À medida que você altera as configurações de valores mínimo e máximo, os dados que serão suprimidos são mostrados pelo sombreamento no grafo.  
  
 Depois que você tiver selecionado com quais exceções trabalhar, informe ao assistente como manipular as exceções. Você pode excluir as linhas que contêm os valores de exceção ou especificar um valor de substituição, como um valor médio, nulo ou outro de sua escolha.  
  
 O assistente lhe dá algumas opções para exibir os novos dados. Você pode substituir os dados originais pelos novos valores, adicionar uma nova coluna à tabela que contém os novos valores ou criar uma nova planilha que contenha os dados atualizados.  
  
### <a name="using-the-outlier-wizard"></a>Usando o Assistente de Exceções  
  
1.  Na faixa de opções **mineração de dados** , clique em **limpar dados**e selecione **exceções**.  
  
2.  Na caixa de diálogo **selecionar dados de origem** , selecione uma tabela de dados do Excel ou um intervalo de células e clique em **Avançar**.  
  
    > [!WARNING]  
    >  Você não pode usar o assistente de **exceções** em dados externos, a menos que você o copie para o Excel primeiro.  
  
3.  Na caixa de diálogo **Selecionar coluna** , selecione uma **única** coluna.  
  
     Clique em **Próximo**.  
  
4.  Na caixa de diálogo **especificar limites** , examine a distribuição de dados.  
  
    -   Se a coluna contiver valores discretos, o assistente exibirá um histograma contendo a contagem de cada valor discreto.  
  
         Supondo que as exceções sejam raras, você pode filtrá-las alterando o valor **mínimo** .  
  
    -   Se a coluna contiver dados numéricos, você poderá clicar no botão **Exibir como discreto** ou **Exibir como botão numérico** para alternar entre a exibição dos valores em um gráfico de barras ou em um gráfico de linhas.  
  
5.  Na caixa de diálogo **especificar limites** , escolha o intervalo de dados que você deseja manter digitando um valor mínimo e máximo ou arrastando as barras de controle deslizante. Clique em **Próximo**.  
  
6.  Na caixa de diálogo **tratamento** de exceções, especifique se deseja que os valores sejam excluídos ou substituídos e clique em **Avançar**.  
  
7.  Na caixa de diálogo **Selecionar destino** , especifique onde você deseja que os novos dados sejam salvos.  
  
### <a name="related-options"></a>Opções relacionadas  
 O assistente fornece as seguintes opções:  
  
|**Opções**|**Comentário**|  
|-----------------|-----------------|  
|**Selecionar coluna**|Você pode trabalhar somente com uma coluna por vez.|  
|**Especificar tratamento de limites**|Defina um limite usando o **mínimo** para excluir valores que são encontrados em menos linhas do que o valor do limite.<br /><br /> Inicialmente, o valor no **mínimo** é igual ao valor com menos linhas, e você não pode tornar o mínimo menor que esse valor.|  
|**Manipulação de Exceções**|Se você decidir excluir exceções, poderá alterar os dados na planilha atual ou criar uma cópia dos dados em uma nova planilha.|  
  
## <a name="see-also"></a>Consulte Também  
 [Explorar dados &#40;SQL Server suplementos de mineração de dados&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
  
