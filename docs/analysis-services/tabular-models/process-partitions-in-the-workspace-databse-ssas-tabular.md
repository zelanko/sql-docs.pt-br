---
title: "Processar partições no banco de dados de espaço de trabalho (SSAS Tabular) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a369705-43fa-4961-9045-32e06fbdde33
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 650821073c8c2c15d143ba0fb2ff24e1352c9cb6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="process-partitions-in-the-workspace-databse-ssas-tabular"></a>Processar partições no banco de dados de espaço de trabalho (SSAS tabular)
  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As tarefas neste tópico descrevem como processar partições no banco de dados de espaço de trabalho modelo usando a caixa de diálogo **Processar Partições** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Depois que um modelo for implantado em outra instância do Analysis Services, os administradores de banco de dados podem criar e gerenciar partições no modelo (implantado) usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], por script ou usando um pacote IS. Para obter mais informações, consulte [Criar e gerenciar partições de modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
###  <a name="bkmk_create_new"></a> Para processar uma partição  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** , em **Processar** (Atualizar) e em **Processar Partições**.  
  
2.  Na caixa de listagem **Modo** , selecione um dos seguintes modos de processo:  
  
    |Modo|Description|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de um objeto de partição e realiza o processamento necessário para passar os objetos de partição não processados ou parcialmente processados para um estado completamente processado. Os dados para tabelas vazias e partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas.|  
    |**Processar Completo**|Processa um objeto de partição e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto.|  
    |**Processar Dados**|Carregue os dados em uma partição ou uma tabela sem recriar hierarquias ou relações ou recalcular colunas calculadas e medidas.|  
    |**Processar Limpeza**|Remove todos os dados de uma partição.|  
    |**Processar adição**|Atualize a partição incrementalmente com novos dados.|  
  
3.  Na coluna da caixa de seleção **Processar** , selecione as partições que você deseja processar com o modo selecionado e clique em **Ok**.  
  
## <a name="see-also"></a>Consulte também  
 [Partições &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [Criar e gerenciar partições no banco de dados de espaço de trabalho &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)  
  
  
