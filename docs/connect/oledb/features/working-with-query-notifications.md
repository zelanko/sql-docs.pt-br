---
title: Trabalhando com notificações de consulta | Microsoft Docs
description: Trabalhando com notificações de consulta no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], query notifications
- rowsets [SQL Server], notifications
- OLE DB Driver for SQL Server, query notifications
- notifications [OLE DB Driver for SQL Server]
- query notifications [SQL Server], OLE DB Driver for SQL Server
- canceling rowset changes
- IRowsetNotify interface
- MSOLEDBSQL, query notifications
- OLE DB Driver for SQL Server, query notifications
- consumer notification for rowset changes [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0c425e8bc1b5d3dc9dfe6a5f68998b87a9e7def1
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612341"
---
# <a name="working-with-query-notifications"></a>Trabalhando com notificações de consulta
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Notificações de consulta foram introduzidas no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e OLE DB para SQL Server. Baseadas na infraestrutura do Service Broker, introduzida no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], as notificações de consulta permitem que os aplicativos sejam notificados em caso de alteração nos dados. Esse recurso é particularmente útil para aplicativos que fornecem um cache de informações de um banco de dados, como um aplicativo da Web, e precisam ser notificados quando os dados de origem são alterados.  
  
 As notificações de consulta permitem que você solicite uma notificação em um tempo limite especificado quando os dados subjacentes de uma consulta são alterados. A solicitação por notificação especifica as opções de notificação, que incluem o nome do serviço, o texto da mensagem e o valor do tempo limite do servidor. As notificações são entregues através de uma fila do Service Broker na qual os aplicativos podem sondar as notificações disponíveis.  
  
 A sintaxe da cadeia de opções de notificações de consulta é:  
  
 `service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`  
  
 Por exemplo:  
  
 `service=mySSBService;local database=mydb`  
  
 As assinaturas de notificação duram mais tempo do que o processo que as inicia, já que um aplicativo pode criar uma assinatura de notificação e, em seguida, ser encerrado. A assinatura permanece válida e a notificação será feita se os dados forem alterados no tempo limite especificado na criação da assinatura. Uma notificação é identificada pela consulta executada, pelas opções de notificação e pelo texto da mensagem, podendo ser cancelada definindo-se o valor de seu tempo limite como zero.  
  
 As notificações só são enviadas uma vez. Para que as notificações de alteração de dados sejam contínuas, é preciso criar uma nova assinatura e executar novamente a consulta depois que cada notificação foi processada.  
  
 OLE DB Driver para aplicativos do SQL Server normalmente receber notificações usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] [RECEIVE](../../../t-sql/statements/receive-transact-sql.md) comando para ler as notificações da fila associada ao serviço especificado nas opções de notificação.  
  
> [!NOTE]  
>  Os nomes de tabela devem ser qualificados nas consultas para as quais a notificação é requerida, por exemplo, `dbo.myTable`. Os nomes de tabela devem ser qualificados com nomes de duas partes. A assinatura é considerada inválida se nomes com três ou quatro partes são usados.  
  
 A infraestrutura de notificação baseia-se em um recurso de fila introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Em geral, as notificações geradas no servidor são enviadas através dessas filas para serem processadas posteriormente.  
  
 Para usar notificações de consulta, uma fila e um serviço devem existir no servidor. Eles podem ser criados usando [!INCLUDE[tsql](../../../includes/tsql-md.md)] da seguinte forma:  
  
```  
CREATE QUEUE myQueue  
CREATE SERVICE myService ON QUEUE myQueue   
  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])  
```  
  
> [!NOTE]  
>  O serviço deve usar o contrato predefinido, como mostrado acima.  
  
## <a name="ole-db-driver-for-sql-server"></a>Driver do OLE DB para SQL Server  
 O Driver OLE DB para SQL Server dá suporte à notificação do consumidor na modificação do conjunto de linhas. O consumidor recebe uma notificação em cada fase da modificação do conjunto de linhas e em qualquer tentativa de alteração.  
  
> [!NOTE]  
>  Passando uma consulta de notificação para o servidor com **ICommand:: execute** é a única maneira válida de assinar notificações de consulta com o Driver OLE DB para SQL Server.  
  
### <a name="the-dbpropsetsqlserverrowset-property-set"></a>O conjunto de propriedades DBPROPSET_SQLSERVERROWSET  
 Para oferecer suporte a notificações de consulta através do OLE DB, OLE DB Driver para SQL Server adiciona as propriedades a seguir para o conjunto de propriedades DBPROPSET_SQLSERVERROWSET.  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|O número de segundos que a notificação de consulta permanece ativa.<br /><br /> O padrão é 432,000 segundos (5 dias). O valor mínimo é 1 segundo e o valor máximo é 2^31-1 segundos.|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|O texto da mensagem da notificação. Isso é definido pelo usuário e não tem nenhum formato predefinido.<br /><br /> Por padrão, a cadeia de caracteres fica vazia. Você pode especificar uma mensagem que contenha entre 1-2000 caracteres.|  
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|As opções de notificação de consulta. São especificadas em uma cadeia de caracteres com *nome*=*valor* sintaxe. O usuário é responsável por criar o serviço e ler as notificações da fila.<br /><br /> O padrão é uma cadeia de caracteres vazia.|  
  
 A assinatura de notificação é sempre confirmada, independentemente do fato de a instrução ter sido executada em uma transação de usuário ou em uma confirmação automática ou se a transação na qual a instrução foi executada tiver sido confirmada ou revertida. A notificação do servidor é acionada mediante uma das seguintes condições inválidas de notificação: alteração dos dados subjacentes ou do esquema ou quando o tempo limite expira; a que ocorrer primeiro. Os registros de notificação são excluídos assim que são disparados. Consequentemente, em caso de recebimento de notificações, o aplicativo deve realizar uma nova assinatura caso queira obter mais atualizações.  
  
 Outra conexão ou thread pode verificar se há notificações na fila de destino. Por exemplo:  
  
```  
WAITFOR (RECEIVE * FROM MyQueue);   // Where MyQueue is the queue name.   
```  
  
 Observe que SELECT * não exclui a entrada da fila, porém RECEIVE \* FROM exclui. Isso irá interromper um thread de servidor se a fila estiver vazia. Se houver entradas na fila durante o momento da chamada, elas serão retornadas imediatamente; caso contrário, a chamada aguardará até que seja feita a entrada na fila.  
  
```  
RECEIVE * FROM MyQueue  
```  
  
 Essa instrução retornará imediatamente um conjunto de resultados vazio se a fila estiver vazia; caso contrário, retornará todas as notificações da fila.  
  
 Se SSPROP_QP_NOTIFICATION_MSGTEXT e SSPROP_QP_NOTIFICATION_OPTIONS forem não nulos e não vazios, o cabeçalho do TDS para notificações de consulta que contém as três propriedades definidas acima é enviado ao servidor em cada execução do comando. Se algum deles for nulo (ou vazio), o cabeçalho não será enviado e DB_E_ERRORSOCCURRED será usado, (ou DB_S_ERRORSOCCURRED se as propriedades estiverem marcadas como opcionais), e o valor do status será definido como DBPROPSTATUS_BADVALUE. A validação é feita em Execute/Prepare. De maneira semelhante, db_s_errorsoccured será usado quando as propriedades de notificação de consulta são definidas para conexões com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] versões anteriores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. O valor de status nesse caso é DBPROPSTATUS_NOTSUPPORTED.  
  
 Iniciar uma assinatura não garante que as mensagens subsequentes sejam entregues com êxito. Além disso, nenhuma verificação é feita em relação à validade do nome de serviço especificado.  
  
> [!NOTE]  
>  A preparação de assinaturas nunca fará com que a assinatura seja iniciada; somente a execução da instrução iniciará a assinatura e as notificações de consulta não são impactadas pelo uso dos serviços principais do OLE DB.  
  
 Para obter mais informações sobre o conjunto de propriedades DBPROPSET_SQLSERVERROWSET, consulte [propriedades de conjunto de linhas e comportamentos](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md).  
  

  
## <a name="see-also"></a>Consulte também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)     
  
  
