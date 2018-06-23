---
title: MSSQLSERVER_3619 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6dc81452b043cc99a02052ccd9fe94a8b6d2a8e9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012254"
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
  
  