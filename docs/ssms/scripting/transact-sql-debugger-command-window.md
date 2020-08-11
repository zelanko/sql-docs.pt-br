---
title: Janela Comando
description: Saiba como usar a janela Comando do depurador Transact-SQL para executar comandos de depuração e editar comandos no código que você está depurando.
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3e9a1e432de7b9bb0871ffc094f7d37cd1709aff
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248051"
---
# <a name="transact-sql-debugger---command-window"></a>Depurador do Transact-SQL – Janela Comando

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use a **Janela Comando** para executar comandos (como de depuração e edição) sobre o código na janela do Editor de Consultas [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está atualmente em depuração. É necessário estar no modo de depuração para usar a **Janela Comando**. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] dá suporte a muitos dos comandos que também têm suporte na janela de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Comando**. Para obter mais informações, veja [Janela Comando do Visual Studio](https://go.microsoft.com/fwlink/?LinkId=112007).  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>Lista de Tarefas

**Para acessar a Janela de Comando**

- No menu **Depurar** , clique em **Iniciar Depuração**.

**Para imprimir o valor de uma variável**

- Na **Janela Comando**, digite **Debug.Print \<VariableName>** e pressione ENTER.

**Para listar as informações sobre a thread atual**

- Na **Janela Comando**, digite **Debug.ListThread**e pressione ENTER.

**Para adicionar uma variável à janela QuickWatch.**

- Na **Janela Comando**, digite **Debug.QuickWatch \<VariableName>** e pressione ENTER.

## <a name="see-also"></a>Consulte Também

[Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)
