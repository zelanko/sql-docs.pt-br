---
title: Sintaxe de comando | Microsoft Docs
description: Sintaxe de comando e procedimentos armazenados
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8e7fab68cc4a945bc34c64b2b832b182c734d927
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105932"
---
# <a name="command-syntax"></a>Sintaxe de comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server reconhece a sintaxe de comando especificada pela macro DBGUID_SQL. Para o Driver do OLE DB para SQL Server, o especificador indica que um amálgama de ODBC SQL, ISO, e [!INCLUDE[tsql](../../../includes/tsql-md.md)] é uma sintaxe válida. Por exemplo, a seguinte instrução SQL usa uma sequência de escape do ODBC SQL para especificar a função de cadeia de caracteres LCASE:  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE retorna uma cadeia de caracteres, convertendo todos os caracteres em maiúscula aos seus equivalentes em minúsculas. A função LOWER de cadeia de caracteres ISO executa a mesma operação, assim a seguinte instrução SQL é uma equivalente ISO para a instrução ODBC apresentada acima:  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 O OLE DB Driver for SQL Server processa uma das duas formas da instrução com êxito quando especificada como texto de um comando.  
  
## <a name="stored-procedures"></a>Procedimentos armazenados  
 Ao executar um procedimento armazenado do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando um comando do OLE DB Driver for SQL Server, use a sequência de escape CALL do ODBC no texto do comando. Em seguida, o OLE DB Driver for SQL Server usa o mecanismo de chamada de procedimento remoto do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para otimizar o processamento do comando. Por exemplo, a seguinte instrução SQL do ODBC é o texto de comando preferido à forma do [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
