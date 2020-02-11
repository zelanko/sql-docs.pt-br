---
title: MSSQLSERVER_601 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9aebe73ac73ee09ed2ba6de9162877d0e70bc7e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62867725"
---
# <a name="mssqlserver_601"></a>MSSQLSERVER_601
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|601|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Não foi possível continuar a verificação com NOLOCK devido ao movimento de dados.|  
  
## <a name="explanation"></a>Explicação  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não pode continuar a execução da consulta porque está tentando ler dados atualizados ou excluídos por outra transação. A consulta está usando ou dicas de bloqueio NOLOCK ou o nível de isolamento da transação READ UNCOMMITTED.  
  
 Geralmente, o acesso aos dados que estão sendo alterados por outra transação é negado devido aos bloqueios dos dados. Porém, a dica de bloqueio NOLOCK e o nível de isolamento da transação READ UNCOMMITTED permitem que uma consulta leia dados bloqueados por outra transação. Isso é chamado de leitura suja, porque você pode ler valores que ainda não estão confirmados e estão sujeitos a mudanças.  
  
## <a name="user-action"></a>Ação do usuário  
 Este erro cancela a consulta. Envie a consulta novamente ou remova a dica de bloqueio NOLOCK.  
  
## <a name="see-also"></a>Consulte Também  
 [MSSQLSERVER_605](mssqlserver-605-database-engine-error.md)   
 [Dicas de tabela &#40;&#41;Transact-SQL](/sql/t-sql/queries/hints-transact-sql-table)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)  
  
  
