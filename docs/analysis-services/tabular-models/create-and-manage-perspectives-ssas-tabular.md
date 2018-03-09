---
title: Criar e gerenciar perspectivas | Microsoft Docs
ms.custom: 
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.perspectivedb.f1
ms.assetid: 2a411c2b-2820-4086-ad7f-ce6a941fefc7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5149052156082507c6c970512ab7db0194209ab5
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="create-and-manage-perspectives"></a>Criar e gerenciar perspectivas 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
As perspectivas definem subconjuntos visíveis de um modelo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo. As tarefas neste tópico descrevem como criar e gerenciar perspectivas usando a caixa de diálogo **Perspectivas** no designer modelo.  
  
## <a name="tasks"></a>Tarefas  
 Para criar perspectivas, você usará a caixa de diálogo **Criar e Gerenciar Perspectivas** , onde você pode adicionar, editar, excluir, copiar e exibir perspectivas. Para exibir a caixa de diálogo **Perspectivas** , no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e clique em **Perspectivas**.  
  
###  <a name="bkmk_add"></a> Para adicionar uma perspectiva  
  
-   Para adicionar uma nova perspectiva, clique em **Nova Perspectiva**. É possível marcar e desmarcar os objetos de campo a serem incluídos e fornecer um nome à nova perspectiva.  
  
     Se você criar uma perspectiva vazia com todos os campos de objeto, um usuário que usa essa perspectiva verá uma Lista de Campos vazia. Perspectivas devem conter pelo menos uma tabela e coluna.  
  
###  <a name="bkmk_edit"></a> Para editar uma perspectiva  
  
-   Para modificar uma perspectiva, marque e desmarque os campos na coluna da perspectiva, o que adiciona e remove objetos de campo da perspectiva.  
  
###  <a name="bkmk_rename"></a> Para renomear uma perspectiva  
  
-   Quando você focaliza um cabeçalho da coluna da perspectiva (o nome da perspectiva), o botão **Renomear** é exibido. Para renomear a perspectiva, clique em **Renomear**e insira um novo nome ou edite o nome existente.  
  
###  <a name="bkmk_delete"></a> Para excluir uma perspectiva  
  
-   Quando você focaliza um cabeçalho da coluna da perspectiva (o nome da perspectiva), o botão **Excluir** é exibido. Para excluir a perspectiva, clique no botão **Excluir** e clique em **Sim** na janela de confirmação.  
  
###  <a name="bkmk_copy"></a> Para copiar uma perspectiva  
  
-   Quando você focaliza um cabeçalho de coluna da perspectiva, o botão **Copiar** é exibido. Para criar uma cópia dessa perspectiva, clique no botão **Copiar** . Uma cópia da perspectiva selecionada é adicionada como uma nova perspectiva à direita das perspectivas existentes. A nova perspectiva herda o nome da perspectiva copiada e uma anotação *- Copiar* é acrescentada ao final do nome. Por exemplo, se uma cópia da perspectiva *Vendas* for criada, a nova perspectiva será chamada *Vendas – Cópia*.  
  
## <a name="see-also"></a>Consulte também  
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Hierarquias](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
