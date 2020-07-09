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
ms.openlocfilehash: a1c516a70788d16fc4c80e5ed0b9f0277eccf020
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728353"
---
# <a name="mssqlserver_601"></a>MSSQLSERVER_601
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
  
