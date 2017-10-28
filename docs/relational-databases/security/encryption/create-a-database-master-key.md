---
title: Criar uma chave mestra do banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e2ea4a853ecc29a2173b9a471cb380fb77ce39c0
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="create-a-database-master-key"></a>Criar uma chave mestra de banco de dados
  Este tópico descreve como criar uma chave mestra de banco de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   [Para criar uma chave mestra do banco de dados usando o Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-create-a-database-master-key"></a>Criar uma chave mestra de banco de dados  
  
1.  Escolha uma senha por criptografar a cópia da chave mestra que será armazenada no banco de dados.  
  
2.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
3.  Na barra Padrão, clique em **Nova Consulta**.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates a database master key for the "AdventureWorks2012" database.   
    -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."  
    USE AdventureWorks2012;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md).  
  
  

