---
title: Alternar um ponto de interrupção | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c477ab89-a1cd-4f2c-aa7c-40525041100f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4b5024566db8fe4bd572a5ae26d4c2f44fb3ee7a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39534696"
---
# <a name="toggle-a-breakpoint"></a>Alternar um ponto de interrupção
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  O ato de definir um ponto de interrupção em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é chamado de alternar um ponto de interrupção.  
  
## <a name="breakpoints"></a>Pontos de interrupção  
 Quando o ponto de interrupção foi definido, ele é representado por um ícone na barra cinza à esquerda da instrução. O ícone é chamado de um glifo de ponto de interrupção. [!INCLUDE[tsql](../../includes/tsql-md.md)] são aplicados a uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] completa. Quando um ponto de interrupção é ativado, o depurador realça a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] associada.  
  
 Se houver várias instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em uma linha, você poderá alternar um ponto de interrupção para cada instrução. Clicar na barra cinza à esquerda da janela alterna um ponto de interrupção na primeira instrução na linha. Você poderá alternar um ponto de interrupção em uma instrução subsequente realçando qualquer parte da instrução, ou movendo o cursor na instrução, e pressionando F9 ou clicando em **Alternar Ponto de Interrupção** no menu **Depurar** . Se você tiver vários pontos de interrupção em uma linha, haverá somente um glifo de ponto de interrupção na barra cinza à esquerda.  
  
 Depois que um ponto de interrupção for alternado, você poderá executar várias ações no ponto de interrupção, como editar suas propriedades ou desabilitá-las temporariamente. Para obter mais informações, veja [Pontos de interrupção Transact-SQL](../../relational-databases/scripting/transact-sql-breakpoints.md).  
  
## <a name="toggle-a-breakpoint"></a>Alternar um ponto de interrupção  
 **Para alternar um ponto de interrupção em uma instrução Transact-SQL**  
  
1.  Clique na barra cinza à esquerda da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
2.  Outra alternativa é realçar qualquer parte da instrução ou mover o cursor para a instrução, e depois executar uma das ações:  
  
    -   Pressione F9.  
  
    -   No menu **Depurar** , clique em **Alternar Ponto de Interrupção**.  
  
  
