---
title: Processamento em lotes (Analysis Services) | Microsoft Docs
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
helpviewer_keywords: batches [Analysis Services]
ms.assetid: ba4dcf72-0667-41d0-816b-ab8ff9a7d9cb
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d9ed1a3c1c832a1ceb34d96f0df44030da2e33cf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="batch-processing-analysis-services"></a>Processamento em lotes (Analysis Services)
  No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode usar o comando Batch para enviar vários comandos de processamento para o servidor em uma única solicitação. O processamento em lotes dá a você uma maneira de controlar quais objetos serão processados e em qual ordem. Além disso, o processamento em lotes pode ser executado como uma série de trabalhos autônomos ou uma transação na qual a falha de um processo causa uma reversão do lote completo.  
  
 O processamento em lotes maximiza a disponibilidade de dados consolidando e reduzindo a quantidade de tempo gasto para confirmar alterações. Ao processar uma dimensão completamente, qualquer partição que usa aquela dimensão é marcada como não processada. Como resultado, os cubos que contêm as partições não processadas ficam indisponíveis para navegar. Para resolver isso, use um trabalho de processamento em lotes e processe as dimensões junto com as partições afetadas. A execução do trabalho de processamento em lotes como uma transação assegura que todos os objetos incluídos na transação permaneçam disponíveis para consulta até a conclusão do processamento. Como a transação confirma as alterações, são colocados bloqueios nos objetos afetados, tornando-os temporariamente indisponíveis, mas, em geral, a quantidade de tempo usada para confirmar as alterações é menor que se você tivesse processado os objetos individualmente.  
  
 Os procedimentos neste tópico mostram as etapas para processar dimensões e partições completamente. O processamento em lote também pode incluir outras opções de processamento, como o processamento incremental. Para esses procedimentos funcionarem corretamente, você deve usar um banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém pelo menos duas dimensões e uma partição.  
  
 Este tópico inclui as seguintes seções:  
  
 [Processamento em lotes em Ferramentas de Dados do SQL Server](#bkmk_ssdt)  
  
 [Processamento em lotes usando XMLA no Management Studio](#bkmk_xmla)  
  
##  <a name="bkmk_ssdt"></a> Processamento em lotes em Ferramentas de Dados do SQL Server  
 Antes que os objetos possam ser processados no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], o projeto que contém os objetos deve ser implantado. Para obter mais informações, consulte [Implantar projetos do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md).  
  
1.  Abra o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
2.  Abra um projeto que foi implantado.  
  
3.  Em Gerenciador de Soluções, no projeto implantado, expanda a pasta **Dimensões** .  
  
4.  Com a tecla Ctrl pressionada, clique em cada dimensão listada na pasta **Dimensões** .  
  
5.  Clique com o botão direito do mouse nas dimensões selecionadas e escolha **Processar**.  
  
6.  Com a tecla Ctrl pressionada, clique em cada dimensão listada na **Lista de objetos**.  
  
7.  Clique com o botão direito do mouse nas dimensões selecionadas e escolha **Processar Completo**.  
  
8.  Para personalizar o trabalho de processo em lote, clique em **Alterar Configurações**.  
  
9. Em **Opções de processamento**, marque as seguintes configurações:  
  
    -   **Ordem de processamento** é definido como **Sequencial**e **Modo de transação** é definido como **Uma Transação**.  
  
    -   **Opção da Tabela de Write-back** é definida como **Usar existente**.  
  
    -   Em **Objetos Afetados**, marque a caixa de seleção **Objetos afetados pelo processo** .  
  
10. Clique na guia **Erros de chave de dimensão** . Verifique se **Usar configuração de erro padrão** está selecionado.  
  
11. Clique em **OK** para fechar a tela **Alterar Configurações** .  
  
12. Clique em **Executar** na tela **Processar Objetos** para iniciar o trabalho de processamento.  
  
13. Quando a caixa **Status** mostrar **Processo com êxito**, clique em **Fechar**.  
  
14. Clique em **Fechar** na tela **Processar Objetos** .  
  
##  <a name="bkmk_xmla"></a> Processamento em lotes usando XMLA no Management Studio  
 Você pode criar um script XMLA que executa processamento em lotes. Inicie gerando um script XMLA no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para cada objeto e, em seguida, combine-os em uma única Consulta de XMLA que você executa interativamente ou dentro de uma tarefa agendada.  
  
 Para obter instruções passo a passo, consulte **Exemplo 2** em [Agendar tarefas administrativas do SSAS com o SQL Server Agent](../../analysis-services/instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)  
  
## <a name="see-also"></a>Consulte também  
 [Processando um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
