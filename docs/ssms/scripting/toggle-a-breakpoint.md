---
title: Alternar um ponto de interrupção
description: Saiba como alternar um ponto de interrupção para realçar a instrução Transact-SQL associada e executar várias ações na instrução (tais como a edição).
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c477ab89-a1cd-4f2c-aa7c-40525041100f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f9b9ddfd58beed00a00c3512b5db51e7a3a7907c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036202"
---
# <a name="toggle-a-breakpoint"></a>Alternar um ponto de interrupção

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

O ato de definir um ponto de interrupção em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é chamado de alternar um ponto de interrupção.  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="breakpoints"></a>Pontos de interrupção

Quando o ponto de interrupção foi definido, ele é representado por um ícone na barra cinza à esquerda da instrução. O ícone é chamado de um glifo de ponto de interrupção. [!INCLUDE[tsql](../../includes/tsql-md.md)] são aplicados a uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] completa. Quando um ponto de interrupção é ativado, o depurador realça a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] associada.  
  
 Se houver várias instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em uma linha, você poderá alternar um ponto de interrupção para cada instrução. Clicar na barra cinza à esquerda da janela alterna um ponto de interrupção na primeira instrução na linha. Você poderá alternar um ponto de interrupção em uma instrução subsequente realçando qualquer parte da instrução, ou movendo o cursor na instrução, e pressionando F9 ou clicando em **Alternar Ponto de Interrupção** no menu **Depurar** . Se você tiver vários pontos de interrupção em uma linha, haverá somente um glifo de ponto de interrupção na barra cinza à esquerda.  
  
 Depois que um ponto de interrupção for alternado, você poderá executar várias ações no ponto de interrupção, como editar suas propriedades ou desabilitá-las temporariamente. Para obter mais informações, veja [Pontos de interrupção Transact-SQL](./transact-sql-breakpoints.md).  
  
## <a name="toggle-a-breakpoint"></a>Alternar um ponto de interrupção  
 **Para alternar um ponto de interrupção em uma instrução Transact-SQL**  
  
1.  Clique na barra cinza à esquerda da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
2.  Outra alternativa é realçar qualquer parte da instrução ou mover o cursor para a instrução, e depois executar uma das ações:  
  
    -   Pressione F9.  
  
    -   No menu **Depurar** , clique em **Alternar Ponto de Interrupção**.  
  
