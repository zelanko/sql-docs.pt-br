---
title: Comandos que geram resultados de vários conjuntos de linhas (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- SQL Server Native Client OLE DB provider, commands
- SQL Server Native Client OLE DB provider, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
ms.assetid: 4567668d-35fd-4162-b61f-f7536862cdcb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d9febce09a93e92ff2a344b091fd3cd85d6bdc2b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247038"
---
# <a name="sql-server-native-client-commands-generating-multiple-rowset-results"></a>Comandos de SQL Server Native Client gerando resultados de vários conjuntos de linhas
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo pode retornar vários conjuntos de linhas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instruções. As instruções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornam resultados de vários conjuntos de linhas nas seguintes condições:  
  
-   Instruções SQL processadas em lotes são enviadas como um único comando.  
  
-   Os procedimentos armazenados implementam um lote de instruções SQL.  
  
## <a name="batches"></a>Lotes  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo reconhece o caractere ponto e vírgula como um delimitador de lote para instruções SQL:  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 Enviar várias instruções SQL em um único lote é mais eficiente do que executar cada instrução SQL separadamente. O envio de um lote reduz as viagens de ida e volta de rede do cliente para o servidor.  
  
## <a name="stored-procedures"></a>Procedimentos armazenados  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna um conjunto de resultados para cada instrução em um procedimento armazenado, assim a maioria dos procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna vários conjuntos de resultados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando IMultipleResults para processar vários conjuntos de resultados](../../relational-databases/native-client-ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
