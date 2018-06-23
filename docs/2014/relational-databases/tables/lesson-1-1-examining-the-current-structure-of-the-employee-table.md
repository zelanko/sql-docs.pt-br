---
title: Examinando a estrutura atual da tabela Employee | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c99b17d6c3b88f7dacdc99437ece36f0d242166f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010163"
---
# <a name="examining-the-current-structure-of-the-employee-table"></a>Examinando a estrutura atual da tabela Employee
  O banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] contém uma tabela **Employee** no esquema **HumanResources** . Para evitar alterar a tabela original, este passo cria uma cópia da tabela **Employee** nomeada **EmployeeDemo**. Para simplificar o exemplo, você copia só cinco colunas da tabela original. Em seguida, você consulta o **Employeedemo** para revisar como os dados são estruturados em uma tabela sem usar o `hierarchyid` tipo de dados.  
  
### <a name="to-copy-the-employee-table"></a>Para copiar a tabela Employee  
  
1.  Em uma janela Editor de Consultas, execute o código seguinte para copiar a estrutura de tabela e dados da tabela **Employee** em uma tabela nova nomeada **EmployeeDemo**.  
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT EmployeeID, LoginID, ManagerID, Title, HireDate   
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee ;  
    GO  
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>Para examinar a estrutura e dados da tabela EmployeeDemo  
  
-   Esta nova tabela **EmployeeDemo** representa uma tabela típica em um banco de dados existente que você pode querer migrar para uma nova estrutura. Em uma janela de Editor de Consultas, execute o código seguinte para mostrar como a tabela usa uma autojunção para exibir as relações de funcionário/gerente:  
  
    ```  
    SELECT   
         Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
         Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.Title  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  Title  
    NULL NULL                      109 adventure-works\ken0     Chief Executive Officer  
    3    adventure-works\roberto0  4   adventure-works\rob0     Senior Tool Designer  
    3    adventure-works\roberto0  9   adventure-works\gail0    Design Engineer  
    3    adventure-works\roberto0  11  adventure-works\jossef0  Design Engineer  
    3    adventure-works\roberto0  158 adventure-works\dylan0   Research and Development Manager  
    3    adventure-works\roberto0  263 adventure-works\ovidiu0  Senior Tool Designer  
    3    adventure-works\roberto0  267 adventure-works\michael8 Senior Design Engineer  
    3    adventure-works\roberto0  270 adventure-works\sharon0  Design Engineer  
    6    adventure-works\david0    2   adventure-works\kevin0   Marketing Assistant  
    ...  
    ```  
  
     Os resultados continuam por um total de 290 linhas.  
  
 Observe que a cláusula `ORDER BY` fez com que a saída listasse os relatórios diretos de cada nível de administração junto. Por exemplo, todos os sete relatórios diretos de **MgrID** 3 (roberto0) são listados adjacentes um ao outro. Embora não seja impossível, é muito mais difícil de agrupar todos aqueles que eventualmente se reportem ao **MgrID** 3.  
  
 Na próxima tarefa, nós criaremos uma nova tabela com um tipo de dados `hierarchyid` e moveremos os dados para a nova tabela.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Populando uma tabela com dados hierárquicos existentes](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  