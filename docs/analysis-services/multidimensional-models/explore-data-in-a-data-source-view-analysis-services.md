---
title: "Explorar dados em uma exibição da fonte de dados (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exploring data [Analysis Services]
- data source views [Analysis Services], exploring data
- viewing source data
ms.assetid: 2c922c35-fbcb-45b2-96b1-c7a846d8b419
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de15507d7fedd1f582e158e85d1f6245972cf27b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="explore-data-in-a-data-source-view-analysis-services"></a>Explorar dados em uma exibição da fonte de dados (Analysis Services)
  Você pode usar a caixa de diálogo **Explorar Dados** do Designer de Exibição da Fonte de Dados do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para procurar dados para uma tabela, exibição ou consulta nomeada de uma DSV (exibição da fonte de dados). Ao explorar os dados no Designer de Exibição da Fonte de Dados, você pode exibir o conteúdo de cada coluna de dados da tabela, exibição ou consulta nomeada selecionada. Exibir o conteúdo real é útil para determinar se todas as colunas são necessárias, se os cálculos nomeados são requeridos para torná-los mais amigável para o usuário e melhorar a usabilidade e se os cálculos nomeados ou as consultas nomeadas existentes retornam os valores previstos.  
  
 Para exibir os dados, é necessária uma conexão ativa com a(s) fonte(s) de dados do objeto selecionado na DSV (exibição da fonte de dados). Todos os cálculos nomeados de uma tabela também são enviados na consulta.  
  
 Os dados retornados em um formato de tabela que você pode classificar e copiar. Clique nos cabeçalhos das colunas para reclassificar as linhas das respectivas colunas. Você também pode realçar dados na grade e pressionar Ctrl-C para copiar a seleção para a área de transferência.  
  
 Você também pode controlar o método de exemplo e a contagem de exemplo. Por padrão, as 5.000 primeiras linhas são retornadas.  
  
## <a name="to-browse-data-or-change-sampling-options"></a>Para procurar dados ou alterar opções de amostragem  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto ou conecte-se ao banco de dados que contém a exibição da fonte de dados na qual você deseja procurar dados.  
  
2.  No Gerenciador de Soluções, expanda a pasta **Exibições da Fonte de Dados** e clique duas vezes na exibição da fontes de dados.  
  
3.  Clique com o botão direito do mouse na tabela, exibição ou consulta nomeada que contém os dados que você deseja exibir e, em seguida, clique em **Explorar Dados**.  
  
     Os dados de origem subjacente da tabela, exibição, ou consulta nomeada na exibição da fonte de dados são consultas e os resultados aparecem no **explorar \<nome do objeto > tabela** guia.  
  
4.  Sobre o **explorar \<nome do objeto > tabela** barra de ferramentas, clique no **opções de amostragem** ícone.  
  
     A caixa de diálogo **Opções de Exploração de Dados** é aberta. Nela você pode especificar o método de amostragem (menos ou mais registros que o tamanho de amostragem padrão de 5000 linhas) ou a contagem de exemplo.  
  
5.  Clique em **OK** ou em **Cancelar** , conforme apropriado.  
  
6.  Para obter uma nova amostra dos dados, clique em **criar nova amostra dos dados** no **explorar \<nome do objeto > tabela** barra de ferramentas.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  

