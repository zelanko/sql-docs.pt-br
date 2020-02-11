---
title: Criando uma tabela usando um tipo de dados hierarchyid | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 0d1f361f-336c-4571-99d1-f4813b2d9fc4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 98ce16a3630032001a1191b09b1b0ade13aacb73
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110114"
---
# <a name="creating-a-table-using-the-hierarchyid-data-type"></a>Criando uma tabela por meio de um tipo de dados hierarchyid
  O exemplo a seguir cria uma tabela com o nome EmployeeOrg, que inclui dados de funcionário junto com sua hierarquia de relatórios. O exemplo cria a tabela no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , mas isso é opcional. Para manter o exemplo simples, essa tabela inclui somente cinco colunas:  
  
-   OrgNode é uma coluna `hierarchyid` que armazena a relação hierárquica.  
  
-   OrgLevel é uma coluna computada, com base na coluna OrgNode, que armazena cada nível de nó na hierarquia. Ela será usada para um índice por amplitude.  
  
-   EmployeeID contém o número de identificação de funcionário comum usado para aplicativos como folha de pagamento. No desenvolvimento de um novo aplicativo, os aplicativos podem usar a coluna OrgNode e a coluna EmployeeID separada não é necessária.  
  
-   EmpName contém o nome do funcionário.  
  
-   Title contém o cargo do funcionário.  
  
### <a name="to-create-the-employeeorg-table"></a>Para criar a tabela EmployeeOrg  
  
1.  Em uma janela do Editor de Consulta, execute o código a seguir para criar a tabela `EmployeeOrg` . A especificação da coluna `OrgNode` como a chave primária com um índice clusterizado criará um índice por amplitude:  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    CREATE TABLE HumanResources.EmployeeOrg  
    (  
       OrgNode hierarchyid PRIMARY KEY CLUSTERED,  
       OrgLevel AS OrgNode.GetLevel(),  
       EmployeeID int UNIQUE NOT NULL,  
       EmpName varchar(20) NOT NULL,  
       Title varchar(20) NULL  
    ) ;  
    GO  
    ```  
  
2.  Execute o seguinte código para criar um índice composto nas colunas `OrgLevel` e `OrgNode` para oferecer suporte a pesquisas eficientes por amplitude:  
  
    ```  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
 Agora a tabela está pronta para receber dados. A próxima tarefa populará a tabela usando métodos hierárquicos.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Preenchendo uma tabela hierárquica utilizando métodos hierárquicos](lesson-2-2-populating-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
