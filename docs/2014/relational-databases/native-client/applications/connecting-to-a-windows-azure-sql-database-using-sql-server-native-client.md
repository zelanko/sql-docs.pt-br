---
title: Conectar-se ao banco de dados SQL do Azure usando o SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a03d8d9aa407fd57f658c76a035650952648dcfc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063756"
---
# <a name="connecting-to-a-azure-sql-database-using-sql-server-native-client"></a>Conectando a um Banco de Dados SQL do Azure usando o SQL Server Native Client
  Para obter um exemplo que mostra como se conectar a um [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] usando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, consulte [desenvolvimento: tópicos de instruções (Windows Azure SQL Database)](http://msdn.microsoft.com/library/ee621787.aspx).  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>Problemas conhecidos ao conectar a um banco de dados SQL  
 Estes são problemas conhecidos ao conectar a um [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   Uma conexão feita com o `SQLBrowseConnect` poderá ser rejeitada se `SQLBrowseConnect` for usado em fases.  Por exemplo, se o nome do driver for enviado na primeira chamada, o servidor e as credenciais (usuário e senha) serão enviados na segunda chamada, estabelecendo a conexão, e um nome de banco de dados e um idioma na terceira chamada.  A terceira chamada levará o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a emitir uma instrução USE para alterar bancos de dados. Entretanto, a instrução USE não tem suporte no [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], gerando o seguinte erro:  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos com o SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  
