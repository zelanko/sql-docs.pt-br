---
title: Processar banco de dados, tabela ou partição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMS.PARTITIONS.PROCESSINGOPTIONS.IMBI.F1
ms.assetid: 307d69c3-cabb-4dfa-b90c-9852492c1213
author: minewiskan
ms.author: owend
ms.openlocfilehash: 08c0856df10c2b70dc58ab1b52b0b7a4a1041e1b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938737"
---
# <a name="process-database-table-or-partition"></a>Processar banco de dados, tabela ou partição
  As tarefas neste tópico descrevem como processar um banco de dados de modelo tabular, uma tabela ou partições manualmente usando a caixa de diálogo **processar \<object> ** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 Para obter mais informações sobre o processamento de modelos de tabela, veja [Processar dados &#40;SSAS de Tabela&#41;](../process-data-ssas-tabular.md).  
  
##  <a name="tasks"></a><a name="bkmk_process_tasks"></a>Tarefa  
  
###  <a name="to-process-a-database"></a><a name="bkmk_process_db"></a>Para processar um banco de dados  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no banco de dados que deseja processar e clique em **Processar Banco de Dados**.  
  
2.  Na caixa de diálogo **Processar Banco de Dados** , na caixa de listagem **Modo** , selecione um dos modos de processamento a seguir:  
  
    |Mode|Descrição|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de objetos de banco de dados e realiza o processamento necessário para passar os objetos não processados ou parcialmente processados para um estado completamente processado. Os dados das tabelas vazias e das partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas (recalculadas).|  
    |**Processar Completo**|Processa um banco de dados e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto. Esta opção requer a maioria dos recursos.|  
    |**Processar Limpeza**|Remove todos os dados dos objetos de banco de dados.|  
    |**Processar Recálculo**|Atualiza e recalcula hierarquias, relações e colunas calculadas.|  
  
3.  Na coluna da caixa de seleção **Processar** , selecione as partições que você deseja processar com o modo selecionado e clique em **Ok**.  
  
###  <a name="to-process-a-table"></a><a name="bkmk_process_table"></a>Para processar uma tabela  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no modelo de banco de dados de tabela que contém a tabela a ser processada, expanda o nó **Tabelas** , clique com o botão direito do mouse na tabela a ser processada e clique em **Processar Tabela**.  
  
2.  Na caixa de diálogo **Processar Tabela** , na caixa de listagem **Modo** , selecione um dos modos de processamento a seguir:  
  
    |Mode|Descrição|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de um objeto de tabela e realiza o processamento necessário para passar os objetos não processados ou parcialmente processados para um estado completamente processado. Os dados das tabelas vazias e das partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas (recalculadas).|  
    |**Processar Completo**|Processa um objeto de tabela e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto. Esta opção requer a maioria dos recursos.|  
    |**Processar dados**|Carregue os dados em uma tabela sem recriar hierarquias ou relações, ou recalcular medidas e colunas calculadas.|  
    |**Processar Limpeza**|Remove todos os dados de uma tabela e de qualquer partição de tabela.|  
    |**Processar Desfragmentação**|Desfragmenta os índices de tabela auxiliares.|  
  
3.  Na coluna da caixa de seleção da tabela, verifique a tabela; se desejar, selecione qualquer outra tabela que deseje processar e clique em **Ok**.  
  
###  <a name="to-process-one-or-more-partitions"></a><a name="bkmk_process_partition"></a>Para processar uma ou mais partições  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na tabela que tem as partições que você deseja processar e clique em **Partições**.  
  
2.  Na caixa de diálogo **Partições** , em **Partições**, clique no botão Processar.  
  
3.  Na caixa de diálogo **Processar Partição** , na caixa de listagem **Modo** , selecione um dos modos de processamento a seguir:  
  
    |Mode|Descrição|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de um objeto de partição e realiza o processamento necessário para passar os objetos de partição não processados ou parcialmente processados para um estado completamente processado. Os dados das tabelas vazias e das partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas (recalculadas).|  
    |**Processar Completo**|Processa um objeto de partição e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto.|  
    |**Processar dados**|Carregue os dados em uma partição ou uma tabela sem recriar hierarquias ou relações ou recalcular colunas calculadas e medidas.|  
    |**Processar Limpeza**|Remove todos os dados de uma partição.|  
    |**Processar adição**|Atualize a partição incrementalmente com novos dados.|  
  
4.  Na coluna da caixa de seleção **Processar** , selecione as partições que você deseja processar com o modo selecionado e clique em **Ok**.  
  
## <a name="see-also"></a>Consulte Também  
 [Partições de modelo de tabela &#40;SSAS de tabela&#41;](tabular-model-partitions-ssas-tabular.md)   
 [Criar e gerenciar partições de modelos de tabela &#40;SSAS de Tabela&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
