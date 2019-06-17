---
title: MSSQL_ENG018456 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018456 error
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff5d5a983bda1dd5efa68c282373f37ab8fda571
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63055646"
---
# <a name="mssqleng018456"></a>MSSQL_ENG018456
    
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
 Certifique-se de ter especificado uma senha para a conta. Para obter mais informações, consulte [Proteger o Distribuidor](security/secure-the-distributor.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
