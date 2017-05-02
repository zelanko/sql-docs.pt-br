---
title: MSSQLSERVER_21892 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 21892 (Database Engine error)
ms.assetid: 199818e8-28f4-440e-ad85-7bea88f51153
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3ce5f5c4d88232aee27695aae35bfcf55734497d
ms.lasthandoff: 04/11/2017

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
**sp_validate_replica_hosts_as_publishers** consulta o primário atual do grupo de disponibilidade associado ao publicador redirecionado, a fim de determinar as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedam as réplicas membro.  Quando essa consulta falha, o erro 21892 é retornado.  
  
Normalmente, **sp_validate_replica_hosts_as_publishers** está no primeiro uso do servidor vinculado temporário; portanto, se houver problemas de conectividade, será provável que eles apareçam primeiro com **sp_validate_replica_hosts_as_publishers**. Ao contrário de **sp_validate_redirected_publisher**, o servidor vinculado usado por **sp_validate_replica_hosts_as_publishers** sempre usa as credenciais do chamador ao se conectar a qualquer um dos hosts de réplica do grupo de disponibilidade.  
  
## <a name="user-action"></a>Ação do usuário  
Ao executar este procedimento armazenado, verifique se a execução está sendo realizada a partir de um logon válido em todas as réplicas. O logon exigirá autorização suficiente para consultar tabelas de metadados de grupo de disponibilidade, bem como para consultar as tabelas de metadados de assinatura na réplica do banco de dados publicador.  
  
Examine o erro referenciado original para determinar a causa da falha e execute a ação corretiva apropriada.  
  

