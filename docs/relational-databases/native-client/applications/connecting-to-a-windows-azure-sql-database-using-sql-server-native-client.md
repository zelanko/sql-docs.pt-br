---
title: Conectar-se ao Banco de Dados SQL do Azure
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: db4f18fc780f1c3b0a88b5c18cd2ff3410800dad
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823641"
---
# <a name="connecting-to-an-azure-sql-database-using-sql-server-native-client"></a>Connecting to an Azure SQL Database Using SQL Server Native Client (Conectando a um Banco de Dados SQL do Azure usando o SQL Server Native Client)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Para obter um exemplo que mostra como se conectar a um [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] usando um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente nativo, consulte [desenvolvimento: tópicos de instruções (banco de dados SQL do Azure)](https://msdn.microsoft.com/library/ee621787.aspx).  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>Problemas conhecidos ao conectar a um banco de dados SQL  
 Estes são problemas conhecidos ao conectar a um [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   Uma conexão feita com **SQLBrowseConnect** poderá ser rejeitada se **SQLBrowseConnect** for usado em estágios.  Por exemplo, se o nome do driver for enviado na primeira chamada, o servidor e as credenciais (usuário e senha) serão enviados na segunda chamada, estabelecendo a conexão, e um nome de banco de dados e um idioma na terceira chamada.  A terceira chamada levará o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a emitir uma instrução USE para alterar bancos de dados. Entretanto, a instrução USE não tem suporte no [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], gerando o seguinte erro:  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
