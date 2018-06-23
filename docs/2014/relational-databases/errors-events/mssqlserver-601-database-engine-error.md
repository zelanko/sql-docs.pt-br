---
title: MSSQLSERVER_601 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0cb9c16487408f5be8598a7fee3c748efd8591e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119341"
---
# <a name="mssqlserver601"></a>MSSQLSERVER_601
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|601|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Não foi possível continuar a verificação com NOLOCK devido ao movimento de dados.|  
  
## <a name="explanation"></a>Explicação  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não pode continuar a execução da consulta porque está tentando ler dados atualizados ou excluídos por outra transação. A consulta está usando ou dicas de bloqueio NOLOCK ou o nível de isolamento da transação READ UNCOMMITTED.  
  
 Geralmente, o acesso aos dados que estão sendo alterados por outra transação é negado devido aos bloqueios dos dados. Porém, a dica de bloqueio NOLOCK e o nível de isolamento da transação READ UNCOMMITTED permitem que uma consulta leia dados bloqueados por outra transação. Isso é chamado de leitura suja, porque você pode ler valores que ainda não estão confirmados e estão sujeitos a mudanças.  
  
## <a name="user-action"></a>Ação do usuário  
 Este erro cancela a consulta. Envie a consulta novamente ou remova a dica de bloqueio NOLOCK.  
  
## <a name="see-also"></a>Consulte também  
 [MSSQLSERVER_605](mssqlserver-605-database-engine-error.md)   
 [Dicas de tabela &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)  
  
  
