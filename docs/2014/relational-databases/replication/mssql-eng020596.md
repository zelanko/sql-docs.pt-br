---
title: MSSQL_ENG020596 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020596 error
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ddabe3e1a3a12e3aa14c5a6c641345d3236c2fe2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52776898"
---
# <a name="mssqleng020596"></a>MSSQL_ENG020596
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|20596|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Somente '%s' ou membros de db_owner podem descartar o agente anônimo.|  
  
## <a name="explanation"></a>Explicação  
 Você não tem permissões adequadas para descartar o agente da assinatura anônima. O logon usado para chamar [sp_dropanonymousagent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql) deve ser um membro da função de servidor fixa **sysadmin** no Distribuidor ou da função de banco de dados fixa **db_owner** no banco de dados de distribuição ou, então, o usuário deve ter iniciado a primeira execução do agente.  
  
## <a name="user-action"></a>Ação do usuário  
 Efetue logon com as credenciais apropriadas e execute **sp_dropanonymousagent**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
