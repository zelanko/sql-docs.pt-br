---
title: MSSQLSERVER_21892 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21892 (Database Engine error)
ms.assetid: 199818e8-28f4-440e-ad85-7bea88f51153
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4ca49ebb4a7481fc7fd23e916d10a185632280cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056648"
---
# <a name="mssqlserver21892"></a>MSSQLSERVER_21892
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21892|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21892|  
|Texto da mensagem|Não é possível consultar sys.availability_replicas no primário do grupo de disponibilidade associado ao nome de rede virtual '%s' quanto aos nomes de servidor das réplicas membro: erro = %d, mensagem de erro = %s.'|  
  
## <a name="explanation"></a>Explicação  
**sp_validate_replica_hosts_as_publishers** consulta o primário atual do grupo de disponibilidade associado ao publicador redirecionado, a fim de determinar as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedam as réplicas membro.  Quando essa consulta falha, o erro 21892 é retornado.  
  
Normalmente, **sp_validate_replica_hosts_as_publishers** está no primeiro uso do servidor vinculado temporário; portanto, se houver problemas de conectividade, será provável que eles apareçam primeiro com **sp_validate_replica_hosts_as_publishers**. Ao contrário de **sp_validate_redirected_publisher**, o servidor vinculado usado por **sp_validate_replica_hosts_as_publishers** sempre usa as credenciais do chamador ao se conectar a qualquer um dos hosts de réplica do grupo de disponibilidade.  
  
## <a name="user-action"></a>Ação do usuário  
Ao executar este procedimento armazenado, verifique se a execução está sendo realizada a partir de um logon válido em todas as réplicas. O logon exigirá autorização suficiente para consultar tabelas de metadados de grupo de disponibilidade, bem como para consultar as tabelas de metadados de assinatura na réplica do banco de dados publicador.  
  
Examine o erro referenciado original para determinar a causa da falha e execute a ação corretiva apropriada.  
  
