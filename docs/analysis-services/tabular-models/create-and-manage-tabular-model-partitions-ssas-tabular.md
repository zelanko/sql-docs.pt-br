---
title: Criar e gerenciar partições de modelo Tabular | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9a23d2753f6fe1d94fcccab648766c3471581906
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263387"
---
# <a name="create-and-manage-tabular-model-partitions"></a>Criar e gerenciar partições de modelo de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As partições definidas para um modelo durante a criação de modelo são duplicadas em um modelo implantado. Uma vez implantado, você pode gerenciar essas partições usando a caixa de diálogo **Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou usando um script. As tarefas fornecidas neste tópico descrevem como criar e gerenciar partições para um modelo implantado.  
  
  > [!NOTE]  
>  Partições em modelos de tabela criados no nível de compatibilidade 1400 são definidas usando uma instrução de consulta M. Para obter mais informações, consulte [M referência](/powerquery-m/power-query-m-reference). 
>
  
## <a name="tasks"></a>Tarefas  
 Para criar e gerenciar partições para um banco de dados modelo tabular implantado, você usará a caixa de diálogo **Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para exibir a caixa de diálogo **Gerenciador de Partições** , no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse em uma tabela e clique em **Partições**.  
  
###  <a name="bkmk_create_new"></a> Para criar uma nova partição  
  
1.  Na caixa de diálogo **Partições** , clique no botão **Novo** .  
  
2.  Em **Nome da Partição**, digite um nome para a partição. Por padrão, o nome da partição padrão será numerado incrementalmente para cada nova partição.  
  
3.  Na **instrução de consulta**, digite ou cole uma instrução de consulta SQL ou M que define as colunas e as cláusulas que você deseja incluir na partição na janela de consulta.  
  
4.  Para validar a instrução, clique em **Verificar Sintaxe**.  
  
###  <a name="bkmk_copy"></a> Para copiar uma partição  
  
1.  Na caixa de diálogo **Partições** , na lista **Partições** , selecione a partição que você deseja copiar e clique em **Copiar** .  
  
2.  Em **Nome da Partição**, digite um novo nome para a partição.  
  
3.  Na **instrução de consulta**, edite a instrução de consulta.  
  
###  <a name="bkmk_merge"></a> Para mesclar duas ou mais partições  
  
-   Na caixa de diálogo **Partições** , na lista **Partições** , use Ctrl+click para selecionar as partições que você deseja mesclar e clique em **Mesclar** .  
  
> [!IMPORTANT]  
>  Mesclar partições não atualiza os metadados da partição. Você deve editar a instrução SQL ou M para a partição resultante garantir que as operações de processamento processem todos os dados na partição mesclada.  
  
###  <a name="bkmk_delete"></a> Para excluir uma partição  
  
-   Na caixa de diálogo **Partições** , na lista **Partições** , selecione a partição que você deseja excluir e clique em **Excluir** .  
  
## <a name="see-also"></a>Confira também  
 [Partições de modelo de tabela](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Partições de modelo tabular de processo](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  
