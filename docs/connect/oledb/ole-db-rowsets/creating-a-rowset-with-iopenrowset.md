---
title: Criando um conjunto de linhas com IOpenRowset | Microsoft Docs
description: Criar um conjunto de linhas com IOpenRowset interface do Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 78b08a3da3da89e0db0d801945416dcdb1ff9c03
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799212"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Criando um conjunto de linhas com IOpenRowset
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server dá suporte a **IOpenRowset:: OPENROWSET** método com as seguintes restrições:  
  
-   É necessário especificar uma exibição ou uma tabela base em uma estrutura DBID (ID de banco de dados) para a qual o parâmetro *pTableID* aponte.  
  
-   O membro *eKind* de DBID precisa indicar DBKIND_NAME.  
  
-   O membro *uName* de DBID precisa especificar o nome de uma exibição ou uma tabela base existente como uma cadeia de caracteres Unicode.  
  
-   O parâmetro *pIndexID* de **OpenRowset** precisa ser NULL.  
  
 O conjunto de resultados de **IOpenRowset::OpenRowset** contém um único conjunto de linhas. Conjuntos de resultados que contêm um único conjunto de linhas podem ter suporte por meio de cursores [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O suporte de cursor permite ao desenvolvedor usar mecanismos de simultaneidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
