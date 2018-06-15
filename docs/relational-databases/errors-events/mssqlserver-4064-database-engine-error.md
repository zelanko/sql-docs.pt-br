---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c58d5a054999da21c3b2850e529a067df0edfb22
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34318757"
---
# <a name="mssqlserver4064"></a>MSSQLSERVER_4064
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
