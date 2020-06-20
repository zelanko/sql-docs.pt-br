---
title: Criar e gerenciar partições de modelo de tabela (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
author: minewiskan
ms.author: owend
ms.openlocfilehash: 27f6bda21381a3388e51c387b072c80026b44c6a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939777"
---
# <a name="create-and-manage-tabular-model-partitions-ssas-tabular"></a>Criar e Gerenciar partições de modelos tabulares (SSAS tabular)
  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As partições definidas para um modelo durante a criação de modelo são duplicadas em um modelo implantado. Uma vez implantado, você pode gerenciar essas partições usando a caixa de diálogo **Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou usando um script. As tarefas fornecidas neste tópico descrevem como criar e gerenciar partições para um modelo implantado.  
  
 Este tópico inclui as seguintes tarefas:  
  
-   [Para criar uma nova partição](#bkmk_create_new)  
  
-   [Para copiar uma partição](#bkmk_copy)  
  
-   [Para mesclar duas ou mais partições](#bkmk_merge)  
  
-   [Para excluir uma partição](#bkmk_delete)  
  
## <a name="tasks"></a>Tarefas  
 Para criar e gerenciar partições para um banco de dados modelo tabular implantado, você usará a caixa de diálogo **Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para exibir a caixa de diálogo **Gerenciador de Partições** , no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse em uma tabela e clique em **Partições**.  
  
###  <a name="to-create-a-new-partition"></a><a name="bkmk_create_new"></a>Para criar uma nova partição  
  
1.  Na caixa de diálogo **Partições** , clique no botão **Novo** .  
  
2.  Em **Nome da Partição**, digite um nome para a partição. Por padrão, o nome da partição padrão será numerado incrementalmente para cada nova partição.  
  
3.  Em **Instrução SQL**, digite ou cole uma instrução de consulta SQL que define as colunas e as cláusulas que você quer incluir na partição na janela de consulta.  
  
4.  Para validar a instrução, clique em **Verificar Sintaxe**.  
  
###  <a name="to-copy-a-partition"></a><a name="bkmk_copy"></a> Para copiar uma partição  
  
1.  Na caixa de diálogo **Partições** , na lista **Partições** , selecione a partição que você deseja copiar e clique em **Copiar** .  
  
2.  Em **Nome da Partição**, digite um novo nome para a partição.  
  
3.  Em **Instrução SQL**, edite a instrução de consulta SQL.  
  
###  <a name="to-merge-two-or-more-partitions"></a><a name="bkmk_merge"></a> Para mesclar duas ou mais partições  
  
-   Na caixa de diálogo **Partições** , na lista **Partições** , use Ctrl+click para selecionar as partições que você deseja mesclar e clique em **Mesclar** .  
  
> [!IMPORTANT]  
>  Mesclar partições não atualiza os metadados da partição. Os administradores devem alterar a Instrução SQL para a partição resultante para garantir que as operações de processamento processem todos os dados na partição mesclada.  
  
###  <a name="to-delete-a-partition"></a><a name="bkmk_delete"></a> Para excluir uma partição  
  
-   Na caixa de diálogo **Partições** , na lista **Partições** , selecione a partição que você deseja excluir e clique em **Excluir** .  
  
## <a name="see-also"></a>Consulte Também  
 [Partições de modelo de tabela &#40;SSAS de tabela&#41;](partitions-ssas-tabular.md)   
 [Processar partições de modelo de tabela &#40;SSAS de Tabela&#41;](process-tabular-model-partitions-ssas-tabular.md)  
  
  
