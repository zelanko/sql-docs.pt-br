---
title: Suporte ao OLE DB Driver for SQL Server para LocalDB | Microsoft Docs
description: Saiba como se conectar a uma versão leve do SQL Server, chamada LocalDB, usando o Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c7f5ac94ff64ef32aaee793c59529ad0377b2f5
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860678"
---
# <a name="ole-db-driver-for-sql-server-support-for-localdb"></a>Suporte ao OLE DB Driver for SQL Server para LocalDB
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], uma versão leve do SQL Server, denominada LocalDB, será disponibilizada. Este tópico descreve como conectar-se a um banco de dados em uma instância do LocalDB.  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar sua instância do LocalDB, consulte:  
  
-   [Referência de LocalDB do SQL Server Express](../../../relational-databases/sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 Para resumir, o LocalDB permite:  
  
-   Usar **sqllocaldb.exe i** para descobrir o nome da instância padrão.  
  
-   Usar a palavra-chave da cadeia de conexão **AttachDBFilename** para especificar o arquivo de banco de dados que o servidor deve anexar. Ao usar **AttachDBFilename**, se você não especificar o nome do banco de dados com a palavra-chave da cadeia de conexão **Database** , o banco de dados será removido da instância do LocalDB quando o aplicativo for fechado.  
  
-   Especifique uma instância do LocalDB em sua cadeia de conexão:  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 Se necessário, você pode criar uma instância do LocalDB com sqllocaldb.exe. Você também pode usar sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, **sqlcmd -S (localdb)\v11.0**.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
