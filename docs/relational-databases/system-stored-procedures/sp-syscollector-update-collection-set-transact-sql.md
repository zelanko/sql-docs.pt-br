---
title: sp_syscollector_update_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_set_TSQL
- sp_syscollector_update_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 2dccc3cd-0e93-4e3e-a4e5-8fe89b31bd63
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7d77ec36f36260226a78136b46656b1e2e8187e5
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527168"
---
# <a name="spsyscollectorupdatecollectionset-transact-sql"></a>sp_syscollector_update_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado para modificar as propriedades de um conjunto de coleta definido pelo usuário ou para renomear um desses conjuntos.  
  
> [!WARNING]  
>  Nos casos em que a conta do Windows configurada como um proxy é um usuário não interativo ou interativo que ainda não fez logon, o diretório de perfil não existirá e a criação do diretório de preparo falhará. Portanto, se você estiver usando uma conta proxy em um controlador de domínio, deverá especificar uma conta interativa que tenha sido usada pelo menos uma vez para assegurar que o diretório de perfil foi criado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_update_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    ,[ [ @schedule_uid = ] 'schedule_uid' ]  
    ,[ [ @schedule_name = ] 'schedule_uid' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @collection_set_id = ] collection_set_id` É o identificador local exclusivo para o conjunto de coleta. *collection_set_id* está **int** e deve ter um valor se *nome* é NULL.  
  
`[ @name = ] 'name'` É o nome do conjunto de coleta. *nome da* está **sysname** e deve ter um valor se *collection_set_id* é NULL.  
  
`[ @new_name = ] 'new_name'` É o novo nome para o conjunto de coleta. *new_name* está **sysname**, e se usado, não pode ser uma cadeia de caracteres vazia. *new_name* deve ser exclusivo. Para obter uma lista dos nomes dos conjuntos de coleta atuais, consulte a exibição de sistema syscollector_collection_sets.  
  
`[ @target = ] 'target'` Reservado para uso futuro.  
  
`[ @collection_mode = ] collection_mode` É o tipo de coleta de dados para usar. *collection_mode* está **smallint** e pode ter um dos seguintes valores:  
  
 0 - Modo de cache. A coleta e o carregamento de dados estão em agendas separadas. Especifique o modo cache para a coleta contínua.  
  
 1 - Modo não armazenado em cache. A coleção e o carregamento de dados estão na mesma agenda. Especifique o modo não armazenado em cache para a coleta ad hoc ou de instantâneo.  
  
 Se a alteração do modo não armazenado em cache para o modo de cache (0), você deve também especificar *schedule_uid* ou *schedule_name*.  
  
`[ @days_until_expiration = ] days_until_expiration` É o número de dias que os dados coletados são salvos no data warehouse de gerenciamento. *days_until_expiration* está **smallint**. *days_until_expiration* deve ser 0 ou um número inteiro positivo.  
  
`[ @proxy_id = ] proxy_id` É o identificador exclusivo para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta proxy do agente. *proxy_id* está **int**.  
  
`[ @proxy_name = ] 'proxy_name'` É o nome do proxy. *proxy_name* está **sysname** e é anulável.  
  
`[ @schedule_uid = ] 'schedule_uid'` É o GUID que aponta para um agendamento. *schedule_uid* está **uniqueidentifier**.  
  
 Para obter *schedule_uid*, consultar a tabela de sistema sysschedules.  
  
 Quando *collection_mode* é definido como 0, *schedule_uid* ou *schedule_name* deve ser especificado. Quando *collection_mode* é definido como 1, *schedule_uid* ou *schedule_name* será ignorado se especificado.  
  
`[ @schedule_name = ] 'schedule_name'` É o nome da agenda. *schedule_name* está **sysname** e é anulável. Se especificado, *schedule_uid* deve ser NULL. Para obter *schedule_name*, consultar a tabela de sistema sysschedules.  
  
`[ @logging_level = ] logging_level` É o nível de log. *logging_level* está **smallint** com um dos seguintes valores:  
  
 0 - informações de execução de log e eventos do [!INCLUDE[ssIS](../../includes/ssis-md.md)] que monitoram:  
  
-   Iniciando/interrompendo conjuntos de coleta  
  
-   Iniciando/interrompendo pacotes  
  
-   Informações de erro  
  
 1 - log de nível 0 e:  
  
-   Estatísticas de execução  
  
-   Progresso da coleta em execução contínua  
  
-   Eventos de advertência do [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2 - log de nível 1 e informações de evento detalhadas do [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 O valor padrão para *logging_level* é 1.  
  
`[ @description = ] 'description'` É a descrição do conjunto de coleta. *Descrição* está **nvarchar (4000)**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_syscollector_update_collection_set deve ser executado no contexto do banco de dados do sistema msdb.  
  
 Qualquer um dos *collection_set_id* ou *nome* deve ter um valor, ambos não podem ser NULL. Para obter esses valores, consulte a exibição de sistema syscollector_collection_sets.  
  
 Se o conjunto de coleta está em execução, você pode atualizar apenas *schedule_uid* e *descrição*. Para interromper o conjunto de coleta, use [sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento, a associação na função de banco de dados fixa dc_admin ou dc_operator (com a permissão EXECUTE) é necessária. Embora dc_operator possa executar esse procedimento armazenado, membros desta função estão limitados nas propriedades que eles podem alterar. As propriedades a seguir só podem ser alteradas através de dc_admin:  
  
-   @new_name  
  
-   @target  
  
-   @proxy_id  
  
-   @description  
  
-   @collection_mode  
  
-   @days_until_expiration  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-renaming-a-collection-set"></a>A. Renomeando um conjunto de coleta  
 O exemplo a seguir renomeia um conjunto de coleta definido pelo usuário.  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 1',  
@new_name = N'Collection set test 1 in cached mode';  
GO  
```  
  
### <a name="b-changing-the-collection-mode-from-non-cached-to-cached"></a>B. Alterando o modo de coleta de não armazenado em cache para cache  
 O exemplo a seguir altera o modo de coleta de modo não armazenado em cache para cache. Essa alteração exige que você especifique uma ID ou um nome de agenda.  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Collection set test 1 in cached mode',  
@collection_mode = 0,  
@schedule_uid = 'C7022AF3-51B8-4011-B159-64C47C88FF70';  
-- alternatively, use @schedule_name.  
-- @schedule_name = N'CollectorSchedule_Every_15min;  
GO  
```  
  
### <a name="c-changing-other-collection-set-parameters"></a>C. Alterando outros parâmetros do conjunto de coleta  
 O exemplo a seguir atualiza várias propriedades do conjunto de coleta denominado "Teste do conjunto de coleta simples 2'.  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 2',  
@collection_mode = 1,  
@days_until_expiration = 5,  
@description = N'This is a test collection set that runs in noncached mode.',  
@logging_level = 0;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)   
 [dbo.sysschedules &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
