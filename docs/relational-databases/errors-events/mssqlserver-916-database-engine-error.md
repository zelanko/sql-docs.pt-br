---
title: MSSQLSERVER_916 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 916 (Database Engine error)
ms.assetid: 73eb6581-99fe-49a5-9b42-e239d7ffe27f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c35337a50a964b2af9455e53592d8c45c7371307
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver916"></a>MSSQLSERVER_916
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|916|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NOTUSER|  
|Texto da mensagem|A entidade de segurança do servidor "%.*ls" não é capaz de acessar o banco de dados "%.\*ls" no contexto de segurança atual.|  
  
## <a name="explanation"></a>Explicação  
O logon não tem permissões suficientes para conectar-se ao banco de dados nomeado. Os logons que podem conectar-se a essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas que não têm permissões específicas em um banco de dados, recebem as permissões do usuário convidado. Esta é uma medida de segurança para evitar que usuários em um banco de dados se conectem a outros bancos de dados em que não têm privilégios. Esta mensagem de erro pode ocorrer quando o usuário convidado não tem permissão CONNECT para o banco de dados nomeado e a propriedade confiável não está definida. Essa mensagem de erro poderá ser exibida quando o usuário convidado não tiver a permissão CONNECT para o banco de dados nomeado.  
  
Quando a permissão CONNECT para o banco de dados msdb for negada ou revogada, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] poderá receber esse erro quando o Pesquisador de Objetos tentar mostrar o status do gerenciamento baseado em políticas de cada banco de dados. O Pesquisador de Objetos usa as permissões do logon atual para consultar o banco de dados msdb quanto a essas informações, o que causa o erro. A seguinte mensagem de erro também ocorre:  
  
Falha ao recuperar dados para esta solicitação. (Microsoft.SqlServer.Management.Sdk.Sfc)  
  
## <a name="user-action"></a>Ação do usuário  
  
> [!WARNING]  
> Para evitar esta medida de segurança, verifique se há uma compreensão clara sobre a autenticação de usuários em diversos bancos de dados. Os métodos a seguir talvez permitam que usuários tenham permissões em um banco de dados para se conectarem a outros bancos de dados que podem expor os dados a um usuário mal-intencionado. Quando os bancos de dados independentes são habilitados, as etapas a seguir podem permitir proprietários de banco de dados em um banco de dados para conceder acesso a outro banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Você pode se conectar ao banco de dados de uma das seguintes maneiras:  
  
-   Concedendo ao logon específico acesso ao banco de dados nomeado. O exemplo a seguir concede ao logon `Adventure-Works\Larry` acesso ao banco de dados `msdb`.  
  
    USE msdb ;  
  
    GO  
  
    GRANT CONNECT TO [Adventure-Works\Larry] ;  
  
-   Concedendo a permissão CONNECT ao banco de dados nomeado na mensagem de erro para o usuário convidado. O exemplo a seguir concede a permissão `CONNECT` ao banco de dados `msdb` para o usuário `guest`.  
  
    USE msdb ;  
  
    GO  
  
    GRANT CONNECT TO guest ;  
  
-   Habilite a propriedade TRUSTWORTHY no banco de dados que tem o usuário autenticado.  
  
    `ALTER DATABASE AdventureWorks SET TRUSTWORTHY ON;`  
  
