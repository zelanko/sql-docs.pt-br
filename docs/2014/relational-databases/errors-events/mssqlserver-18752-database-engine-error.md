---
title: MSSQLSERVER_18752 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c61d4634fa4f82ffc70748ff185ff8294f50063f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421895"
---
# <a name="mssqlserver18752"></a>MSSQLSERVER_18752
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|18752|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REPL_INUSE|  
|Texto da mensagem|Somente um Agente de Leitor de Log ou um procedimento relacionado ao log (sp_repldone, sp_replcmds e sp_replshowcmds) pode se conectar ao banco de dados de cada vez. Se você tiver executado um procedimento relacionado ao log, descarte a conexão através da qual o procedimento foi executado ou execute sp_replflush por essa conexão antes de iniciar o Agente de Leitor de Log ou de executar outro procedimento relacionado ao log.|  
  
## <a name="explanation"></a>Explicação  
 Somente um Log Reader Agent ou um procedimento relacionado ao log pode se conectar ao banco de dados de cada vez.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se nenhum outro leitor de log está sendo executado no mesmo banco de dados de publicação e se nenhuma outra conexão ativa executou sp_replcmds/sp_repltrans/sp_repldone anteriormente sem executar sp_replflush em seguida ou desconectar.  
  
  
