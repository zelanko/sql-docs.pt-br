---
title: Criar e gerenciar partições no banco de dados de espaço de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.partitionmgr.f1
ms.assetid: 0b3027d6-652b-4eb3-a197-58b25df65218
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3d0701ce2c1e7d7cccf999de93714daeb4799861
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-manage-partitions-in-the-workspace-database"></a>Criar e gerenciar partições no banco de dados de espaço de trabalho 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de ou em paralelo com outras partições. As partições podem melhorar a escalabilidade e a gerenciabilidade de bancos de dados grandes. Por padrão, cada tabela tem uma partição que inclui todas as colunas. As tarefas neste tópico descrevem como criar e gerenciar partições no banco de dados de espaço de trabalho modelo usando o **Gerenciador de partições** da caixa de diálogo[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
 Depois que um modelo for implantado em outra instância do Analysis Services, os administradores de banco de dados podem criar e gerenciar partições no modelo (implantado) usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [criar e gerenciar partições de modelo de tabela](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
> [!NOTE]  
>  Você não pode mesclar partições no banco de dados de espaço de trabalho modelo usando a caixa de diálogo Gerenciador de Partições. As partições só podem ser mescladas em um modelo implantado usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="tasks"></a>Tarefas  
 Para criar e gerenciar partições, você usará a caixa de diálogo **Gerenciador de Partições** . Para exibir a caixa de diálogo **Gerenciador de Partições** , no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Tabela** e clique em **Partições**.  
  
###  <a name="bkmk_create_new"></a> Para criar uma nova partição  
  
1.  No designer de modelo, selecione a tabela para a qual você deseja definir uma partição.  
  
2.  Clique no menu **Tabela** e clique em **Partições**.  
  
3.  No **Gerenciador de Partições**, na caixa de listagem **Tabela** , verifique ou selecione a tabela que você deseja particionar e clique em **Novo**.  
  
4.  Em **Nome da Partição**, digite um nome para a partição. Por padrão, o nome da partição padrão será numerado incrementalmente para cada nova partição.  
  
5.  Você pode selecionar as linhas e as colunas a serem incluídas na partição usando o modo de visualização de Tabela ou usando uma consulta SQL criada usando o modo Editor de Consultas.  
  
     Para usar o modo de visualização de Tabela (padrão), clique no botão **Visualização de Tabela** no canto superior direito da janela de visualização. Selecione as colunas que você quer incluir na partição marcando a caixa de seleção ao lado do nome da coluna. Para filtrar linhas, clique com o botão direito do mouse em um valor de célula e clique em **Filtrar por Valor da Célula Selecionada**.  
  
     Para usar uma instrução SQL, clique no botão **Editor de Consultas** no canto superior direito da janela de visualização, e digite ou cole uma instrução de consulta SQL na janela de consulta. Para validar sua instrução, clique em **Validar**. Para usar o Designer de Consulta, clique em **Design**.  
  
###  <a name="bkmk_copy"></a> Para copiar uma partição  
  
1.  No **Gerenciador de Partições**, na caixa de listagem **Tabela** , verifique ou selecione a tabela que contém a partição que você deseja copiar.  
  
2.  Na lista **Partições** , selecione a partição que você deseja copiar e clique em **Copiar**.  
  
3.  Em **Nome da Partição**, digite um novo nome para a partição.  
  
###  <a name="bkmk_delete"></a> Para excluir uma partição  
  
1.  No **Gerenciador de Partições**, na caixa de listagem **Tabela** , verifique ou selecione a tabela que contém a partição que você deseja excluir.  
  
2.  Na lista **Partições** , selecione a partição que você deseja excluir e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Partições](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [Processar partições no banco de dados de espaço de trabalho](../../analysis-services/tabular-models/process-partitions-in-the-workspace-databse-ssas-tabular.md)  
  
  
