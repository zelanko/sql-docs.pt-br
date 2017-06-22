---
title: MSSQL_ENG018456 | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG018456 error
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 03184d93644598527b76f054051c66f92ecc6d3e
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng018456"></a>MSSQL_ENG018456
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do Evento|18456|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Falha no logon do usuário '%.*ls'.%.\*ls|  
  
## <a name="explanation"></a>Explicação  
 O erro MSSQL_ENG018456 ocorre sempre que uma tentativa de logon falha. Se a mensagem de erro incluir a conta **distributor_admin** (Falha de logon para o usuário 'distributor_admin'.), o problema estará relacionado a uma conta usada pela replicação. A replicação cria um servidor remoto, **repl_distributor**, que permite a comunicação entre o Distribuidor e o Publicador. O logon **distributor_admin** é associado a esse servidor remoto e tem uma senha válida.  
  
## <a name="user-action"></a>Ação do usuário  
 Certifique-se de ter especificado uma senha para a conta. Para obter mais informações, consulte [Proteger o Distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
