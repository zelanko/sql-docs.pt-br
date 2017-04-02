---
title: "Mover arquivos de banco de dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "recuperação de desastre [SQL Server], movendo arquivos de banco de dados"
  - "arquivos [SQL Server], movendo"
  - "arquivos de dados [SQL Server], movendo"
  - "movendo arquivos [SQL Server]"
  - "movendo catálogos de texto completo"
  - "movendo bancos de dados"
  - "catálogos de texto completo [SQL Server], movendo"
  - "movendo arquivos de banco de dados"
  - "manutenção de disco programada [SQL Server]"
  - "movendo arquivos"
  - "realocando arquivos de banco de dados"
  - "realocações planejadas de banco de dados [SQL Server]"
  - "banco de dados [SQL Server], movendo"
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Mover arquivos de banco de dados
  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível mover bancos de dados de usuários e sistemas especificando o novo local do arquivo na cláusula FILENAME da instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md). É possível mover arquivos de dados, logs e catálogos de texto completo deste modo. Isso pode ser útil nas seguintes situações:  
  
-   Recuperação de falha. Por exemplo, o banco de dados está em modo suspeito ou foi fechado por causa de um problema de hardware.  
  
-   Realocação planejada.  
  
-   Realocação para manutenção de disco programada.  
  
## Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Mover bancos de dados de usuário](../../relational-databases/databases/move-user-databases.md)|Descreve os procedimentos para mover arquivos de banco de dados de usuários e arquivos de catálogo de texto completo para um local novo.|  
|[Mover bancos de dados do sistema](../../relational-databases/databases/move-system-databases.md)|Descreve os procedimentos para mover arquivos de banco de dados de sistema para um novo local.|  
  
## Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  