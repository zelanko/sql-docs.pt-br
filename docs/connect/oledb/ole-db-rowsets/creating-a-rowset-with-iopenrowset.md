---
title: Criando um conjunto de linhas com IOpenRowset | Microsoft Docs
description: Criando um conjunto de linhas com IOpenRowset interface do Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e89c61159ccc2b0faee46f1709adccee67a182a2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Criando um conjunto de linhas com IOpenRowset
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server oferece suporte a **IOpenRowset:: OPENROWSET** método com as seguintes restrições:  
  
-   Uma tabela base ou exibição deve ser especificada em um banco de dados ID (DBID) estrutura que o *pTableID* parâmetro aponta para.  
  
-   O DBID *eKind* membro deve indicar DBKIND_NAME.  
  
-   O DBID *uName* membro deve especificar o nome de uma tabela base existente ou uma exibição como uma cadeia de caracteres Unicode.  
  
-   O *pIndexID* parâmetro **OpenRowset** deve ser NULL.  
  
 O conjunto de resultados de **IOpenRowset:: OPENROWSET** contém um único conjunto de linhas. Conjuntos de resultados que contêm um único conjunto de linhas podem ter suporte de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cursores. O suporte de cursor permite ao desenvolvedor usar mecanismos de simultaneidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
