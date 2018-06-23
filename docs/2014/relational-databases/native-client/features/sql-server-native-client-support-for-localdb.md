---
title: Suporte do SQL Server Native Client para LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 144fe940cd1be0c2338e4e874658738b8854583d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115418"
---
# <a name="sql-server-native-client-support-for-localdb"></a>Suporte do SQL Server Native Client para LocalDB
  A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], uma versão leve do SQL Server, denominada LocalDB, será disponibilizada. Este tópico descreve como conectar-se a um banco de dados em uma instância do LocalDB.  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar sua instância do LocalDB, consulte:  
  
-   [Referência do SQL Server Express LocalDB](../../sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2014 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 Para resumir, o LocalDB permite:  
  
-   Usar `sqllocaldb.exe i` para descobrir o nome da instância padrão.  
  
-   Usar a palavra-chave da cadeia de conexão `AttachDBFilename` para especificar o arquivo de banco de dados que o servidor deve anexar. Ao usar `AttachDBFilename`, se você não especificar o nome do banco de dados com o **banco de dados** palavra-chave cadeia de caracteres de conexão, o banco de dados será removido da instância do LocalDB quando o aplicativo for fechado.  
  
-   Especifique uma instância do LocalDB em sua cadeia de conexão:  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 Se necessário, você pode criar uma instância do LocalDB com sqllocaldb.exe. Você também pode usar sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, `sqlcmd -S (localdb)\v11.0`.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
  