---
title: MSSQLSERVER_15517 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 06e21c4e075dbf092e4ae3731b38806390ea2a47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007046"
---
# <a name="mssqlserver15517"></a>MSSQLSERVER_15517
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|15517|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CANNOTEXECUTEASUSER|  
|Texto da mensagem|Não é possível executar como banco de dados de entidade, pois a entidade “*principal*” não existe, esse tipo de entidade não pode ser representada ou você não tem permissão para isso.|  
  
## <a name="user-action"></a>Ação do usuário  
 Use o nome de uma entidade existente ou obtenha a permissão IMPERSONATE nessa entidade.  
  
 15517 também pode ocorrer depois da execução de um anexo e a restauração de um banco de dados por alguém que não seja o proprietário original do banco de dados. Para resolver esse erro, altere o db_owner para um logon no servidor, executando o seguinte comando:  
  
```  
ALTER AUTHORIZATION ON DATABASE:: DBName TO [NewLogin]  
```  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  