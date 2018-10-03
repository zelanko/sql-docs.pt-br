---
title: sp_addscriptexec (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords:
- sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42bc6c0c89c5f697eabec38485a70a955ffe456e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722754"
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
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [  **@scriptfile=** ] **'***scriptfile***'**  
 É o caminho completo para o arquivo script SQL. *ScriptFile* está **nvarchar (4000)**, sem padrão.  
  
 [  **@skiperror=** ] **'***skiperror***'**  
 Indica se o Distribution Agent ou Merge Agent devem parar quando um erro é encontrado durante o processamento de script. *SkipError* está **bit**, com um padrão de 0.  
  
 **0** = o agente irá parar.  
  
 **1** = o agente continua o script e ignora o erro.  
  
 [  **@publisher=** ] **'***publisher***'**  
 Especifica um não[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser usado durante a publicação de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addscriptexec** é usado em replicação de mesclagem e de replicação transacional.  
  
 **sp_addscriptexec** não é usado para replicação de instantâneo.  
  
 Para usar **sp_addscriptexec**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço deve ter de leitura e permissões de gravação em que o instantâneo local e permissão de leitura no local onde os scripts são armazenadas.  
  
 O [utilitário sqlcmd](../../tools/sqlcmd-utility.md) é usado para executar o script no assinante, e o script é executado no contexto de segurança usado pelo Distribution Agent ou Merge Agent ao conectar-se ao banco de dados de assinatura. Quando o agente é executado em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [utilitário osql](../../tools/osql-utility.md) é usado em vez de [sqlcmd](../../tools/sqlcmd-utility.md).  
  
 **sp_addscriptexec** é útil para aplicar scripts nos assinantes e usa [sqlcmd](../../tools/sqlcmd-utility.md) para aplicar o conteúdo do script no assinante. Porém, como as configurações de Assinante podem variar, scripts testados antes da postagem no Publicador ainda podem provocar erros em um Assinante. *skiperror* fornece a capacidade de ter o Distribution Agent ou Merge Agent ignore erros e continuar se houver. Use [sqlcmd](../../tools/sqlcmd-utility.md) para testar scripts antes de executar **sp_addscriptexec**.  
  
> [!NOTE]  
>  Erros ignorados continuarão sendo registrados no histórico do Agente para referência.  
  
 Usando o **sp_addscriptexec** para lançar um arquivo de script para publicações usando FTP para entrega de instantâneo só tem suporte para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_addscriptexec**.  
  
## <a name="see-also"></a>Consulte também  
 [Executar Scripts durante a sincronização &#40;programação de Transact-SQL de replicação&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
