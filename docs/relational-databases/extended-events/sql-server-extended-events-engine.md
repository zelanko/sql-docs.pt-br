---
title: Mecanismo de eventos estendidos do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], engine
ms.assetid: d74642a5-42b9-4a15-aa3d-f98bfe695050
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: adc05e30e226e298236de8bae1d45d43bb607001
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39532956"
---
# <a name="sql-server-extended-events-engine"></a>Mecanismo de eventos estendidos do SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  O mecanismo de Eventos Estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é uma coleção de serviços e objetos que:  
  
-   Habilita a definição de eventos.  
  
-   Habilita dados de evento de processamento.  
  
-   Gerencia serviços de eventos estendidos e objetos no sistema.  
  
-   Mantenha uma lista de sessões de eventos estendidos e gerencie o acesso àquela lista.  
  
 O mecanismo de eventos estendidos não fornece qualquer evento ou ações que ocorram quando um evento é disparado. Os processos que usam o mecanismo de evento estendido definem interação com o mecanismo. Estes processos adicionam pontos de evento e fornecem ações para que ocorram em resposta ao disparo do evento.  
  
 A ilustração seguinte mostra uma exibição simplificada de uma sessão de eventos estendidos. Para obter mais informações, consulte [Sessões de eventos estendidos do SQL Server](../../relational-databases/extended-events/sql-server-extended-events-sessions.md).  
  
 ![Arquitetura detalhada de eventos estendidos](../../relational-databases/extended-events/media/xearchitecturedetailed.gif "Arquitetura detalhada de eventos estendidos")  
  
 Observe o seguinte:  
  
-   Cada processo do Windows pode ter um ou mais módulos (**processo Win32**, **módulo Win32**). Estes também são conhecidos como *binários* ou *módulos de executáveis*.  
  
-   Cada um dos módulos de processo do Windows pode conter um ou mais pacotes de eventos estendidos (**Pacote**) que contêm um ou mais objetos de eventos estendidos (**Tipo**, **Destino**, **Ação**, **Mapa**, **Predicado**e **Evento**).  
  
-   Dentro de um processo de host pode haver só uma instância do mecanismo de eventos estendidos (**Mecanismo de evento estendido**) que:  
  
    -   Gerencia alguns aspectos da sessão (por exemplo, enumerar sessões).  
  
    -   Gerencia envio (**Dispatcher**). Isso é semelhante a um pool de thread.  
  
    -   Gerencia buffers de memória (**Buffer**) para eventos. Quando os buffers estiverem cheios, eles são despachados para os destinos.  
  
-   Depois que uma sessão for criada e os eventos associados à sessão opcionalmente (**Contexto de sessão**):  
  
    -   Instâncias de destinos (**Instância de destino**) podem também ser criadas e adicionadas à sessão.  
  
    -   Quando os buffers estão cheios, aqueles buffers são despachados para os destinos.  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
