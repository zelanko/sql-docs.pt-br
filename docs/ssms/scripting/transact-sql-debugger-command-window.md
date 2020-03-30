---
title: Janela Comando
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
ms.openlocfilehash: 226acc4696b5edacde3b6950c10c8b5370e29b42
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75243425"
---
# <a name="transact-sql-debugger---command-window"></a>Depurador do Transact-SQL – Janela Comando

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use a **Janela Comando** para executar comandos como de depuração e edição na janela do Editor de Consultas do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está atualmente em depuração. É necessário estar no modo de depuração para usar a **Janela Comando**. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] dá suporte a muitos dos comandos que também têm suporte na janela de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Comando**. Para obter mais informações, veja [Janela Comando do Visual Studio](https://go.microsoft.com/fwlink/?LinkId=112007).  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>Lista de Tarefas

**Para acessar a Janela de Comando**

- No menu **Depurar** , clique em **Iniciar Depuração**.

**Para imprimir o valor de uma variável**

- No **CommandWindow**, digite **Debug.Print \<VariableName>** e pressione ENTER.

**Para listar as informações sobre a thread atual**

- Na **Janela Comando**, digite **Debug.ListThread**e pressione ENTER.

**Para adicionar uma variável à janela QuickWatch.**

- Na **CommandWindow**, digite **Debug.QuickWatch \<VariableName>** e pressione ENTER.

## <a name="see-also"></a>Consulte Também

[Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)
