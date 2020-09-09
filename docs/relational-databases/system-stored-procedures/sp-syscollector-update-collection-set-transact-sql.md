---
description: sp_syscollector_update_collection_set (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fd55d65173d190d1c28708bfae46b10eaa0030a4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534828"
---
# <a name="sp_syscollector_update_collection_set-transact-sql"></a>sp_syscollector_update_collection_set (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Usado para modificar as propriedades de um conjunto de coleta definido pelo usuário ou para renomear um desses conjuntos.  
  
> [!WARNING]  
>  Nos casos em que a conta do Windows configurada como um proxy é um usuário não interativo ou interativo que ainda não fez logon, o diretório de perfil não existirá e a criação do diretório de preparo falhará. Portanto, se você estiver usando uma conta proxy em um controlador de domínio, deverá especificar uma conta interativa que tenha sido usada pelo menos uma vez para assegurar que o diretório de perfil foi criado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @collection_set_id = ] collection_set_id` É o identificador local exclusivo para o conjunto de coleta. *collection_set_id* é **int** e deve ter um valor se *Name* for NULL.  
  
`[ @name = ] 'name'` É o nome do conjunto de coleta. o *nome* é **sysname** e deve ter um valor se *collection_set_id* for NULL.  
  
`[ @new_name = ] 'new_name'` É o novo nome para o conjunto de coleta. *new_name* é **sysname**e, se usado, não pode ser uma cadeia de caracteres vazia. *new_name* deve ser exclusivo. Para obter uma lista dos nomes dos conjuntos de coleta atuais, consulte a exibição de sistema syscollector_collection_sets.  
  
`[ @target = ] 'target'` Reservado para uso futuro.  
  
`[ @collection_mode = ] collection_mode` É o tipo de coleção de dados a ser usado. *collection_mode* é **smallint** e pode ter um dos seguintes valores:  
  
 0 - Modo de cache. A coleta e o carregamento de dados estão em agendas separadas. Especifique o modo cache para a coleta contínua.  
  
 1 - Modo não armazenado em cache. A coleção e o carregamento de dados estão na mesma agenda. Especifique o modo não armazenado em cache para a coleta ad hoc ou de instantâneo.  
  
 Se a alteração do modo não armazenado em cache para o modo em cache (0), você também deverá especificar *schedule_uid* ou *schedule_name*.  
  
`[ @days_until_expiration = ] days_until_expiration` É o número de dias que os dados coletados são salvos no data warehouse de gerenciamento. *days_until_expiration* é **smallint**. *days_until_expiration* deve ser 0 ou um número inteiro positivo.  
  
`[ @proxy_id = ] proxy_id` É o identificador exclusivo de uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta proxy do Agent. *proxy_id* é **int**.  
  
`[ @proxy_name = ] 'proxy_name'` É o nome do proxy. *proxy_name* é **sysname** e permite valor nulo.  
  
`[ @schedule_uid = ] 'schedule_uid'` É o GUID que aponta para uma agenda. *schedule_uid* é **uniqueidentifier**.  
  
 Para obter *schedule_uid*, consulte a tabela do sistema sysschedules.  
  
 Quando *collection_mode* é definido como 0, *schedule_uid* ou *schedule_name* deve ser especificado. Quando *collection_mode* for definido como 1, *schedule_uid* ou *schedule_name* será ignorado se for especificado.  
  
`[ @schedule_name = ] 'schedule_name'` É o nome da agenda. *schedule_name* é **sysname** e permite valor nulo. Se especificado, *schedule_uid* deve ser nulo. Para obter *schedule_name*, consulte a tabela do sistema sysschedules.  
  
`[ @logging_level = ] logging_level` É o nível de log. *logging_level* é **smallint** com um dos seguintes valores:  
  
 0 - informações de execução de log e eventos do [!INCLUDE[ssIS](../../includes/ssis-md.md)] que monitoram:  
  
-   Iniciando/interrompendo conjuntos de coleta  
  
-   Iniciando/interrompendo pacotes  
  
-   Informações de erro  
  
 registro em log de 1 nível-0 e:  
  
-   Estatísticas de execução  
  
-   Progresso da coleta em execução contínua  
  
-   Eventos de advertência do [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2 - log de nível 1 e informações de evento detalhadas do [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 O valor padrão para *logging_level* é 1.  
  
`[ @description = ] 'description'` É a descrição do conjunto de coleta. a *Descrição* é **nvarchar (4000)**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_syscollector_update_collection_set deve ser executado no contexto do banco de dados do sistema msdb.  
  
 O *collection_set_id* ou o *nome* deve ter um valor, ambos não podem ser nulos. Para obter esses valores, consulte a exibição de sistema syscollector_collection_sets.  
  
 Se o conjunto de coleta estiver em execução, você só poderá atualizar *schedule_uid* e *Descrição*. Para parar o conjunto de coleta, use [sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento, a associação na função de banco de dados fixa dc_admin ou dc_operator (com a permissão EXECUTE) é necessária. Embora dc_operator possa executar esse procedimento armazenado, membros desta função estão limitados nas propriedades que eles podem alterar. As propriedades a seguir só podem ser alteradas através de dc_admin:  
  
-   @new_name  
  
-   @target  
  
-   @proxy_id  
  
-   @description  
  
-   @collection_mode  
  
-   @days_until_expiration  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-renaming-a-collection-set"></a>a. Renomeando um conjunto de coleta  
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
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)   
 [&#41;&#40;Transact-SQL de syscollector_collection_sets ](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)   
 [ Agendas dedbo.sys&#40;&#41;de Transact-SQL ](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
