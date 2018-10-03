---
title: Instantâneos do banco de dados com Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 7432da1c-ce2f-4cd9-af41-54c97744166b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 434d0ef7782766cfcf5a590c6a6adc3e5e13f504
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808674"
---
# <a name="database-snapshots-with-always-on-availability-groups-sql-server"></a>Instantâneos do banco de dados com grupos de disponibilidade AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Você pode criar um instantâneo de banco de dados em um banco de dados primário ou secundário em um grupo de disponibilidade. A função de réplica deve ser PRIMARY ou SECONDARY, em vez de estar no estado RESOLVING.  
  
 É recomendável que o estado de sincronização de banco de dados seja SYNCHRONIZING ou SYNCHRONIZED quando você criar um instantâneo de banco de dados. No entanto, os instantâneos de banco de dados poderão ser criados quando o estado de sincronização de banco de dados for NOT SYNCHRONIZING.  
  
 Um instantâneo do banco de dados em uma réplica secundária deverá continuar funcionando se a réplica for desconectada (DISCONNECTED) da réplica primária.  
  
 Algumas condições de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] fazem o banco de dados de origem e seus instantâneos do banco de dados serem reiniciados, desconectando os usuários temporariamente. Estas condições são as seguintes:  
  
-   A réplica primária altera funções, ou porque a réplica primária atual é desconectada e fica online novamente na mesma instância de servidor ou porque o grupo de disponibilidade realiza o failover.  
  
-   O banco de dados entra na função secundária.  
  
 Se a réplica de disponibilidade que hospeda os instantâneos do banco de dados realizar failover, os instantâneos do banco de dados permanecerão na instância de servidor onde foram criados. Os usuários podem continuar usando os instantâneos depois do failover. Se o desempenho for uma preocupação em seu ambiente, nós recomendamos que você crie instantâneos do banco de dados somente em bancos de dados secundários que estão hospedados por uma réplica secundária que está configurada para modo de failover manual.  Se você já realizou failover manual no grupo de disponibilidade para esta réplica secundária, poderá criar um novo conjunto de instantâneos do banco de dados em outra réplica secundária, redirecionar clientes para os novos instantâneos do banco de dados e remover todos os instantâneos dos bancos de dados agora primários.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Instantâneos de banco de dados &#40;SQL Server&#41;](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
