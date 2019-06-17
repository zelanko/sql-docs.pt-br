---
title: Ferramentas e abordagens para processamento (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- process [Analysis Services]
- processing [Analysis Services]
ms.assetid: 82347a16-4145-4655-8adf-2a300f1fdf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 66696d32b62f29df7a4a1866978d72f5d4a173ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072816"
---
# <a name="tools-and-approaches-for-processing-analysis-services"></a>Ferramentas e abordagens para processamento (Analysis Services)
  O processamento é uma operação em que o Analysis Services consulta uma fonte de dados relacional e popula objetos do Analysis Services usando esses dados.  
  
 Como administrador do sistema do Analysis Services, você pode executar e monitorar o processamento de objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando estas abordagens:  
  
-   Executar análise de impacto para entender as dependências de objeto e o escopo de operações  
  
-   Processar objetos individuais no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Processar objetos individuais ou múltiplos no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   Executar análise de impacto para analisar uma lista de objetos relacionados que terão o processamento cancelado como resultado da ação atual.  
  
-   Gerar e executar um script em uma janela de consulta XMLA do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para processar objetos individuais ou múltiplos  
  
-   Usar cmdlets do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell  
  
-   Usar fluxos de controle e tarefas em pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
-   Monitorar o processamento com o SQL Server Profiler  
  
-   Programar uma solução personalizada usando AMO. Para obter mais informações, consulte [Programming AMO OLAP Basic Objects](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects).  
  
 O processamento é uma operação altamente configurável, controlada por um conjunto de opções de processamento que determinam se o processamento cheio ou incremental ocorre no nível do objeto. Para obter mais informações sobre como processar opções e objetos, consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md) e [Processando objetos do Analysis Services](processing-analysis-services-objects.md).  
  
> [!NOTE]  
>  Este tópico descreve as ferramentas e as abordagens para processar modelos multidimensionais. Para obter mais informações sobre como processar modelos de tabela, consulte [processar banco de dados, tabela ou partição](../tabular-models/process-database-table-or-partition-analysis-services.md) e [processar dados &#40;SSAS de tabela&#41;](../process-data-ssas-tabular.md).  
  
### <a name="processing-objects-in-sql-server-management-studio"></a>Processando objetos no SQL Server Management Studio  
  
1.  Inicie o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e conecte-se ao Analysis Services.  
  
2.  Clique com o botão direito do mouse no objeto do Analysis Services a ser processado e clique em **Processar**. Você pode processar dados em qualquer um destes níveis:  
  
    -   Bancos de dados  
  
    -   Cubes  
  
    -   Grupos de medidas ou partições individuais no mesmo grupo de medidas  
  
    -   Dimensões  
  
    -   Modelos de mineração  
  
    -   Estruturas de mineração  
  
     Objetos do Analysis Services são hierárquicos. Se você escolher o banco de dados, o processamento poderá ocorrer para todos os objetos contidos no banco de dados. O real processamento depende da opção de processamento selecionada e do estado do objeto. Especificamente, se um objeto não for processado, o processamento de seu pai resultará no processamento desse objeto. Para obter mais informações sobre dependências de objeto, consulte [Processing Analysis Services Objects](processing-analysis-services-objects.md).  
  
3.  Na caixa de diálogo **Processo** , em **Opções de Processo**, use o valor padrão fornecido ou selecione outra opção na lista. Para obter mais informações sobre cada opção, consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
4.  Clique em **Análise de Impacto** para identificar e, opcionalmente, processar objetos dependentes que sejam afetados se os objetos listados na caixa de diálogo Processo forem processados.  
  
5.  Outra alternativa é clicar em **Alterar Configurações** para modificar a ordem de processamento, o comportamento do processamento relativo a tipos específicos de erros e outras configurações.  
  
6.  Clique em **OK**.  
  
     A caixa de diálogo Progresso do Processo fornece o status contínuo de cada comando. Se uma mensagem de status estiver truncada, você poderá clicar em **Exibir Detalhes** para ler a mensagem inteira.  
  
### <a name="processing-objects-in-sql-server-data-tools"></a>Processando objetos em ferramentas de dados do SQL Server  
  
1.  Inicie o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e abra um projeto que foi implantado.  
  
2.  Em Gerenciador de Soluções, no projeto implantado, expanda a pasta **Dimensões** .  
  
3.  Clique com o botão direito do mouse em uma dimensão e clique em **Processar**. Você pode clicar com o botão direito em várias dimensões para processar vários objetos de uma vez. Para obter mais informações, consulte [Processamento em lote &#40;Analysis Services&#41;](batch-processing-analysis-services.md).  
  
4.  Na caixa de diálogo **Processar Dimensão** , na coluna **Opções de Processo** na **Lista de objetos**, verifique se a opção dessa coluna é **Processar Completo**. Se essa opção não estiver selecionada, em **Opções de Processo**, clique na opção e selecione **Processar Completo** na lista suspensa.  
  
5.  Clique em **Executar**.  
  
6.  Quando o processamento terminar, clique em **Fechar**.  
  
##  <a name="bkmk_impactanalysis"></a> Executar análise de impacto para identificar as dependências de objeto e o escopo de operações  
  
1.  Antes de processar um objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], você pode analisar o efeito sobre objetos relacionados clicando em **Análise de Impacto** em uma das caixas de diálogo **Processar Objetos** .  
  
2.  Clique com o botão direito do mouse em uma dimensão, cubo, grupo de medidas ou partição para abrir uma caixa de diálogo **Processar Objetos** .  
  
3.  Clique em **Análise de Impacto**. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] examina o modelo e relata sobre o reprocessamento de requisitos para objetos que estão relacionados ao que você selecionou para processar.  
  
### <a name="processing-objects-using-xmla"></a>Processando objetos usando o XMLA  
  
1.  Inicie o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e conecte-se ao Analysis Services.  
  
2.  Clique com o botão direito do mouse no objeto a ser processado e, em seguida, clique em **Processo**.  
  
3.  Na caixa de diálogo **Processo** , selecione a opção de processo que você deseja usar. Modifique outras configurações. Execute a Análise de Impacto para identificar as alterações necessárias.  
  
4.  Clique em **Script** na tela **Processar Objetos** .  
  
     Isto gera um script XMLA e abre uma janela Consulta XMLA do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
5.  Feche a caixa de diálogo. O script contém o comando de processamento e as opções especificadas na caixa de diálogo.  
  
6.  Opcionalmente, você poderá continuar adicionando ao script se desejar processar outros objetos no mesmo lote. Para continuar, repita as etapas anteriores, adicionando o script gerado para que você tenha um único script para todas as operações de processamento. Para exibir um exemplo, consulte [Schedule SSAS Administrative Tasks with SQL Server Agent](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md).  
  
7.  Na barra de menus, clique em **Consulta**e, em seguida, clique em **Executar**.  
  
### <a name="processing-objects-using-powershell"></a>Processando objetos usando o PowerShell  
  
1.  A partir desta versão do SQL Server, você pode usar cmdlets do Analysis Services PowerShell para processar objetos. Os seguintes cmdlets podem ser executados de forma interativa ou no script:  
  
    -   [Cmdlet Invoke-ProcessCube](/sql/analysis-services/powershell/invoke-processcube-cmdlet)  
  
    -   [Cmdlet Invoke-ProcessDimension](/sql/analysis-services/powershell/invoke-processdimension-cmdlet)  
  
    -   [Cmdlet Invoke-ProcessPartition](/sql/analysis-services/powershell/invoke-processpartition-cmdlet)  
  
    -   [Cmdlet Invoke-ASCmd](/sql/analysis-services/powershell/invoke-ascmd-cmdlet), que pode ser usado para executar o script XMLA, MDX ou DMX que inclui comandos de processamento.  
  
### <a name="monitoring-object-processing-using-sql-server-profiler"></a>Monitorando o processamento de objetos usando o SQL Server Profiler  
  
1.  Conectar a uma instância do Analysis Services no SQL Server Profiler.  
  
2.  Em Seleção de Eventos, clique em **Mostrar todos os eventos** para adicionar todos os eventos à lista.  
  
3.  Escolha os seguintes eventos:  
  
    -   **Command Begin** e **Command End** para mostrar ao processar inícios e paradas  
  
    -   **Error** para capturar erros  
  
    -   **Progress Report Begin**, **Progress Report Current**e **Progress Report End** para reportar sobre o status do processo e mostrar as consultas de SQL usadas para recuperar os dados  
  
    -   **Execute MDX Script Begin** e **Execute MDX Script End** para mostrar os cálculos de cubo  
  
    -   Opcionalmente, adicione eventos de bloqueio se você estiver diagnosticando problemas de desempenho relacionados ao processamento  
  
### <a name="process-analysis-services-objects-using-integration-services"></a>Processar objetos do Analysis Services usando Integration Services  
  
1.  No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], crie um pacote que usa a Tarefa Processamento do Analysis Services para preencher os objetos automaticamente com novos dados quando você fizer atualizações regulares no banco de dados relacional de origem.  
  
2.  Na **Caixa de Ferramentas do SSIS**, clique duas vezes em **Processamento do Analysis Services** para adicioná-lo ao pacote.  
  
3.  Edite a tarefa para especificar uma conexão com o banco de dados, quais objetos processar e opção de processamento. Para obter mais informações sobre como implementar essa tarefa, consulte [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md).  
  
## <a name="see-also"></a>Consulte também  
 [Processamento de objetos de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md)  
  
  
