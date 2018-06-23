---
title: Criar e gerenciar perspectivas (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.perspectivedb.f1
ms.assetid: 2a411c2b-2820-4086-ad7f-ce6a941fefc7
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3d49d87c3cd5ff2b4ae68e485cfa9cc5afe31d6f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010512"
---
# <a name="create-and-manage-perspectives-ssas-tabular"></a>Criar e Gerenciar Perspectivas (SSAS tabular)
  As perspectivas definem subconjuntos visíveis de um modelo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo. As tarefas neste tópico descrevem como criar e gerenciar perspectivas usando a caixa de diálogo **Perspectivas** no designer modelo.  
  
 Este tópico inclui as seguintes tarefas:  
  
-   [Para adicionar uma perspectiva](#bkmk_add)  
  
-   [Para editar uma perspectiva](#bkmk_edit)  
  
-   [Para renomear uma perspectiva](#bkmk_rename)  
  
-   [Para excluir uma perspectiva](#bkmk_delete)  
  
-   [Para copiar uma perspectiva](#bkmk_copy)  
  
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
 [Perspectivas &#40;Tabular do SSAS&#41;](perspectives-ssas-tabular.md)   
 [Hierarquias &#40;Tabular do SSAS&#41;](hierarchies-ssas-tabular.md)  
  
  