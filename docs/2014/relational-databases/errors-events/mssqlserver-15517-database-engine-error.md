---
title: MSSQLSERVER_15517 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ebbc87a299cb55658c7a8506fa4a63a2e2d1d215
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426465"
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
  
  
