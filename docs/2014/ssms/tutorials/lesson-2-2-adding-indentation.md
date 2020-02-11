---
title: Adicionando recuo | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9dce05c1-c52f-455d-8b8d-6f303e242760
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 009f61563548e0c060350a75e9627804e18a7c54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63222943"
---
# <a name="adding-indentation"></a>Adicionando recuo
  O Editor de Consultas permite o recuo de grandes seções de código em uma única etapa, além de também possibilitar a alteração da quantidade de recuo.  
  
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
  
     ![Aparência da caixa de diálogo Guias](media/tabsdialog.gif "Aparência da caixa de diálogo Guias")  
  
3.  Clique em **OK**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Maximizando o Editor de Consultas](lesson-2-3-maximizing-query-editor.md)  
  
  
