---
title: Mover arquivos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9e283055864a824d2a575fb77e0d64fcd1f2a990
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37276812"
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
  
  
