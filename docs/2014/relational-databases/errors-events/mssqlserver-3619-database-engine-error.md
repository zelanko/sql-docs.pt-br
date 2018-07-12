---
title: MSSQLSERVER_3619 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 963267a102c16b57860d5859a6600a34781ca2c8
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413795"
---
# <a name="mssqlserver3619"></a>MSSQLSERVER_3619
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3619|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SYS_NOLOG|  
|Texto da mensagem|Não foi possível gravar um registro de ponto de verificação na ID do banco de dados %d porque não há espaço no log. Entre em contato com o administrador de banco de dados para truncar o log ou aloque mais espaço para os arquivos de log de banco de dados.|  
  
## <a name="explanation"></a>Explicação  
 O log de transações tem espaço em disco insuficiente.  
  
## <a name="user-action"></a>Ação do usuário  
 Trunque o log para liberar espaço ou aloque mais espaço para o log. Para obter mais informações, consulte “Solucionando problemas em um log de transação completa (erro 9002)” nos Manuais Online do SQL Server.  
  
  
