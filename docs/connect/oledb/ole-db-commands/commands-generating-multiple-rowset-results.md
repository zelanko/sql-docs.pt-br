---
title: Comandos que geram resultados de vários conjuntos de linhas | Microsoft Docs
description: Comandos que geram resultados de vários conjuntos de linhas
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- OLE DB Driver for SQL Server, commands
- OLE DB Driver for SQL Server, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5374e1ccd1024993369091b431a025676bccf1f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016060"
---
# <a name="commands-generating-multiple-rowset-results"></a>Comandos que geram resultados de vários conjuntos de linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O driver OLE DB para SQL Server pode retornar vários conjuntos de linhas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de instruções. As instruções do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retornam resultados de vários conjuntos de linhas nas seguintes condições:  
  
-   Instruções SQL processadas em lotes são enviadas como um único comando.  
  
-   Os procedimentos armazenados implementam um lote de instruções SQL.  
  
## <a name="batches"></a>Lotes  
 O driver OLE DB para SQL Server reconhece o caractere ponto e vírgula como um delimitador de lote para instruções SQL:  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 Enviar várias instruções SQL em um único lote é mais eficiente do que executar cada instrução SQL separadamente. O envio de um lote reduz as viagens de ida e volta de rede do cliente para o servidor.  
  
## <a name="stored-procedures"></a>Procedimentos armazenados  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retorna um conjunto de resultados para cada instrução em um procedimento armazenado, assim a maioria dos procedimentos armazenados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retorna vários conjuntos de resultados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando IMultipleResults para processar vários conjuntos de resultados](../../oledb/ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
