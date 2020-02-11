---
title: Filtrar o cubo de origem para uma estrutura de mineração | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74220f2385e27484c5cc511c84be5625290a28db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081146"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>Filtrar o cubo de origem para uma estrutura de mineração
  Ao criar uma estrutura de mineração baseada em dados em um modelo multidimensional (um cubo OLAP), você pode *dividir* o cubo no qual a estrutura de mineração se baseia. A divisão permite criar subconjuntos de dados, como um tipo de filtro nos dados que são usados para treinar o modelo de mineração.  
  
### <a name="to-slice-a-cube"></a>Para fatiar um cubo  
  
1.  No designer de mineração de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]dados no, selecione a guia **estrutura de mineração** ou a guia **modelos de mineração** .  
  
2.  No menu **modelo de mineração** , selecione **definir fatia de cubo de estrutura de mineração**.  
  
     A caixa de diálogo **cubo de fatia** é aberta.  
  
3.  Na coluna **dimensão** da caixa de diálogo **cubo de fatia** , selecione a dimensão que você deseja filtrar.  
  
4.  Selecione um nível de hierarquia, usando a lista na coluna **hierarquia** .  
  
5.  Selecione um operador da lista na coluna **operador** para usar na criação da condição de filtro.  
  
6.  Clique na caixa na coluna **filtro** .  
  
     A caixa de diálogo que é aberta contém todos os membros no nível especificado da hierarquia.  
  
7.  Selecione o membro ou membros aos quais você pretende aplicar o filtro.  
  
8.  Clique em **OK** na caixa de diálogo membro.  
  
9. Clique em **OK** na caixa de diálogo **cubo de fatia** .  
  
     O cubo de origem agora é filtrado do modo definido pela fatia de cubo.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções da estrutura de mineração](data-mining/mining-structure-tasks-and-how-tos.md)   
 [Criar uma nova estrutura de mineração OLAP](data-mining/create-a-new-olap-mining-structure.md)  
  
  
