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
manager: craigg
ms.openlocfilehash: 9f0853d7db0664e75140c0e5478af19c233a2517
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761717"
---
# <a name="mssqlserver_8689"></a>MSSQLSERVER_8689
    
## <a name="details"></a>Detalhes  
  
|||  
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
 [Dicas de consulta &#40;&#41;Transact-SQL](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guias de plano](../performance/plan-guides.md)  
  
  
