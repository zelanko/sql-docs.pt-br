---
title: Examinando a estrutura atual da tabela Employee | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 620defd42e27b122a92ee145da6b4b14d1cbf996
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-1---examining-the-current-structure-of-the-employee-table"></a>Lição 1-1 – Examinando a estrutura atual da tabela Employee
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
O banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] (ou posterior) de exemplo contém uma tabela **Funcionário** no esquema **HumanResources**. Para evitar alterar a tabela original, este passo cria uma cópia da tabela **Employee** nomeada **EmployeeDemo**. Para simplificar o exemplo, você copia só cinco colunas da tabela original. Então, você consulta a tabela **HumanResources.EmployeeDemo** para revisar como os dados são estruturados em uma tabela sem usar o tipo de dados **hierarchyid** .  
  
### <a name="to-copy-the-employee-table"></a>Para copiar a tabela Employee  
  
1.  Em uma janela Editor de Consultas, execute o código seguinte para copiar a estrutura de tabela e dados da tabela **Employee** em uma tabela nova nomeada **EmployeeDemo**. Como a tabela original já usa hierarchyid, essa consulta basicamente mescla a hierarquia para recuperar o gerente do funcionário. Em partes subsequentes desta lição, reconstruiremos essa hierarquia.
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
      (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
            WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
                (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID
        , emp.JobTitle, emp.HireDate
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee emp ;
    GO
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>Para examinar a estrutura e dados da tabela EmployeeDemo  
  
-   Esta nova tabela **EmployeeDemo** representa uma tabela típica em um banco de dados existente que você pode querer migrar para uma nova estrutura. Em uma janela de Editor de Consultas, execute o código seguinte para mostrar como a tabela usa uma autojunção para exibir as relações de funcionário/gerente:  
  
    ```  
    SELECT   
        Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
        Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.JobTitle  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  JobTitle  
    NULL    NULL    1   adventure-works\ken0    Chief Executive Officer
    1   adventure-works\ken0    2   adventure-works\terri0  Vice President of Engineering
    1   adventure-works\ken0    16  adventure-works\david0  Marketing Manager
    1   adventure-works\ken0    25  adventure-works\james1  Vice President of Production
    1   adventure-works\ken0    234 adventure-works\laura1  Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0   Information Services Manager
    1   adventure-works\ken0    273 adventure-works\brian3  Vice President of Sales
    2   adventure-works\terri0  3   adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0    Senior Tool Designer
    ...  
    ```  
  
    Os resultados continuam por um total de 290 linhas.  
  
Observe que a cláusula **ORDER BY** fez com que a saída listasse os relatórios diretos de cada nível de administração junto. Por exemplo, todos os sete relatórios diretos de **MgrID** 1 (ken0) estão listados adjacentes uns aos outros. Embora não seja impossível, é muito mais difícil agrupar todos aqueles que eventualmente se reportem ao **MgrID** 1.  
  
Na próxima tarefa, nós criaremos uma nova tabela com um tipo de dados **hierarchyid** e moveremos os dados para a nova tabela.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Populando uma tabela com dados hierárquicos existentes](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  
  
