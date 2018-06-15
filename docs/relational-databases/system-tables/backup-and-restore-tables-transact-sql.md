---
title: Backup e restauração de tabelas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system tables [SQL Server], backup tables
- backup system tables [SQL Server]
- system tables [SQL Server], restore tables
- restore system tables [SQL Server]
ms.assetid: aa615add-54e6-40f5-8b55-3728b26884ee
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09a35a516808c5330199cd60f1e9dbde9192d004
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33256431"
---
# <a name="backup-and-restore-tables-transact-sql"></a>Tabelas de backup e restauração (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os tópicos desta seção descrevem as tabelas do sistema que armazenam informações usadas pelas operações de backup e restauração do banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
 [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
 Contém uma linha para cada arquivo de dados ou de log do banco de dados.  
  
 [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
 Contém uma linha para cada grupo de arquivos em um banco de dados no momento do backup.  
  
 [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
 Contém uma linha para cada família de mídia.  
  
 [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
 Contém uma linha para cada conjunto de mídias de backup.  
  
 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
 Contém uma linha para cada conjunto de backup.  
  
 [logmarkhistory](../../relational-databases/system-tables/logmarkhistory-transact-sql.md)  
 Contém uma linha para cada transação marcada que foi confirmada.  
  
 [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
 Contém uma linha para cada arquivo restaurado. Isso inclui arquivos restaurados indiretamente pelo nome do grupo de arquivos.  
  
 [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
 Contém uma linha para cada grupo de arquivos restaurado.  
  
 [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
 Contém uma linha para cada operação de restauração.  
  
 [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md)  
 Contém uma linha por página com falha com um erro 824 (com um limite de 1.000 linhas).  
  
 [sysopentapes](../../relational-databases/system-tables/sysopentapes-transact-sql.md)  
 Contém uma linha para cada dispositivo de fita aberto atualmente.  
  
  
