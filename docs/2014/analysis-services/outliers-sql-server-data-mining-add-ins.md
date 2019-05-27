---
title: Exceções (SQL Server Data Mining Add-ins) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3043c8f63433396f059f5c456512ad4ba2bffd93
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072142"
---
# <a name="outliers-sql-server-data-mining-add-ins"></a>Exceções (Suplementos de Mineração de Dados do SQL Server)
  ![Assistente de exceções na faixa de opções mineração de dados](media/dmc-outliers.gif "Assistente de exceções na faixa de opções mineração de dados")  
  
 Uma *outlier* significa um valor de dados que é problemático por qualquer um dos seguintes motivos:  
  
-   O valor está fora do intervalo esperado.  
  
-   Os dados talvez tenham sido inseridos incorretamente.  
  
-   O valor está faltando.  
  
-   Os dados consistem em um espaço ou outra cadeia de caracteres nula.  
  
-   O valor é preciso, mas até agora está fora da distribuição, o que pode afetar significativamente o modelo.  
  
 O Cliente de Mineração de Dados para Excel o ajuda a detectar esses dados e atualiza ou elimina os valores. Por exemplo, você pode substituir exceções por uma média aritmética ou excluir linhas que contenham valores potencialmente errados.  
  
## <a name="handling-outliers"></a>Manipulando exceções  
 O **remover exceções** assistente oferece várias ferramentas para manipular exceções corretamente:  
  
-   Primeiro, você pode explorar os dados para entender melhor a distribuição dos valores e a relação das exceções para outros dados.  
  
     Por exemplo, você pode usar o **explorar dados** tarefa para examinar e corrigir os valores. O **remover exceções** assistente também exibe um gráfico, uma linha ou um gráfico de barras, para ajudá-lo a entender a distribuição de todos os valores.  
  
-   Em seguida, você pode usar o **exceções** Assistente para remover ou alterar exceções. O método usado depende se os valores são discretos ou contínuos.  
  
     O assistente exibe valores discretos em um gráfico de barras, no qual cada barra representa um valor específico, e a altura da barra indica o número de casos de cada valor. Ao deslizar o controle de limite no gráfico, você pode remover barras que representam grupos de valores potencial ou extremamente incorretos.  
  
-   O assistente exibe valores contínuos em um gráfico de barras ou linha. No gráfico de linha, o valor é representado no eixo x e a contagem de valores no eixo y.  
  
     Você pode controlar se deseja remover ou manter valores nas extremidades baixos e altas do gráfico alterando a **mínimo** e **máximo** valores ou deslizando as barras. À medida que você altera as configurações de valores mínimo e máximo, os dados que serão suprimidos são mostrados pelo sombreamento no grafo.  
  
 Depois que você tiver selecionado com quais exceções trabalhar, informe ao assistente como manipular as exceções. Você pode excluir as linhas que contêm os valores de exceção ou especificar um valor de substituição, como um valor médio, nulo ou outro de sua escolha.  
  
 O assistente lhe dá algumas opções para exibir os novos dados. Você pode substituir os dados originais pelos novos valores, adicionar uma nova coluna à tabela que contém os novos valores ou criar uma nova planilha que contenha os dados atualizados.  
  
### <a name="using-the-outlier-wizard"></a>Usando o Assistente de Exceções  
  
1.  No **Data Mining** faixa de opções, clique em **limpar dados**e selecione **exceções**.  
  
2.  No **Selecionar fonte de dados** caixa de diálogo, selecione uma tabela de dados do Excel ou um intervalo de células e clique em **próxima**.  
  
    > [!WARNING]  
    >  Não é possível usar o **exceções** assistente em dados externos, a menos que você copiá-lo para o Excel pela primeira vez.  
  
3.  No **Selecionar coluna** caixa de diálogo, selecione uma **único** coluna.  
  
     Clique em **Avançar**.  
  
4.  No **especificar limites** caixa de diálogo caixa, examine a distribuição de dados.  
  
    -   Se a coluna contiver valores discretos, o assistente exibirá um histograma contendo a contagem de cada valor discreto.  
  
         Supondo que as exceções são valores raros, você pode filtrá-los fora, alterando a **mínimo** valor.  
  
    -   Se a coluna contiver dados numéricos, você pode clicar na **exibir como discreto** botão ou o **exibir como numérico** botão para alternar entre a exibição dos valores em um gráfico de barras ou linha.  
  
5.  No **especificar limites** caixa de diálogo, escolha o intervalo de dados que você deseja manter digitando um valor mínimo e máximo ou arrastando as barras de controle deslizante. Clique em **Avançar**.  
  
6.  No **manipulação de exceção** diálogo caixa, especifique se deseja que os valores sejam excluídos ou substituídos e clique em **próxima**.  
  
7.  No **Selecionar destino** caixa de diálogo, especifique onde deseja que os novos dados a serem salvos.  
  
### <a name="related-options"></a>Opções relacionadas  
 O assistente fornece as seguintes opções:  
  
|**Opções**|**Comentário**|  
|-----------------|-----------------|  
|**Selecionar coluna**|Você pode trabalhar somente com uma coluna por vez.|  
|**Especificar tratamento de limites**|Defina um limite usando **mínimo** para excluir os valores que são encontrados em menos linhas do que o valor de limite.<br /><br /> Inicialmente, o valor em **mínimo** é igual ao valor com o menor número de linhas, e você não pode fazer com que o mínimo menor que esse valor.|  
|**Manipulação de exceções**|Se você decidir excluir exceções, poderá alterar os dados na planilha atual ou criar uma cópia dos dados em uma nova planilha.|  
  
## <a name="see-also"></a>Consulte também  
 [Explorar dados &#40;suplementos de mineração de dados do SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
  
