---
title: Criar e gerenciar perspectivas em modelos de tabela do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 962b6b90de6d95107d1a4cdd3484a44205afb630
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162980"
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
  
-   Quando você focaliza o cabeçalho da coluna da perspectiva (o nome da perspectiva), o **Renomear** botão é exibido. Para renomear a perspectiva, clique em **Renomear**e insira um novo nome ou edite o nome existente.  
  
###  <a name="bkmk_delete"></a> Para excluir uma perspectiva  
  
-   Quando você focaliza o cabeçalho da coluna da perspectiva (o nome da perspectiva), o **excluir** botão é exibido. Para excluir a perspectiva, clique no botão **Excluir** e clique em **Sim** na janela de confirmação.  
  
###  <a name="bkmk_copy"></a> Para copiar uma perspectiva  
  
-   Quando você focaliza o cabeçalho de coluna da perspectiva, o **cópia** botão é exibido. Para criar uma cópia dessa perspectiva, clique no botão **Copiar** . Uma cópia da perspectiva selecionada é adicionada como uma nova perspectiva à direita das perspectivas existentes. A nova perspectiva herda o nome da perspectiva copiada e uma anotação *- Copiar* é acrescentada ao final do nome. Por exemplo, se uma cópia do *Sales* perspectiva é criada, a nova perspectiva será chamada *vendas – cópia*.  
  
## <a name="see-also"></a>Confira também  
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Hierarquias](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
