---
title: Executar uma carga incremental de várias tabelas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],multiple tables
ms.assetid: 39252dd5-09c3-46f9-a17b-15208cfd336d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d1549b8fa0979bba109c84485a89384722c82e7d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62835392"
---
# <a name="perform-an-incremental-load-of-multiple-tables"></a>Executar uma carga incremental de várias tabelas
  No tópico [Melhorando cargas incrementais com o Change Data Capture](change-data-capture-ssis.md), o diagrama ilustra um pacote básico que executa uma carga incremental em apenas uma tabela. No entanto, carregar uma tabela não é tão comum quanto ter que realizar uma carga incremental de diversas tabelas.  
  
 Ao executar uma carga incremental de diversas tabelas, algumas etapas devem ser realizadas uma vez para todas as tabelas e outras etapas devem ser repetidas para cada tabela de origem. Você tem mais de uma opção para implementar estas etapas no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:  
  
-   Usar um pacote pai e pacotes filho.  
  
-   Usar diversas tarefas de Fluxo de Dados em um único pacote.  
  
## <a name="loading-multiple-tables-by-using-a-parent-package-and-multiple-child-packages"></a>Carregando diversas tabelas usando um pacote pai e diversos pacotes filho  
 É possível usar um pacote pai para executar essas etapas que só precisam ser executadas uma vez. Os pacotes filho executarão essas etapas que precisam ser executadas para cada tabela de origem.  
  
#### <a name="to-create-a-parent-package-that-performs-those-steps-that-only-have-to-be-done-once"></a>Para criar um pacote pai que executa essas etapas que só precisam ser executadas uma vez  
  
1.  Crie um pacote pai.  
  
2.  No fluxo de controle, use uma tarefa Executar SQL ou expressões do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para calcular os pontos de extremidade.  
  
     Para obter um exemplo de como calcular os pontos de extremidade, consulte [Especificar um intervalo de dados de alteração](specify-an-interval-of-change-data.md).  
  
3.  Se necessário, use um contêiner Loop For para atrasar a execução até que os dados de alteração para o período selecionado estejam prontos.  
  
     Para obter um exemplo de um contêiner Loop For desse tipo, consulte [Determinar se os dados de alteração estão prontos](determine-whether-the-change-data-is-ready.md).  
  
4.  Use diversas tarefas Executar Pacote para executar pacotes filho para cada tabela a ser carregada. Passe os pontos de extremidade calculados no pacote pai para cada pacote filho usando as Configurações de Variáveis do Pacote Pai.  
  
     Para obter mais informações, consulte [Tarefa Executar Pacote](../control-flow/execute-package-task.md) e [Usar os valores de variáveis e parâmetros em um pacote filho](../use-the-values-of-variables-and-parameters-in-a-child-package.md).  
  
#### <a name="to-create-child-packages-to-perform-those-steps-that-have-to-be-done-for-each-source-table"></a>Para criar pacotes filho para executar as etapas que precisam ser executadas para cada tabela de origem  
  
1.  Para cada tabela de origem, crie um pacote filho.  
  
2.  No fluxo de controle, use uma tarefa Script ou Executar SQL para montar a instrução SQL que será usada para consultar a existência de alterações.  
  
     Para obter um exemplo de como montar a consulta, consulte [Preparar para consultar os dados de alteração](prepare-to-query-for-the-change-data.md).  
  
3.  Use uma tarefa de Fluxo de Dados simples em cada pacote filho para carregar os dados de alteração e aplicá-los no destino. Configure o Fluxo de Dados conforme descrito nas seguintes etapas:  
  
    1.  No fluxo de dados, use um componente de origem para consultar as tabelas de alterações para as alterações que caem dentro dos pontos de extremidade selecionados.  
  
         Para obter um exemplo de como consultar as tabelas de alteração, consulte [Recuperar e compreender os dados de alteração](retrieve-and-understand-the-change-data.md).  
  
    2.  Use uma transformação de Divisão Condicional para direcionar as inserções, atualizações e exclusões para saídas diferentes para o processamento apropriado.  
  
         Para obter um exemplo de como configurar essa transformação para direcionar a saída, consulte [Processar inserções, atualizações e exclusões](process-inserts-updates-and-deletes.md).  
  
    3.  Use um componente de destino para aplicar as inserções ao destino. Use as transformações de Comando OLE DB com as instruções UPDATE e DELETE com parâmetros para aplicar atualizações e exclusões ao destino.  
  
         Para obter um exemplo de como usar essa transformação para aplicar atualizações e exclusões, consulte [Aplicar as alterações ao destino](apply-the-changes-to-the-destination.md).  
  
## <a name="loading-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>Carregando diversas tabelas usando diversas tarefas de Fluxo de Dados em um único pacote  
 Como alternativa, é possível usar um único pacote que contém uma tarefa de Fluxo de Dados separado para cada tabela de origem que será carregada.  
  
#### <a name="to-load-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>Para carregar diversas tabelas usando diversas tarefas de Fluxo de Dados em um único pacote  
  
1.  Crie um único pacote.  
  
2.  No fluxo de controle, use uma Tarefa Executar SQL ou expressões do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para calcular os pontos de extremidade.  
  
     Para obter um exemplo de como calcular os pontos de extremidade, consulte [Especificar um intervalo de dados de alteração](specify-an-interval-of-change-data.md).  
  
3.  Se necessário, use um contêiner Loop For para atrasar a execução até que os dados de alteração para o intervalo selecionado estejam prontos.  
  
     Para obter um exemplo de um contêiner Loop For desse tipo, consulte [Determinar se os dados de alteração estão prontos](determine-whether-the-change-data-is-ready.md).  
  
4.  Use uma tarefa Script ou Executar SQL para montar a instrução SQL que será usada para consultar a existência de alterações.  
  
     Para obter um exemplo de como montar a consulta, consulte [Preparar para consultar os dados de alteração](prepare-to-query-for-the-change-data.md).  
  
5.  Use diversas tarefas de Fluxo de Dados para carregar os dados de alteração de cada tabela de origem e aplicá-los no destino. Configure cada tarefa de Fluxo de Dados conforme descrito nas seguintes etapas.  
  
    1.  Em cada fluxo de dados, use um componente de origem para consultar as tabelas de alterações para as alterações que caem dentro dos pontos de extremidade selecionados.  
  
         Para obter um exemplo de como consultar as tabelas de alteração, consulte [Recuperar e compreender os dados de alteração](retrieve-and-understand-the-change-data.md).  
  
    2.  Use uma transformação de Divisão Condicional para direcionar as inserções, atualizações e exclusões para saídas diferentes para o processamento apropriado.  
  
         Para obter um exemplo de como configurar essa transformação para direcionar a saída, consulte [Processar inserções, atualizações e exclusões](process-inserts-updates-and-deletes.md).  
  
    3.  Use um componente de destino para aplicar as inserções ao destino. Use as transformações de Comando OLE DB com as instruções UPDATE e DELETE com parâmetros para aplicar atualizações e exclusões ao destino.  
  
         Para obter um exemplo de como usar essa transformação para aplicar atualizações e exclusões, consulte [Aplicar as alterações ao destino](apply-the-changes-to-the-destination.md).  
  
  
