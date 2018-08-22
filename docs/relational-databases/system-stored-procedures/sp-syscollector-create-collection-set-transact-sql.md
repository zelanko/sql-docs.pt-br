---
title: sp_syscollector_create_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_set_TSQL
- sp_syscollector_create_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_create_collection_set
ms.assetid: 69e9ff0f-c409-43fc-89f6-40c3974e972c
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e709e05834ed30701d2944547945ba439b8d418d
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392454"
---
# <a name="spsyscollectorcreatecollectionset-transact-sql"></a>sp_syscollector_create_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um novo conjunto de coleta. Use este procedimento armazenado para criar um conjunto de coleta personalizado para a coleta de dados.  
  
> [!WARNING]  
>  Nos casos em que a conta do Windows configurada como um proxy é um usuário não interativo ou interativo que ainda não fez logon, o diretório de perfil não existirá e a criação do diretório de preparo falhará. Portanto, se você estiver usando uma conta proxy em um controlador de domínio, deverá especificar uma conta interativa que tenha sido usada pelo menos uma vez para assegurar que o diretório de perfil foi criado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_create_collection_set   
      [ @name = ] 'name'  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    , [ [ @schedule_uid = ] 'schedule_uid' ]  
    , [ [ @schedule_name = ] 'schedule_name' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
    , [ @collection_set_id = ] collection_set_id OUTPUT   
    , [ [ @collection_set_uid = ] 'collection_set_uid' OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name =** ] '*nome*'  
 É o nome do conjunto de coleta. *nome da* está **sysname** e não pode ser uma cadeia de caracteres vazia ou nula.  
  
 *nome* deve ser exclusivo. Para obter uma lista dos nomes dos conjuntos de coleta atuais, consulte a exibição de sistema syscollector_collection_sets.  
  
 [  **@target =** ] '*destino*'  
 Reservado para uso futuro. *nome da* está **nvarchar (128)** com um valor padrão de NULL.  
  
 [  **@collection_mode =** ] *collection_mode*  
 Especifica a maneira pela qual os dados são coletados e armazenados. *collection_mode* está **smallint** e pode ter um dos seguintes valores:  
  
 0 - Modo de cache. A coleta e o carregamento de dados estão em agendas separadas. Especifique o modo cache para a coleta contínua.  
  
 1 - Modo não armazenado em cache. A coleção e o carregamento de dados estão na mesma agenda. Especifique o modo não armazenado em cache para a coleta ad hoc ou de instantâneo.  
  
 O valor padrão para *collection_mode* é 0. Quando *collection_mode* é 0, o *schedule_uid* ou *schedule_name* deve ser especificado.  
  
 [  **@days_until_expiration =** ] *days_until_expiration*  
 É o número de dias durante os quais os dados coletados são salvos no data warehouse de gerenciamento. *days_until_expiration* está **smallint** com um valor padrão de 730 (dois anos). *days_until_expiration* deve ser 0 ou um número inteiro positivo.  
  
 [  **@proxy_id =** ] *proxy_id*  
 É o identificador exclusivo de uma conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. *proxy_id* está **int** com um valor padrão de NULL. Se especificado, *proxy_name* deve ser NULL. Para obter *proxy_id*, consultar a tabela de sistema sysproxies. A função de banco de dados fixa dc_admin deve ter permissão para acessar o proxy. Para obter mais informações, consulte [criar um Proxy do SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
 [  **@proxy_name =** ] '*proxy_name*'  
 É o nome da conta proxy. *proxy_name* está **sysname** com um valor padrão de NULL. Se especificado, *proxy_id* deve ser NULL. Para obter *proxy_name*, consultar a tabela de sistema sysproxies.  
  
 [  **@schedule_uid =** ] '*schedule_uid*'  
 É o GUID que aponta para uma agenda. *schedule_uid* está **uniqueidentifier** com um valor padrão de NULL. Se especificado, *schedule_name* deve ser NULL. Para obter *schedule_uid*, consultar a tabela de sistema sysschedules.  
  
 Quando *collection_mode* é definido como 0, *schedule_uid* ou *schedule_name* deve ser especificado. Quando *collection_mode* é definido como 1, *schedule_uid* ou *schedule_name* será ignorado se especificado.  
  
 [  **@schedule_name =** ] '*schedule_name*'  
 É o nome da agenda. *schedule_name* está **sysname** com um valor padrão de NULL. Se especificado, *schedule_uid* deve ser NULL. Para obter *schedule_name*, consultar a tabela de sistema sysschedules.  
  
 [  **@logging_level =** ] *logging_level*  
 É o nível de registro em log. *logging_level* está **smallint** com um dos seguintes valores:  
  
 0 - informações de execução de log e eventos [!INCLUDE[ssIS](../../includes/ssis-md.md)] que monitoram:  
  
-   Iniciando/interrompendo conjuntos de coleta  
  
-   Iniciando/interrompendo pacotes  
  
-   Informações de erro  
  
 1 - log de nível 0 e:  
  
-   Estatísticas de execução  
  
-   Progresso da coleta em execução contínua  
  
-   Eventos de advertência do [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2 - log de nível 1 e informações de evento detalhadas do [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 O valor padrão para *logging_level* é 1.  
  
 [  **@description =** ] '*descrição*'  
 É a descrição do conjunto de coleta. *Descrição* está **nvarchar (4000)** com um valor padrão de NULL.  
  
 [  **@collection_set_id =** ] *collection_set_id*  
 É o identificador local exclusivo do conjunto de coleta. *collection_set_id* está **int** com a saída e é necessária.  
  
 [  **@collection_set_uid =** ] '*collection_set_uid*'  
 É o GUID do conjunto de coleta. *collection_set_uid* está **uniqueidentifier** com OUTPUT com um valor padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 sp_syscollector_create_collection_set deve ser executado no contexto do banco de dados de sistema msdb.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa dc_admin (com a permissão EXECUTE) para executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-collection-set-by-using-default-values"></a>A. Criando um conjunto de coleta com o uso de valores padrão  
 O exemplo a seguir cria um conjunto de coleta especificando apenas os parâmetros necessários. `@collection_mode` não é necessário, mas o modo de coleta padrão (armazenado em cache) requer a especificação de uma ID de agenda ou nome de agenda.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
EXECUTE dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 1',  
    @description = N'This is a test collection set that runs in non-cached mode.',  
    @collection_mode = 1,  
    @collection_set_id = @collection_set_id OUTPUT;  
GO  
```  
  
### <a name="b-creating-a-collection-set-by-using-specified-values"></a>B. Criando um conjunto de coleta usando os valores especificados  
 O exemplo a seguir cria um conjunto de coleta especificando valores para muitos dos parâmetros.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier;  
SET @collection_set_uid = NEWID();  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 2',  
    @collection_mode = 0,  
    @days_until_expiration = 365,  
    @description = N'This is a test collection set that runs in cached mode.',  
    @logging_level = 2,  
    @schedule_name = N'CollectorSchedule_Every_30min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)   
 [Criar um conjunto de coleta personalizado que usa o tipo de coletor de Consultas T-SQL genérico &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
