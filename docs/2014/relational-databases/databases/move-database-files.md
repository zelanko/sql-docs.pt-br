---
title: Mover arquivos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f851fd637ef1781bb1446219e284109e96c306fa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193376"
---
# <a name="move-database-files"></a>Mover arquivos de banco de dados
  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível mover bancos de dados de usuários e sistemas especificando o novo local do arquivo na cláusula FILENAME da instrução [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) . É possível mover arquivos de dados, logs e catálogos de texto completo deste modo. Isso pode ser útil nas seguintes situações:  
  
-   Recuperação de falha. Por exemplo, o banco de dados está em modo suspeito ou foi fechado por causa de um problema de hardware.  
  
-   Realocação planejada.  
  
-   Realocação para manutenção de disco programada.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Mover bancos de dados de usuário](move-user-databases.md)|Descreve os procedimentos para mover arquivos de banco de dados de usuários e arquivos de catálogo de texto completo para um local novo.|  
|[Mover bancos de dados do sistema](system-databases.md)|Descreve os procedimentos para mover arquivos de banco de dados de sistema para um novo local.|  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
