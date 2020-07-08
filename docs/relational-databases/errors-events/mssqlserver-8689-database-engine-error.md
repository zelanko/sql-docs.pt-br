---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 18c8e591f255b57f8cbb935075695fca7bcc3960
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637060"
---
# <a name="mssqlserver_8689"></a>MSSQLSERVER_8689
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|8689|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|USEPLAN_ERR_NO_DB|  
|Texto da mensagem|O banco de dados '%.*ls', especificado na dica USE PLAN, não existe. Especifique um banco de dados existente.|  
  
## <a name="explanation"></a>Explicação  
Um banco de dados especificado na dica USE PLAN não existe.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se todos os bancos de dados que estão especificados na dica USE PLAN existem.  
  
## <a name="see-also"></a>Consulte Também  
[Query Hints &#40;Transact-SQL&#41; [Dicas de consulta (Transact-SQL)]](~/t-sql/queries/hints-transact-sql-query.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
  
