---
title: Suporte do SQL Server Native Client para LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a3f5a8214c2966b1958c3a4ea08edbee5af6a2d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225482"
---
# <a name="sql-server-native-client-support-for-localdb"></a>Suporte do SQL Server Native Client para LocalDB
  A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], uma versão leve do SQL Server, denominada LocalDB, será disponibilizada. Este tópico descreve como conectar-se a um banco de dados em uma instância do LocalDB.  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar sua instância do LocalDB, consulte:  
  
-   [Referência de LocalDB do SQL Server Express](../../sql-server-express-localdb-reference.md)  
  
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
  
  
