---
title: "Criar e gerenciar partições de modelo Tabular (SSAS Tabular) | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09a6acec0d1ee91c553d748a334733faff36bc08
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-manage-tabular-model-partitions"></a>Criar e Gerenciar partições de modelos tabulares

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As partições definidas para um modelo durante a criação de modelo são duplicadas em um modelo implantado. Uma vez implantado, você pode gerenciar essas partições usando a caixa de diálogo **Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou usando um script. As tarefas fornecidas neste tópico descrevem como criar e gerenciar partições para um modelo implantado.  
  
  > [!NOTE]  
>  Partições em modelos de tabela criados no nível de compatibilidade de 1400 são definidas usando uma instrução de consulta M. Para obter mais informações, consulte [M referência](https://msdn.microsoft.com/library/mt211003.aspx). 
>
  
## <a name="tasks"></a>Tarefas  
 Para criar e gerenciar partições para um banco de dados modelo tabular implantado, você usará a caixa de diálogo **Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para exibir a caixa de diálogo **Gerenciador de Partições** , no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse em uma tabela e clique em **Partições**.  
  
###  <a name="bkmk_create_new"></a> Para criar uma nova partição  
  
1.  Na caixa de diálogo **Partições** , clique no botão **Novo** .  
  
2.  Em **Nome da Partição**, digite um nome para a partição. Por padrão, o nome da partição padrão será numerado incrementalmente para cada nova partição.  
  
3.  Em **instrução de consulta**, digite ou cole uma instrução de consulta SQL ou M que define as colunas e as cláusulas que você deseja incluir na partição na janela de consulta.  
  
4.  Para validar a instrução, clique em **Verificar Sintaxe**.  
  
###  <a name="bkmk_copy"></a> Para copiar uma partição  
  
1.  Na caixa de diálogo **Partições** , na lista **Partições** , selecione a partição que você deseja copiar e clique em **Copiar** .  
  
2.  Em **Nome da Partição**, digite um novo nome para a partição.  
  
3.  Em **instrução de consulta**, edite a instrução de consulta.  
  
###  <a name="bkmk_merge"></a> Para mesclar duas ou mais partições  
  
-   Na caixa de diálogo **Partições** , na lista **Partições** , use Ctrl+click para selecionar as partições que você deseja mesclar e clique em **Mesclar** .  
  
> [!IMPORTANT]  
>  Mesclar partições não atualiza os metadados da partição. Você deve editar a instrução SQL ou M para a partição resultante garantir que as operações de processamento processem todos os dados na partição mesclada.  
  
###  <a name="bkmk_delete"></a> Para excluir uma partição  
  
-   Na caixa de diálogo **Partições** , na lista **Partições** , selecione a partição que você deseja excluir e clique em **Excluir** .  
  
## <a name="see-also"></a>Consulte também  
 [Partições de modelo de tabela](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Processar partições de modelo de tabela](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  

