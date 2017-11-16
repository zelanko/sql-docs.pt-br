---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 117bc8fb03796a14176727baf66d3ea468becddd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver4064"></a>MSSQLSERVER_4064
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|4064|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DB_UFAIL_FATAL|  
|Texto da mensagem|Não é possível abrir o banco de dados padrão do usuário. Falha no logon.|  
  
## <a name="explanation"></a>Explicação  
O logon do SQL Server não pôde se conectar devido a um problema com o banco de dados padrão. O próprio banco de dados é inválido ou o logon não tem a permissão CONNECT no banco de dados.  
  
## <a name="user-action"></a>Ação do usuário  
Use ALTER LOGIN para alterar o banco de dados padrão do logon. Conceda a permissão CONNECT para o logon.  
  
