---
title: sp_addscriptexec (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords:
- sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 145afa1da7ae19e480588ecbea28c389350de480
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716398"
---
# <a name="sp_addscriptexec-transact-sql"></a>sp_addscriptexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Posta um script SQL (arquivo .sql ) em todos os Assinantes de uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addscriptexec [ @publication = ] publication  
    [ , [ @scriptfile = ] 'scriptfile' ]  
    [ , [ @skiperror = ] 'skiperror' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @scriptfile = ] 'scriptfile'`É o caminho completo para o arquivo de script SQL. *scriptfile* é **nvarchar (4000)**, sem padrão.  
  
`[ @skiperror = ] 'skiperror'`Indica se o Agente de Distribuição ou Agente de Mesclagem deve parar quando um erro é encontrado durante o processamento do script. *Skiperror* é **bit**, com um padrão de 0.  
  
 **0** = o agente será interrompido.  
  
 **1** = o agente continua o script e ignora o erro.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado ao publicar a partir de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addscriptexec** é usado na replicação transacional e na replicação de mesclagem.  
  
 **sp_addscriptexec** não é usado para replicação de instantâneo.  
  
 Para usar **sp_addscriptexec**, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço deve ter permissões de leitura e gravação no local do instantâneo e permissões de leitura no local onde os scripts são armazenados.  
  
 O [utilitário sqlcmd](../../tools/sqlcmd-utility.md) é usado para executar o script no Assinante, e o script é executado no contexto de segurança usado pelo Agente de Distribuição ou agente de mesclagem ao se conectar ao banco de dados de assinatura. Quando o agente é executado em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o [utilitário osql](../../tools/osql-utility.md) é usado em vez de [sqlcmd](../../tools/sqlcmd-utility.md).  
  
 **sp_addscriptexec** é útil na aplicação de scripts aos assinantes e usa o [sqlcmd](../../tools/sqlcmd-utility.md) para aplicar o conteúdo do script ao Assinante. Porém, como as configurações de Assinante podem variar, scripts testados antes da postagem no Publicador ainda podem provocar erros em um Assinante. o *skiperror* fornece a capacidade de ter o Agente de Distribuição ou agente de mesclagem ignorar erros e continuar. Use o [sqlcmd](../../tools/sqlcmd-utility.md) para testar scripts antes de executar o **sp_addscriptexec**.  
  
> [!NOTE]  
>  Erros ignorados continuarão sendo registrados no histórico do Agente para referência.  
  
 O uso de **sp_addscriptexec** para postar um arquivo de script para publicações usando o FTP para entrega de instantâneo só tem suporte para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addscriptexec**.  
  
## <a name="see-also"></a>Consulte Também  
 [Executar scripts durante a sincronização &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
