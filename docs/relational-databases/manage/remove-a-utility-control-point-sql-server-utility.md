---
title: "Remover um ponto de controle do utilit&#225;rio (Utilit&#225;rio do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c048a416-900e-4c77-8243-e0f0d8b94068
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Remover um ponto de controle do utilit&#225;rio (Utilit&#225;rio do SQL Server)
  Este tópico descreve como remover um UCP (ponto de controle do utilitário) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para remover um ponto de controle do utilitário, usando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Antes de usar esse procedimento para remover o UCP do utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , observe os requisitos a seguir. O procedimento armazenado executará verificações de pré-requisito da operação.  
  
-   Para executar esse procedimento, todas as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser removidas do UCP. Observe que o UCP é uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Remover uma instância do SQL Server do Utilitário do SQL Server](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
-   Esse procedimento deve ser executado em um computador que seja um UCP.  
  
-   Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que o UCP foi removido tiver um conjunto de coleta de dados que não seja do Utilitário, o banco de dados UMDW (sysutility_mdw) não será removido do procedimento. Nesse caso, o banco de dados UMDW (sysutility_mdw) deverá ser removido manualmente antes do UCP ser recriado.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Esse procedimento deve ser executado por um usuário com permissões de **sysadmin** ; as mesmas permissões necessárias para criar um UCP.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para remover um ponto de controle do utilitário  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
## Consulte também  
 [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Usar o Gerenciador do Utilitário para gerenciar o Utilitário do SQL Server](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [Solucionar problemas do Utilitário do SQL Server](../Topic/Troubleshoot%20the%20SQL%20Server%20Utility.md)  
  
  