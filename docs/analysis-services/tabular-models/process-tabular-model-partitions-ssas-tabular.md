---
title: Processar partições de modelo de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6c498d2b-22d6-4661-bc21-2ee708336c8b
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1e4440fad2c2132cfec851c2d55779a11c141145
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="process-tabular-model-partitions"></a>Processar partições de modelo tabular 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As tarefas neste tópico descrevem como processar partições em um banco de dados modelo usando a caixa de diálogo **Processar Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="bkmk_create_new"></a> Para processar uma partição  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na tabela que tem as partições que você deseja processar e clique em **Partições**.  
  
2.  Na caixa de diálogo **Partições** , em **Partições**, clique no botão Processar.  
  
3.  Na caixa de diálogo **Processar Partições** , na caixa de listagem **Modo** , selecione um dos modos de processo a seguir:  
  
    |Modo|Description|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de um objeto de partição e realiza o processamento necessário para passar os objetos de partição não processados ou parcialmente processados para um estado completamente processado. Os dados para tabelas vazias e partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas.|  
    |**Processar Completo**|Processa um objeto de partição e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto.|  
    |**Processar Dados**|Carregue os dados em uma partição ou uma tabela sem recriar hierarquias ou relações ou recalcular colunas calculadas e medidas.|  
    |**Processar Limpeza**|Remove todos os dados de uma partição.|  
    |**Processar adição**|Atualize a partição incrementalmente com novos dados.|  
  
4.  Na coluna da caixa de seleção **Processar** , selecione as partições que você deseja processar com o modo selecionado e clique em **Ok**.  
  
## <a name="see-also"></a>Consulte também  
 [Partições de modelo de tabela](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Criar e gerenciar partições de modelos de tabela](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
