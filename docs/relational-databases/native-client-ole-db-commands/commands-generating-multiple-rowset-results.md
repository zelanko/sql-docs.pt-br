---
title: Comandos que geram resultados de vários conjuntos de linhas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- SQL Server Native Client OLE DB provider, commands
- SQL Server Native Client OLE DB provider, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
ms.assetid: 4567668d-35fd-4162-b61f-f7536862cdcb
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1d836984ac5757909072f5841a8fd2ada2c695ec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="commands-generating-multiple-rowset-results"></a>Comandos que geram resultados de vários conjuntos de linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client pode retornar vários conjuntos de linhas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instruções. As instruções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornam resultados de vários conjuntos de linhas nas seguintes condições:  
  
-   Instruções SQL processadas em lotes são enviadas como um único comando.  
  
-   Os procedimentos armazenados implementam um lote de instruções SQL.  
  
## <a name="batches"></a>Lotes  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client reconhece o caractere de ponto e vírgula como um delimitador de lote para instruções SQL:  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 Enviar várias instruções SQL em um único lote é mais eficiente do que executar cada instrução SQL separadamente. O envio de um lote reduz as viagens de ida e volta de rede do cliente para o servidor.  
  
## <a name="stored-procedures"></a>Procedimentos armazenados  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna um conjunto de resultados para cada instrução em um procedimento armazenado, assim a maioria dos procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna vários conjuntos de resultados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando IMultipleResults para processar vários conjuntos de resultados](../../relational-databases/native-client-ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>Consulte também  
 [Comandos](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
