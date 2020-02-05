---
title: MSSQLSERVER_601 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3aa0ba350e4c1e7e56a545e26793be193b4b5a2d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67903919"
---
# <a name="mssqlserver_601"></a>MSSQLSERVER_601
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
[MSSQLSERVER_605](../../relational-databases/errors-events/mssqlserver-605-database-engine-error.md)  
[Dicas de tabela &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-table.md)  
[SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](~/t-sql/statements/set-transaction-isolation-level-transact-sql.md)  
  
