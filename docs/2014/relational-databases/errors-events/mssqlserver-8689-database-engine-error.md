---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85e33cc4231fb4ebf6a3058a20a0257e81a07b6a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421435"
---
# <a name="mssqlserver8689"></a>MSSQLSERVER_8689
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|8689|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|USEPLAN_ERR_NO_DB|  
|Texto da mensagem|O banco de dados '%.*ls', especificado na dica USE PLAN, não existe. Especifique um banco de dados existente.|  
  
## <a name="explanation"></a>Explicação  
 Um banco de dados especificado na dica USE PLAN não existe.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se todos os bancos de dados que estão especificados na dica USE PLAN existem.  
  
## <a name="see-also"></a>Consulte também  
 [Dicas de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guias de plano](../performance/plan-guides.md)  
  
  
