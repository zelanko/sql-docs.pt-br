---
title: MSSQL_ENG018456 | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG018456 error
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8add3ed10585ee1b10fbc12e32707847d996117
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="mssqleng018456"></a>MSSQL_ENG018456
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|18456|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Falha no logon do usuário '%.*ls'.%.\*ls|  
  
## <a name="explanation"></a>Explicação  
 O erro MSSQL_ENG018456 ocorre sempre que uma tentativa de logon falha. Se a mensagem de erro incluir a conta **distributor_admin** (Falha de logon para o usuário 'distributor_admin'.), o problema estará relacionado a uma conta usada pela replicação. A replicação cria um servidor remoto, **repl_distributor**, que permite a comunicação entre o Distribuidor e o Publicador. O logon **distributor_admin** é associado a esse servidor remoto e tem uma senha válida.  
  
## <a name="user-action"></a>Ação do usuário  
 Certifique-se de ter especificado uma senha para a conta. Para obter mais informações, consulte [Proteger o Distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
