---
title: Gerenciando o Service Broker
ms.custom: seo-dt-2019
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Service Broker [SMO]
ms.assetid: b29d7432-d1e5-4bb6-b544-57b3a9430f95
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3fe187412a70956d1f4496b6c042e39edafd18c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74094405"
---
# <a name="managing-service-broker"></a>Gerenciando o Service Broker

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  No SMO, os objetos do [!INCLUDE[ssSB](../../../includes/sssb-md.md)] são localizados no namespace **Microsoft.SqlServer.Management.Smo.Broker** , que requer uma referência ao Microsoft.SqlServer.Smo.dll. Uma referência ao Microsoft.SqlServer.ServiceBrokerEnum.dll também é necessária para suportar informações de classe.  
  
 O SMO fornece um conjunto de objetos do [!INCLUDE[ssSB](../../../includes/sssb-md.md)] que permitem gerenciamento programático (DDL) da implementação do [!INCLUDE[ssSB](../../../includes/sssb-md.md)] . Isso inclui a definição de tipos de mensagem, contratos, filas e serviços. Como o SMO é uma ferramenta de gerenciamento não voltada à manipulação de dados, o envio e recebimento de mensagens do [!INCLUDE[ssSB](../../../includes/sssb-md.md)] não são suportados pelo SMO.  
  
 No SMO, o objeto <xref:Microsoft.SqlServer.Management.Smo.Database.ServiceBroker%2A> é a classe de nível superior na qual reside toda a funcionalidade do [!INCLUDE[ssSB](../../../includes/sssb-md.md)]. É necessária uma implementação do [!INCLUDE[ssSB](../../../includes/sssb-md.md)] para cada banco de dados que está participando do aplicativo de mensagens distribuído. Portanto, o objeto <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> é filho do objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> contém coleções dos seguintes objetos usados para definir a implementação do [!INCLUDE[ssSB](../../../includes/sssb-md.md)]:  
  
-   Os objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageType> representam tipos de mensagens que definem o conteúdo das mensagens.  
  
-   Os objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageTypeMapping> representam contratos que especificam a direção e o tipo de mensagens em uma determinada conversa.  
  
-   Os objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceQueue> armazenam as mensagens antes do envio e depois que são recebidas. Eles proporcionam comunicação assíncrona entre serviços, bem como outros benefícios, como o bloqueio automático de mensagens no mesmo grupo de conversa.  
  
-   Os objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.BrokerService> representam serviços [!INCLUDE[ssSB](../../../includes/sssb-md.md)], que são os pontos de extremidade endereçáveis para conversas. As mensagens do [!INCLUDE[ssSB](../../../includes/sssb-md.md)] são enviadas de um serviço para outro. Um serviço especifica uma fila para conter as mensagens e determina os contratos para os quais o serviço pode ser o destino.  
  
-   Os objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.RemoteServiceBinding> representam as configurações que o [!INCLUDE[ssSB](../../../includes/sssb-md.md)] usa para segurança e autenticação ao se comunicar com um serviço remoto.  
  
-   Os objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceRoute> representam uma rota do [!INCLUDE[ssSB](../../../includes/sssb-md.md)], que contém as informações de local para o serviço e o banco de dados no qual ele é definido. Uma rota é necessária para a entrega de mensagens. Por padrão, cada banco de dados contém uma rota que especifica o local como a instância atual do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>   
 [SQL Server Service Broker](../../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
