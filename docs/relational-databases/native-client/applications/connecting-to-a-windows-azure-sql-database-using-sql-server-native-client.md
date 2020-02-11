---
title: Cliente nativo, conectar-se ao BD SQL do Azure
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67185f91fa89e84a8733299409b19b2a191fe9bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244212"
---
# <a name="connecting-to-an-azure-sql-database-using-sql-server-native-client"></a>Connecting to an Azure SQL Database Using SQL Server Native Client (Conectando a um Banco de Dados SQL do Azure usando o SQL Server Native Client)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para obter um exemplo que mostra como se conectar a [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando um cliente nativo, consulte [desenvolvimento: tópicos de instruções (banco de dados SQL do Azure)](https://msdn.microsoft.com/library/ee621787.aspx).  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>Problemas conhecidos ao conectar a um banco de dados SQL  
 Estes são problemas conhecidos ao conectar a um [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   Uma conexão feita com **SQLBrowseConnect** poderá ser rejeitada se **SQLBrowseConnect** for usado em estágios.  Por exemplo, se o nome do driver for enviado na primeira chamada, o servidor e as credenciais (usuário e senha) serão enviados na segunda chamada, estabelecendo a conexão, e um nome de banco de dados e um idioma na terceira chamada.  A terceira chamada levará o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a emitir uma instrução USE para alterar bancos de dados. Entretanto, a instrução USE não tem suporte no [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], gerando o seguinte erro:  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
