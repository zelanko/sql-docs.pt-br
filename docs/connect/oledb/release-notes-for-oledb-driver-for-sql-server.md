---
title: Release Notes (Driver do OLE DB para SQL Server) | Microsoft Docs
ms.date: 07/03/2018
ms.prod: sql
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
ms.openlocfilehash: 698ac0a38edb55bca36c2d7dc15c9c7c2faf3efe
ms.sourcegitcommit: 368a7f7e9d860f9407a5a013e135f29f27efcd02
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37872886"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Notas de versão do Driver do Microsoft OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Esta página discute o que foi adicionado em cada versão do Driver da Microsoft OLE DB para SQL Server.

## <a name="whats-new-in-version-1810"></a>Novidades da versão 18.1.0

**Recursos adicionados:**

* Suporte para `UseFMTONLY` palavra-chave de cadeia de caracteres de conexão e `SSPROP_INIT_USEFMTONLY` propriedade de inicialização.
`UseFMTONLY` Controla como os metadados são recuperados ao se conectar ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e mais recente.  
Para obter mais informações, consulte:
  * [Uso de palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

**Bugs corrigidos:**

* Fixo versão incorreta do arquivo de formato BCP. O 18.0 do Driver de banco de dados OLE incorretamente define a versão do arquivo de formato BCP para 18.0 em vez de 11.0. Arquivos de formato gerados pelo 18.0 do Driver de banco de dados OLE não podem ser lido pelo 18.1 do Driver de banco de dados OLE. Se você precisar usar arquivos de formato gerados pela versão anterior do driver com o novo driver, você pode editar manualmente os arquivos para alterar a versão 11.0.

## <a name="whats-new-in-version-1802"></a>Novidades da versão 18.0.2

**Recursos adicionados**:

* Suporte para `MultiSubnetFailover` palavra-chave de cadeia de caracteres de conexão e `SSPROP_INIT_MULTISUBNETFAILOVER` propriedade de inicialização.  
Para obter mais informações, consulte:  
  * [Suporte ao Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastre](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
  * [Uso de palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

## <a name="see-also"></a>Confira também
[Driver do Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
