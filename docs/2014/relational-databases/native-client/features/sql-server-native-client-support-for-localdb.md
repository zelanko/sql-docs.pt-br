---
title: Suporte do SQL Server Native Client para LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c62b4a7c6db2bc7a53c616079d75110ff8c3ad95
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414045"
---
# <a name="sql-server-native-client-support-for-localdb"></a>Suporte do SQL Server Native Client para LocalDB
  A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], uma versão leve do SQL Server, denominada LocalDB, será disponibilizada. Este tópico descreve como conectar-se a um banco de dados em uma instância do LocalDB.  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar sua instância do LocalDB, consulte:  
  
-   [Referência do SQL Server Express LocalDB](../../sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2014 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 Para resumir, o LocalDB permite:  
  
-   Usar `sqllocaldb.exe i` para descobrir o nome da instância padrão.  
  
-   Usar a palavra-chave da cadeia de conexão `AttachDBFilename` para especificar o arquivo de banco de dados que o servidor deve anexar. Ao usar `AttachDBFilename`, se você não especificar o nome do banco de dados com o **banco de dados** palavra-chave da cadeia de conexão, o banco de dados será removido da instância do LocalDB quando o aplicativo é fechado.  
  
-   Especifique uma instância do LocalDB em sua cadeia de conexão:  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 Se necessário, você pode criar uma instância do LocalDB com sqllocaldb.exe. Você também pode usar sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, `sqlcmd -S (localdb)\v11.0`.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
  
