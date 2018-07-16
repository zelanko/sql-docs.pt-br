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
ms.topic: conceptual
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 10ad6c295f61de1f50688bb8f52b12268756860a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226646"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>Filtrar o cubo de origem para uma estrutura de mineração
  Quando você cria uma estrutura de mineração se baseia nos dados em um modelo multidimensional (um cubo OLAP), você pode *fatia* a estrutura de mineração com base no cubo. A divisão permite criar subconjuntos de dados, como um tipo de filtro nos dados que são usados para treinar o modelo de mineração.  
  
### <a name="to-slice-a-cube"></a>Para fatiar um cubo  
  
1.  No Designer de mineração de dados do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], selecione o **estrutura de mineração** guia ou o **modelos de mineração** guia.  
  
2.  Sobre o **modelo de mineração** menu, selecione **definir fatia do cubo da estrutura de mineração**.  
  
     O **fatiar cubo** caixa de diálogo é aberta.  
  
3.  No **dimensão** coluna das **fatiar cubo** caixa de diálogo, selecione a dimensão que você deseja filtrar.  
  
4.  Selecione um nível de uma hierarquia, usando a lista na **hierarquia** coluna.  
  
5.  Selecione um operador na lista de **operador** coluna, a ser usado para criar a condição de filtro.  
  
6.  Clique na caixa de **filtro** coluna.  
  
     A caixa de diálogo que é aberta contém todos os membros no nível especificado da hierarquia.  
  
7.  Selecione o membro ou membros aos quais você pretende aplicar o filtro.  
  
8.  Clique em **Okey** na caixa de diálogo de membro.  
  
9. Clique em **Okey** na **fatiar cubo** caixa de diálogo.  
  
     O cubo de origem agora é filtrado do modo definido pela fatia de cubo.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas de estrutura de mineração e instruções](data-mining/mining-structure-tasks-and-how-tos.md)   
 [Criar uma nova estrutura de mineração OLAP](data-mining/create-a-new-olap-mining-structure.md)  
  
  
