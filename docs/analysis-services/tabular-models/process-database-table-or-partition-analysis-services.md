---
title: Processar banco de dados, tabela ou partição (Analysis Services) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7ae87c71ed58cf557dbf6c1b8bf0627127ea72ff
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="process-database-table-or-partition-analysis-services"></a>Processar banco de dados, tabela ou partição (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  As tarefas neste tópico descrevem como processar um banco de dados de modelo de tabela, tabela ou partições manualmente usando o **processo \<objeto >** da caixa de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Para obter mais informações sobre o processamento do modelo de tabela, consulte [processar dados](../../analysis-services/tabular-models/process-data-ssas-tabular.md).  
  
##  <a name="bkmk_process_tasks"></a> Tarefas  
  
###  <a name="bkmk_process_db"></a> Para processar um banco de dados  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no banco de dados que deseja processar e clique em **Processar Banco de Dados**.  
  
2.  Na caixa de diálogo **Processar Banco de Dados** , na caixa de listagem **Modo** , selecione um dos modos de processamento a seguir:  
  
    |Modo|Description|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de objetos de banco de dados e realiza o processamento necessário para passar os objetos não processados ou parcialmente processados para um estado completamente processado. Os dados das tabelas vazias e das partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas (recalculadas).|  
    |**Processar Completo**|Processa um banco de dados e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto. Esta opção requer a maioria dos recursos.|  
    |**Processar Limpeza**|Remove todos os dados dos objetos de banco de dados.|  
    |**Processar Recálculo**|Atualiza e recalcula hierarquias, relações e colunas calculadas.|  
  
3.  Na coluna da caixa de seleção **Processar** , selecione as partições que você deseja processar com o modo selecionado e clique em **Ok**.  
  
###  <a name="bkmk_process_table"></a> Para processar uma tabela  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no modelo de banco de dados de tabela que contém a tabela a ser processada, expanda o nó **Tabelas** , clique com o botão direito do mouse na tabela a ser processada e clique em **Processar Tabela**.  
  
2.  Na caixa de diálogo **Processar Tabela** , na caixa de listagem **Modo** , selecione um dos modos de processamento a seguir:  
  
    |Modo|Description|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de um objeto de tabela e realiza o processamento necessário para passar os objetos não processados ou parcialmente processados para um estado completamente processado. Os dados das tabelas vazias e das partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas (recalculadas).|  
    |**Processar Completo**|Processa um objeto de tabela e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto. Esta opção requer a maioria dos recursos.|  
    |**Processar Dados**|Carregue os dados em uma tabela sem recriar hierarquias ou relações, ou recalcular medidas e colunas calculadas.|  
    |**Processar Limpeza**|Remove todos os dados de uma tabela e de qualquer partição de tabela.|  
    |**Processar Desfragmentação**|Desfragmenta os índices de tabela auxiliares.|  
  
3.  Na coluna da caixa de seleção da tabela, verifique a tabela; se desejar, selecione qualquer outra tabela que deseje processar e clique em **Ok**.  
  
###  <a name="bkmk_process_partition"></a> Para processar uma ou mais partições  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na tabela que tem as partições que você deseja processar e clique em **Partições**.  
  
2.  Na caixa de diálogo **Partições** , em **Partições**, clique no botão Processar.  
  
3.  Na caixa de diálogo **Processar Partição** , na caixa de listagem **Modo** , selecione um dos modos de processamento a seguir:  
  
    |Modo|Description|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de um objeto de partição e realiza o processamento necessário para passar os objetos de partição não processados ou parcialmente processados para um estado completamente processado. Os dados das tabelas vazias e das partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas (recalculadas).|  
    |**Processar Completo**|Processa um objeto de partição e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto.|  
    |**Processar Dados**|Carregue os dados em uma partição ou uma tabela sem recriar hierarquias ou relações ou recalcular colunas calculadas e medidas.|  
    |**Processar Limpeza**|Remove todos os dados de uma partição.|  
    |**Processar adição**|Atualize a partição incrementalmente com novos dados.|  
  
4.  Na coluna da caixa de seleção **Processar** , selecione as partições que você deseja processar com o modo selecionado e clique em **Ok**.  
  
## <a name="see-also"></a>Consulte também  
 [Partições de modelo de tabela](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Criar e gerenciar partições de modelos de tabela](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
