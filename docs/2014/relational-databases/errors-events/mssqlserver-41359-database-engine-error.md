---
title: MSSQLSERVER_41359 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9cfc69b5c7da77f53c6d49d82a70739fb5a7d09c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412415"
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
  
  
