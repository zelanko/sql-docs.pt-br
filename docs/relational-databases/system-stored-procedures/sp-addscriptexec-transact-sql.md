---
title: sp_addscriptexec (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords:
- sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8e3122de37c27e8372c2aca77f4dde0b267a8d20
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddscriptexec-transact-sql"></a>sp_addscriptexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Posta um script SQL (arquivo .sql ) em todos os Assinantes de uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addscriptexec [ @publication = ] publication  
    [ , [ @scriptfile = ] 'scriptfile' ]  
    [ , [ @skiperror = ] 'skiperror' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@scriptfile=** ] **'***scriptfile***'**  
 É o caminho completo para o arquivo script SQL. *ScriptFile* é **nvarchar (4000)**, sem padrão.  
  
 [  **@skiperror=** ] **'***skiperror***'**  
 Indica se o Distribution Agent ou Merge Agent devem parar quando um erro é encontrado durante o processamento de script. *SkipError* é **bit**, com um padrão de 0.  
  
 **0** = o agente irá parar.  
  
 **1** = o agente continua o script e ignora o erro.  
  
 [  **@publisher=** ] **'***publicador***'**  
 Especifica um não[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado durante a publicação de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_addscriptexec** é usado em replicação de mesclagem e de replicação transacional.  
  
 **sp_addscriptexec** não é usado para replicação de instantâneo.  
  
 Para usar **sp_addscriptexec**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço deve ter de leitura e permissões de gravação em que o instantâneo local e permissão de leitura no local de onde os scripts são armazenadas.  
  
 O [utilitário sqlcmd](../../tools/sqlcmd-utility.md) é usada para executar o script no assinante, e o script é executado no contexto de segurança usado pelo agente de distribuição ou agente de mesclagem ao se conectar ao banco de dados de assinatura. Quando o agente é executado em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [utilitário osql](../../tools/osql-utility.md) é usado em vez de [sqlcmd](../../tools/sqlcmd-utility.md).  
  
 **sp_addscriptexec** é útil para aplicar scripts nos assinantes e usa [sqlcmd](../../tools/sqlcmd-utility.md) para aplicar o conteúdo do script para o assinante. Porém, como as configurações de Assinante podem variar, scripts testados antes da postagem no Publicador ainda podem provocar erros em um Assinante. *skiperror* fornece a capacidade de ter o Distribution Agent ou Merge Agent ignore erros e continue em. Use [sqlcmd](../../tools/sqlcmd-utility.md) para testar scripts antes de executar **sp_addscriptexec**.  
  
> [!NOTE]  
>  Erros ignorados continuarão sendo registrados no histórico do Agente para referência.  
  
 Usando **sp_addscriptexec** para postar um arquivo de script para publicações usando FTP para entrega de instantâneo só tem suporte para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addscriptexec**.  
  
## <a name="see-also"></a>Consulte também  
 [Executar Scripts durante a sincronização &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
