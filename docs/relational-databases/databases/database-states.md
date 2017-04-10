---
title: "Estados de banco de dados | Microsoft Docs"
ms.custom: ""
ms.date: "07/14/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SWB.DATABASESTATES.F1"
helpviewer_keywords: 
  - "estado do banco de dados de emergência [SQL Server]"
  - "verificando estados de banco de dados"
  - "exibindo estados de banco de dados"
  - "exibindo estados de banco de dados"
  - "estados de banco de dados [SQL Server]"
  - "estado de banco de dados atual"
  - "estado do banco de dados offline [SQL Server]"
  - "estado de banco de dados suspeito"
  - "estado de banco de dados de recuperação pendente [SQL Server]"
  - "estados [SQL Server], bancos de dados"
  - "estado de banco de dados online"
  - "estados [SQL Server]"
  - "estado de banco de dados restauração [SQL Server]"
ms.assetid: b7f1f111-ca73-4a89-b567-a98d64d6ecb3
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Estados de banco de dados
  Um banco de dados sempre está em um estado específico. Por exemplo, esses estados incluem ONLINE, OFFLINE ou SUSPECT. Para verificar o estado atual de um banco de dados, selecione a coluna **state_desc** na exibição de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ou a propriedade **Status** da função [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
## Definições de estado de banco de dados  
 A tabela a seguir define os estados de banco de dados.  
  
|Estado|Definição|  
|-----------|----------------|  
|ONLINE|O banco de dados está disponível para acesso. O grupo de arquivos primário está on-line, embora a fase desfazer de recuperação pode não ter sido completada.|  
|OFFLINE|O banco de dados está indisponível. Um banco de dados se torna off-line por ação explícita do usuário e permanece off-line até que uma ação adicional do usuário seja executada. Por exemplo, o banco de dados pode ser ficar off-line para que um arquivo seja movido para um novo disco. O banco de dados é, então, colocado on-line novamente, após a mudança ter sido concluída.|  
|RESTORING|Um ou mais arquivos do grupo de arquivos primário está sendo restaurado ou um ou mais arquivos secundários está sendo restaurado off-line. O banco de dados está indisponível.|  
|RECOVERING|O banco de dados está sendo recuperado. O processo de recuperação é um estado transitório, o banco de dados ficará on-line automaticamente se a recuperação for bem-sucedida. Se a recuperação falhar, o banco de dados se tornará suspeito. O banco de dados está indisponível.|  
|RECOVERY_PENDING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou um erro relacionado a recurso durante a recuperação. O banco de dados não está danificado, mas arquivos podem ter sido perdidos ou limitações de recursos do sistema podem estar impedindo sua inicialização. O banco de dados está indisponível. Uma ação adicional é exigida do usuário para resolver o erro e permitir que o processo de recuperação seja concluído.|  
|SUSPECT|Pelo menos o grupo de arquivos primário é suspeito e pode estar danificado. O banco de dados não pode ser recuperado durante a inicialização de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O banco de dados está indisponível. Ação adicional pelo usuário é exigida para resolver o problema.|  
|EMERGENCY|O usuário alterou o banco de dados e definiu o estado como EMERGENCY. O banco de dados está em modo de usuário único e pode ser reparado ou restaurado. O banco de dados está marcado como READ_ONLY, o log está desabilitado e o acesso é limitado aos membros da função de servidor fixa **sysadmin**. EMERGENCY é usado principalmente para a solução de problemas. Por exemplo, um banco de dados marcado como o suspeito pode ser definido como o estado EMERGENCY. Isso permitiria o acesso somente leitura do administrador de sistema ao banco de dados. Apenas membros da função de servidor fixa **sysadmin** podem definir um banco de dados com o estado EMERGENCY.|  
  
## Conteúdo relacionado  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
 [Estados de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [Estados de arquivo](../../relational-databases/databases/file-states.md)  
  
  