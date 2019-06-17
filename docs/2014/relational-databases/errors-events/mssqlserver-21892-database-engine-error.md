---
title: MSSQLSERVER_21892 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21892 (Database Engine error)
ms.assetid: 199818e8-28f4-440e-ad85-7bea88f51153
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18916e8287841015727c37ed8833fbc29b1e6ba2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869142"
---
# <a name="mssqlserver21892"></a>MSSQLSERVER_21892
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21892|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21892|  
|Texto da mensagem|Não é possível consultar sys.availability_replicas no primário do grupo de disponibilidade associado ao nome de rede virtual '%s' quanto aos nomes de servidor das réplicas membro: erro = %d, mensagem de erro = %s.',|  
  
## <a name="explanation"></a>Explicação  
 `sp_validate_replica_hosts_as_publishers` consulta a réplica primária atual do grupo de disponibilidade associado ao publicador redirecionado, a fim de determinar as instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedam as réplicas de membro.  Quando essa consulta falha, o erro 21892 é retornado.  
  
 `sp_validate_replica_hosts_as_publishers` é geralmente um dos primeiros usos do servidor vinculado temporário; portanto, se houver problemas de conectividade, eles provavelmente aparecerão primeiro com `sp_validate_replica_hosts_as_publishers`. Diferente de `sp_validate_redirected_publisher`, o servidor vinculado usado por `sp_validate_replica_hosts_as_publishers` sempre usa as credenciais do chamador ao se conectar a qualquer host de réplica de grupo de disponibilidade.  
  
## <a name="user-action"></a>Ação do usuário  
 Ao executar este procedimento armazenado, verifique se a execução está sendo realizada a partir de um logon válido em todas as réplicas. O logon exigirá autorização suficiente para consultar tabelas de metadados de grupo de disponibilidade, bem como para consultar as tabelas de metadados de assinatura na réplica do banco de dados publicador.  
  
 Examine o erro referenciado original para determinar a causa da falha e execute a ação corretiva apropriada.  
  
  
