---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ae02cc0d9e5661f4069884c22bf6eea0697bd2d7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031746"
---
# <a name="mssqlserver_8443"></a>MSSQLSERVER_8443
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|8443|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SB_DIALOG_WO_CONV_GROUP|  
|Texto da mensagem|A conversa com a ID '%.*ls' e o iniciador %d referencia um grupo de conversa ausente '%.\*ls'. Execute DBCC CHECKDB para analisar e reparar o banco de dados.|  
  
## <a name="explanation"></a>Explicação  
 A camada de metadados retornou NULL para o grupo de conversa. O banco de dados foi corrompido de algum modo. Uma possível origem da corrupção é um erro de disco.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute DBCC CHECKDB no modo de correção para deixar novamente o banco de dados em um estado consistente. É possível excluir mensagens, se necessário, para restaurar a consistência. Investigue os logs de erros do sistema para saber se o erro foi causado por outra falha no sistema.  
  
  
