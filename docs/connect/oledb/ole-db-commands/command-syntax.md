---
title: Sintaxe do comando | Microsoft Docs
description: Sintaxe de comando e procedimentos armazenados
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3aae81f928c269763aa89e92227cdb013c22cf22
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="command-syntax"></a>Sintaxe de comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server reconhece a sintaxe de comando especificada pela macro DBGUID_SQL. O condutor do OLE DB para SQL Server, o especificador indica que um amálgama de ODBC SQL, ISO, e [!INCLUDE[tsql](../../../includes/tsql-md.md)] é uma sintaxe válida. Por exemplo, a seguinte instrução SQL usa uma sequência de escape do ODBC SQL para especificar a função de cadeia de caracteres LCASE:  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE retorna uma cadeia de caracteres, convertendo todos os caracteres em maiúscula aos seus equivalentes em minúsculas. A função LOWER de cadeia de caracteres ISO executa a mesma operação, assim a seguinte instrução SQL é uma equivalente ISO para a instrução ODBC apresentada acima:  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 O Driver OLE DB para SQL Server processa o formulário da instrução com êxito quando especificado como o texto de um comando.  
  
## <a name="stored-procedures"></a>Procedimentos armazenados  
 Ao executar uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] procedimento armazenado usando um Driver OLE DB para o comando do SQL Server, use a sequência de escape CALL do ODBC no texto do comando. O Driver OLE DB para SQL Server, em seguida, usa o mecanismo de chamada de procedimento remoto de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para otimizar o processamento do comando. Por exemplo, a seguinte instrução SQL do ODBC é o texto de comando preferido à forma do [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
