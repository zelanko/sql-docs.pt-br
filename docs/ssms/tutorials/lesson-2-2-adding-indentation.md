---
title: Adicionando recuo | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 9dce05c1-c52f-455d-8b8d-6f303e242760
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5559f970627449d56863f4c9d933d5e6636f0bd2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="lesson-2-2---adding-indentation"></a>Lição 2-2 – Adicionando recuo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] O Editor de Consultas permite o recuo de grandes seções de código em uma única etapa, além de também possibilitar a alteração da quantidade de recuo.  
  
## <a name="indenting-code"></a>Recuando código  
  
#### <a name="to-indent-multiple-lines-of-code"></a>Para recuar várias linhas de código  
  
1.  Na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Crie uma segunda consulta que seleciona as colunas **BusinessEntityID**, FirstName, **MiddleName**e **LastName** da tabela **Person** do esquema **Person** . Coloque cada coluna em uma linha separada de forma que o código se pareça com o exemplo a seguir:  
  
    ```  
    -- Search for a contact  
    SELECT   
    BusinessEntityID,  
    FirstName,   
    MiddleName,   
    LastName  
    FROM Person.Person  
    WHERE LastName = 'Sanchez';  
    GO  
    ```  
  
3.  Selecione todo o texto de `BusinessEntityID` para `LastName`.  
  
4.  Na barra de ferramentas do **Editor SQL** , clique em **Aumentar Recuo** para recuar todas as linhas de uma vez.  
  
#### <a name="to-change-the-default-indentation"></a>Para alterar o recuo padrão  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Expanda **Editor de Texto**, expanda **Todos os Idiomas**, clique em **Guias** e defina valores de recuo conforme o necessário. Note que você pode alterar o tamanho do recuo assim como o tamanho das guias e se as guias serão convertidas em espaços.  
  
    ![Aparência da caixa de diálogo Guias](./media/lesson-2-2-adding-indentation/tabsdialog.gif "Aparência da caixa de diálogo Guias")  
  
3.  Clique em **OK**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Maximizando o Editor de Consultas](../../tools/sql-server-management-studio/lesson-2-3-maximizing-query-editor.md)  
  
  
  
