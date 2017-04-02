---
title: "Criar e Gerenciar parti&#231;&#245;es de modelos tabulares (SSAS tabular) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 8
---
# Criar e Gerenciar parti&#231;&#245;es de modelos tabulares (SSAS tabular)
  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As partições definidas para um modelo durante a criação de modelo são duplicadas em um modelo implantado. Uma vez implantado, você pode gerenciar essas partições usando a caixa de diálogo **Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou usando um script. As tarefas fornecidas neste tópico descrevem como criar e gerenciar partições para um modelo implantado.  
  
 Este tópico inclui as seguintes tarefas:  
  
-   [Para criar uma nova partição](#bkmk_create_new)  
  
-   [Para copiar uma partição](#bkmk_copy)  
  
-   [Para mesclar duas ou mais partições](#bkmk_merge)  
  
-   [Para excluir uma partição](#bkmk_delete)  
  
## Tarefas  
 Para criar e gerenciar partições para um banco de dados modelo tabular implantado, você usará a caixa de diálogo **Partições** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para exibir a caixa de diálogo **Gerenciador de Partições**, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse em uma tabela e clique em **Partições**.  
  
###  <a name="bkmk_create_new"></a> Para criar uma nova partição  
  
1.  Na caixa de diálogo **Partições** , clique no botão **Novo** .  
  
2.  Em **Nome da Partição**, digite um nome para a partição. Por padrão, o nome da partição padrão será numerado incrementalmente para cada nova partição.  
  
3.  Em **Instrução SQL**, digite ou cole uma instrução de consulta SQL que define as colunas e as cláusulas que você quer incluir na partição na janela de consulta.  
  
4.  Para validar a instrução, clique em **Verificar Sintaxe**.  
  
###  <a name="bkmk_copy"></a> Para copiar uma partição  
  
1.  Na caixa de diálogo **Partições** , na lista **Partições** , selecione a partição que você deseja copiar e clique em **Copiar** .  
  
2.  Em **Nome da Partição**, digite um novo nome para a partição.  
  
3.  Em **Instrução SQL**, edite a instrução de consulta SQL.  
  
###  <a name="bkmk_merge"></a> Para mesclar duas ou mais partições  
  
-   Na caixa de diálogo **Partições**, na lista **Partições**, use Ctrl+click para selecionar as partições que você deseja mesclar e clique em **Mesclar**.  
  
> [!IMPORTANT]  
>  Mesclar partições não atualiza os metadados da partição. Os administradores devem alterar a Instrução SQL para a partição resultante para garantir que as operações de processamento processem todos os dados na partição mesclada.  
  
###  <a name="bkmk_delete"></a> Para excluir uma partição  
  
-   Na caixa de diálogo **Partições** , na lista **Partições** , selecione a partição que você deseja excluir e clique em **Excluir** .  
  
## Consulte também  
 [Partições de modelo de tabela &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Processar partições de modelo de tabela &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  