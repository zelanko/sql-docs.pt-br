---
title: Filtrar o cubo de origem para uma estrutura de mineração | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ed1ff70d4bb0f0ebd20da468c91f2603318ec217
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116479"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>Filtrar o cubo de origem para uma estrutura de mineração
  Quando você cria uma estrutura de mineração com base nos dados em um modelo multidimensional (um cubo OLAP), você pode *fatia* a estrutura de mineração com base no cubo. A divisão permite criar subconjuntos de dados, como um tipo de filtro nos dados que são usados para treinar o modelo de mineração.  
  
### <a name="to-slice-a-cube"></a>Para fatiar um cubo  
  
1.  No Designer de mineração de dados do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], selecione o **estrutura de mineração** guia ou **modelos de mineração** guia.  
  
2.  Sobre o **modelo de mineração** menu, selecione **definir fatia do cubo da estrutura de mineração**.  
  
     O **fatiar cubo** caixa de diálogo é aberta.  
  
3.  No **dimensão** coluna o **fatiar cubo** caixa de diálogo, selecione a dimensão que você deseja filtrar.  
  
4.  Selecione um nível de uma hierarquia, usando a lista no **hierarquia** coluna.  
  
5.  Selecione um operador na lista do **operador** coluna, para usar na criação da condição de filtro.  
  
6.  Clique na caixa de **filtro** coluna.  
  
     A caixa de diálogo que é aberta contém todos os membros no nível especificado da hierarquia.  
  
7.  Selecione o membro ou membros aos quais você pretende aplicar o filtro.  
  
8.  Clique em **Okey** na caixa de diálogo de membro.  
  
9. Clique em **Okey** no **fatiar cubo** caixa de diálogo.  
  
     O cubo de origem agora é filtrado do modo definido pela fatia de cubo.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas de estrutura de mineração e instruções](data-mining/mining-structure-tasks-and-how-tos.md)   
 [Criar uma nova estrutura de mineração OLAP](data-mining/create-a-new-olap-mining-structure.md)  
  
  