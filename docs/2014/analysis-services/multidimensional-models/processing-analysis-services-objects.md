---
title: Processamento do Analysis Services objetos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- OLAP objects [Analysis Services], processing
- OLAP objects [Analysis Services]
ms.assetid: c7e1f66f-16ca-43da-b8c7-4d3e1fa8b58d
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 45fc3c5f6ba3effb69518987256b052f5225cd25
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130459"
---
# <a name="processing-analysis-services-objects"></a>Processando objetos do Analysis Services
  O processamento afeta os seguintes tipos de objeto do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] : bancos de dados, cubos, dimensões, grupos de medidas, partições e estruturas e modelos de mineração de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para cada objeto, é possível especificar o nível de processamento ou selecionar a opção Processar Padrão para habilitar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a selecionar automaticamente o nível ideal de processamento. Para obter mais informações sobre os diferentes níveis de processamento para cada objeto, consulte [Processamento de opções e configurações &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
 É necessário conhecer as consequências do comportamento do processamento para reduzir a ocorrência de repercussões negativas. Por exemplo, processar automaticamente uma dimensão por completo define todas as partições dependentes daquela dimensão como um estado não processado. Desse modo, os cubos afetados ficam indisponíveis para consulta até as partições dependentes serem processadas.  
  
 Este tópico inclui as seguintes seções:  
  
 [Processando um banco de dados](#bkmk_procdb)  
  
 [Processando uma dimensão](#bkmk_procdim)  
  
 [Processando um cubo](#bkmk_proccube)  
  
 [Processando um grupo de medidas](#bkmk_procmeasure)  
  
 [Processando uma partição](#bkmk_procpartition)  
  
 [Processando estruturas e modelos de mineração de dados](#bkmk_procdm)  
  
##  <a name="bkmk_procdb"></a> Processando um banco de dados  
 No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], um banco de dados contém objetos, mas não os dados. Quando você processa um banco de dados, direciona o servidor para processar recursivamente os objetos que armazenam os dados no modelo, como dimensões, partições, estruturas de mineração e modelos de mineração.  
  
 Ao processar um banco de dados, algumas ou todas as partições, dimensões e modelos de mineração contidas no banco de dados são processadas. O tipo de processamento real varia, dependendo do estado de cada objeto e da opção de processamento selecionada. Para obter mais informações, consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
##  <a name="bkmk_proccube"></a> Processando um cubo  
 Um cubo pode ser considerado como um objeto de wrapper para grupos de medidas e partições. Um cubo é feito de dimensões além de uma ou mais medidas, que são armazenadas em partições. As dimensões definem como os dados são dispostos no cubo. Ao processar um cubo, uma consulta SQL é emitida para recuperar valores da tabela de fatos a fim de popular cada membro do cubo com valores de medida adequados. Para qualquer caminho específico para um nó no cubo, há um valor ou um valor calculável.  
  
 Ao processar um cubo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processa todas as dimensões não processadas no cubo e algumas ou todas as partições dos grupos de medidas no cubo. As especificações dependem do estado dos objetos no início do processamento e da opção de processamento selecionada. Para obter mais informações sobre as opções de processamento, consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
 O processamento de um cubo cria arquivos legíveis por máquina que armazenam dados de fatos relevantes. Se alguma agregação for criada, ela será armazenada em arquivos de dados de agregação. O cubo está disponível para ser procurado por meio do Pesquisador de Objetos no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou do Gerenciador de Soluções no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
##  <a name="bkmk_procdim"></a> Processando uma dimensão  
 Ao processar uma dimensão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] formula e executa consultas em tabelas de dimensão para retornar informações necessárias para o processamento.  
  
|País|Região de vendas|Estado|  
|-------------|------------------|-----------|  
|Estados Unidos|Oeste|Califórnia|  
|Estados Unidos|Oeste|Oregon|  
|Estados Unidos|Oeste|Washington|  
  
 O próprio processamento transforma os dados da tabela em hierarquias utilizáveis. Essas hierarquias são nomes de membro completamente articulados que são representados internamente através de caminhos numéricos exclusivos. O exemplo a seguir é uma representação de texto de uma hierarquia.  
  
||  
|-|  
|[United States]|  
|[United States].[Oeste]|  
|[United States].[Oeste].[Califórnia]|  
|[United States].[Oeste].[Oregon]|  
|[United States].[Oeste].[Washington]|  
  
 O processamento da dimensão não cria nem atualiza membros calculados, que são definidos no nível do cubo. Os membros calculados são afetados quando a definição de cubo é atualizada. Além disso, o processamento da dimensão não cria nem atualiza agregações. No entanto, o processamento pode provocar o descarte de agregações. As agregações são criadas ou atualizadas somente durante o processamento da partição.  
  
 Ao processar uma dimensão, observe que a dimensão pode ser usada em vários cubos. Durante o processamento, esses cubos são marcados como não processados e se tornam indisponíveis para consultas. Para processar simultaneamente a dimensão e os cubos relacionados, use as configurações de processamento em lotes. Para obter mais informações, consulte [Batch Processing &#40;Analysis Services&#41;](batch-processing-analysis-services.md).  
  
##  <a name="bkmk_procmeasure"></a> Processando um grupo de medidas  
 Ao processar um grupo de medidas, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processa algumas ou todas as partições do grupo e todas as dimensões não processadas que participam do grupo de medidas. As especificações do trabalho de processamento dependem da opção de processamento selecionada. É possível processar um ou mais grupos de medidas no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sem afetar outros grupos de medidas em um cubo.  
  
> [!NOTE]  
>  Os grupos de medidas individuais podem ser processados de modo programático ou com o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Não é possível processar grupos de medidas individuais no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]; no entanto, é possível processar por partição.  
  
##  <a name="bkmk_procpartition"></a> Processando uma partição  
 A administração eficaz do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] envolve a prática de particionar dados. O processamento da partição é exclusivo porque considera o uso do disco rígido e as limitações de espaço, além dos limites de estrutura de dados impostos pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para manter tempos de resposta de consulta rápidos e uma alta taxa de processamento, é necessário criar, processar e mesclar partições regularmente. É muito importante reconhecer e gerenciar casos de integração de dados redundantes durante a mesclagem de partições. Para obter mais informações, consulte [Mesclar partições no Analysis Services &#40;SSAS – Multidimensional&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md).  
  
 Ao processar uma partição, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processa a partição e qualquer dimensão não processada que exista na partição, dependendo da opção selecionada. O uso de partições oferece várias vantagens para o processamento. É possível processar uma partição sem afetar outras partições em um cubo. As partições são úteis para armazenar dados que estão sujeitos ao write-back de célula. Write-back é um recurso que permite ao usuário realizar uma análise hipotética gravando novos dados na partição para observar o efeito das alterações projetadas. Uma partição de write-back é necessária se o recurso de write-back de célula do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]for utilizado. O processamento de partições em paralelo é útil porque o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa a energia de processamento de modo mais eficaz e pode reduzir consideravelmente o tempo total do processamento. Também é possível processar partições consecutivamente.  
  
##  <a name="bkmk_procdm"></a> Processando estruturas e modelos de mineração de dados  
 Uma estrutura de mineração define o domínio de dados a partir do qual serão criados modelos de mineração de dados. Uma estrutura de mineração pode conter mais de um modelo de mineração. É possível processar uma estrutura de mineração separada dos modelos de mineração associados. Ao ser processada separadamente, uma estrutura de mineração é populada com os dados de treinamento da fonte de dados.  
  
 Quando um modelo de mineração de dados é processado, os dados de treinamento passam pelos algoritmos do modelo de mineração, treinam o modelo usando o algoritmo de mineração de dados e criam o conteúdo. Para obter mais informações sobre a estrutura e o modelo de mineração de dados, consulte [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](../data-mining/mining-structures-analysis-services-data-mining.md).  
  
 Para obter mais informações sobre os modelos e estruturas de mineração de processamento, consulte [Requisitos e considerações de processamento &#40;Data Mining&#41;](../data-mining/processing-requirements-and-considerations-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas e abordagens para processamento &#40;do Analysis Services&#41;](tools-and-approaches-for-processing-analysis-services.md)   
 [O processamento em lotes &#40;do Analysis Services&#41;](batch-processing-analysis-services.md)   
 [Processamento de objetos de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md)  
  
  