---
title: Criar um conjunto de linhas com IOpenRowset (Driver do OLE DB) | Microsoft Docs
description: Criar um conjunto de linhas com a interface IOpenRowset do Driver do OLE DB para SQL Server
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
ms.openlocfilehash: 721a54d4e423675fa5dad39d22e8f94c178228d6
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942372"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Criando um conjunto de linhas com IOpenRowset
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server dá suporte ao método **IOpenRowset::OpenRowset** com as seguintes restrições:  
  
-   É necessário especificar uma exibição ou uma tabela base em uma estrutura DBID (ID de banco de dados) para a qual o parâmetro *pTableID* aponte.  
  
-   O membro *eKind* de DBID precisa indicar DBKIND_NAME.  
  
-   O membro *uName* de DBID precisa especificar o nome de uma exibição ou uma tabela base existente como uma cadeia de caracteres Unicode.  
  
-   O parâmetro *pIndexID* de **OpenRowset** precisa ser NULL.  
  
 O conjunto de resultados de **IOpenRowset::OpenRowset** contém um único conjunto de linhas. Conjuntos de resultados que contêm um só conjunto de linhas podem ter suporte por meio de cursores [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O suporte de cursor permite ao desenvolvedor usar mecanismos de simultaneidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
