---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f66fec380ebd70a4dcbba445f9e0678fb33290eb
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553118"
---
# <a name="mssqlserver_8689"></a>MSSQLSERVER_8689
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
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
 [Dicas de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guias de plano](../performance/plan-guides.md)  
  
  
