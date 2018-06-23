---
title: MSSQLSERVER_41359 | Microsoft Docs
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
- 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6fc668ebab849134cc7e6fb4099c03588f1ad1e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120155"
---
# <a name="mssqlserver41359"></a>MSSQLSERVER_41359
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41359|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQL_READ_COMMITTED_SNAPSHOT_NOT_SUPPORTED|  
|Texto da mensagem|Uma consulta que acessa as tabelas com otimização de memória usando o nível de isolamento READ COMMITTED não pode acessar as tabelas baseadas em disco quando a opção READ_COMMITTED_SNAPSHOT do banco de dados é definida como ON. Forneça um nível de isolamento com suporte para a tabela com otimização de memória usando uma dica de tabela, como WITH (SNAPSHOT).|  
  
## <a name="explanation"></a>Explicação  
 O banco de dados com READ_COMMITTED_SNAPSHOT=ON não oferece suporte a transações que acessam tabelas com otimização de memória e tabelas baseadas em disco.  
  
## <a name="user-action"></a>Ação do usuário  
 Defina READ_COMMITTED_SNAPSHOT como OFF ou forneça um nível de isolamento com suporte para a tabela com otimização de memória usando uma dica no nível de tabela, como WITH (SNAPSHOT). Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  