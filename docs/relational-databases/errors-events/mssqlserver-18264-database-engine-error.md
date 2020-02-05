---
title: MSSQLSERVER_18264 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18264 (Database Engine error)
ms.assetid: 3050fc56-2be5-43cf-916b-50a3ac5f89aa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: df0bd7c7093aeb46421fca75c9e9233f2b1f4263
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68137126"
---
# <a name="mssqlserver_18264"></a>MSSQLSERVER_18264
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|Microsoft SQL Server|  
|ID do evento|18264|  
|Origem do Evento|MSSQLENGINE|  
|Componente|SQLEngine|  
|Nome simbólico|STRMIO_DBDUMP|  
|Texto da mensagem|Backup do banco de dados efetuado. Banco de dados: %s, data (hora) da criação: %s(%s), páginas despejadas: %d, primeiro LSN: %s, último LSN: %s, número de dispositivos de despejo: %d, informações sobre o dispositivo: (%s). Essa mensagem é apenas informativa. Não é necessária nenhuma ação do usuário.|  
  
## <a name="explanation"></a>Explicação  
Por padrão, todo backup bem-sucedido adiciona essa mensagem informativa ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você faz backup do log de transações com muita frequência, essas mensagens podem se acumular muito rapidamente, resultando em logs de erros imensos que podem dificultar a localização de outras mensagens.  
  
## <a name="user-action"></a>Ação do usuário  
Você pode suprimir essas entradas de log usando o sinalizador de rastreamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**3226**. Habilitar o sinalizador de rastreamento é útil quando você executa backups de logs com frequência e se nenhum dos seus scripts depende dessas entradas.  
  
Para obter informações sobre como usar sinalizadores de rastreamento, consulte os Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
[Sinalizadores de rastreamento &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
