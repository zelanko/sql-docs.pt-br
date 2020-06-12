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
ms.openlocfilehash: 058ba6e78fd6c6e5aa7b06fbd5d34c256dac07b3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544448"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>Filtrar o cubo de origem para uma estrutura de mineração
  Ao criar uma estrutura de mineração baseada em dados em um modelo multidimensional (um cubo OLAP), você pode *dividir* o cubo no qual a estrutura de mineração se baseia. A divisão permite criar subconjuntos de dados, como um tipo de filtro nos dados que são usados para treinar o modelo de mineração.  
  
### <a name="to-slice-a-cube"></a>Para fatiar um cubo  
  
1.  No designer de mineração de dados no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] , selecione a guia **estrutura de mineração** ou a guia **modelos de mineração** .  
  
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
  
  
