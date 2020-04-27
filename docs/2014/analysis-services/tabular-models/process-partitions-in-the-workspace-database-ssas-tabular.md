---
title: Processar partições no banco de dados de espaço de trabalho (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 3a369705-43fa-4961-9045-32e06fbdde33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15b9f9203075734dd84d7b601574f66bc401e700
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66066794"
---
# <a name="process-partitions-in-the-workspace-database-ssas-tabular"></a>Processar partições no banco de dados de espaço de trabalho (SSAS tabular)
  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As tarefas neste tópico descrevem como processar partições no banco de dados de workspace modelo usando a caixa de diálogo **Processar Partições** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Depois que um modelo for implantado em outra instância do Analysis Services, os administradores de banco de dados podem criar e gerenciar partições no modelo (implantado) usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], por script ou usando um pacote IS. Para obter mais informações, consulte [Criar e gerenciar partições de modelos tabulares &#40;SSAS tabular&#41;](partitions-ssas-tabular.md).  
  
###  <a name="to-process-a-partition"></a><a name="bkmk_create_new"></a> Para processar uma partição  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** , em **Processar** (Atualizar) e em **Processar Partições**.  
  
2.  Na caixa de listagem **Modo** , selecione um dos seguintes modos de processo:  
  
    |Mode|Descrição|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de um objeto de partição e realiza o processamento necessário para passar os objetos de partição não processados ou parcialmente processados para um estado completamente processado. Os dados para tabelas vazias e partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas.|  
    |**Processar Completo**|Processa um objeto de partição e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto.|  
    |**Processar dados**|Carregue os dados em uma partição ou uma tabela sem recriar hierarquias ou relações ou recalcular colunas calculadas e medidas.|  
    |**Processar Limpeza**|Remove todos os dados de uma partição.|  
    |**Processar adição**|Atualize a partição incrementalmente com novos dados.|  
  
3.  Na coluna da caixa de seleção **Processar** , selecione as partições que você deseja processar com o modo selecionado e clique em **Ok**.  
  
## <a name="see-also"></a>Consulte Também  
 [Partições &#40;SSAS de tabela&#41;](partitions-ssas-tabular.md)   
 [Criar e gerenciar partições no banco de dados de workspace &#40;SSAS de Tabela&#41;](workspace-database-ssas-tabular.md)  
  
  
