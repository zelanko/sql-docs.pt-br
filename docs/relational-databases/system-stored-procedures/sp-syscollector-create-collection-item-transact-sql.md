---
title: sp_syscollector_create_collection_item (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_item
- sp_syscollector_create_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collection_item
- data collector [SQL Server], stored procedures
ms.assetid: 60dacf13-ca12-4844-b417-0bc0a8bf0ddb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1e155fb51bd5f78a3c4a639e9233746131ddf6f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004150"
---
# <a name="spsyscollectorcreatecollectionitem-transact-sql"></a>sp_syscollector_create_collection_item (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um item de coleta em um conjunto de coleta definido pelo usuário. Um item de coleta define os dados a serem coletados e a frequência com a qual esses dados são coletados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_create_collection_item   
      [ @collection_set_id = ] collection_set_id   
    , [ @collector_type_uid = ] 'collector_type_uid'  
    , [ @name = ] 'name'   
    , [ [ @frequency = ] frequency ]  
    , [ @parameters = ] 'parameters'  
    , [ @collection_item_id = ] collection_item_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collection_set_id = ] *collection_set_id*  
 É o identificador local exclusivo do conjunto de coleta. *collection_set_id* está **int**.  
  
 [ @collector_type_uid = ] '*collector_type_uid*'  
 É o GUID que identifica o tipo de coletor a ser usado para este item *collector_type_uid* é **uniqueidentifier** sem nenhum valor padrão... Para obter uma lista dos tipos de coletores, consulte a exibição de sistema syscollector_collector_types.  
  
 [ @name = ] '*name*'  
 É o nome do item de coleta. *nome da* está **sysname** e não pode ser uma cadeia de caracteres vazia ou nula.  
  
 *nome* deve ser exclusivo. Para obter uma lista dos nomes dos itens de coleta atuais, consulte a exibição de sistema syscollector_collection_items.  
  
 [ @frequency =] *frequência*  
 É usado para especificar a frequência (em segundos) em que os dados são coletados por esse item de coleta. *frequência* está **int**, com um padrão de 5. O valor mínimo que pode ser especificado é de 5 segundos.  
  
 Se o conjunto de coleta estiver definido para o modo não armazenado em cache, a frequência será ignorada, pois esse modo faz com que a coleta e o carregamento dos dados ocorram conforme a agenda especificada para o conjunto de coleta. Para exibir o modo de coleta do conjunto de coleta, consulte o [syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md) exibição do sistema.  
  
 [ @parameters = ] '*parameters*'  
 Os parâmetros de entrada do tipo de coletor. *parâmetros* está **xml** com um padrão NULL. O *parâmetros* esquema deve corresponder ao esquema de parâmetros do tipo de coletor.  
  
 [ @collection_item_id = ] *collection_item_id*  
 É o identificador exclusivo que identifica o item do conjunto de coleta. *collection_item_id* está **int** e tem OUTPUT.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_syscollector_create_collection_item deve ser executado no contexto do banco de dados do sistema msdb.  
  
 O conjunto de coleta para o qual o item de coleta está sendo adicionado deve ser interrompido antes da criação do item de coleta. Os itens de coleta não podem ser e adicionados aos conjuntos de coleta do sistema.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa dc_admin (com a permissão EXECUTE) para executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um item de coleta baseado no tipo de coleta `Generic T-SQL Query Collector Type` e o adiciona ao conjunto de coleta denominado `Simple collection set test 2`. Para criar a coleção especificada definida, execute o exemplo B no [sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
```  
USE msdb;  
GO  
DECLARE @collection_item_id int;  
DECLARE @collection_set_id int = (SELECT collection_set_id   
                                  FROM syscollector_collection_sets  
                                  WHERE name = N'Simple collection set test 2');  
DECLARE @collector_type_uid uniqueidentifier =   
    (SELECT collector_type_uid  
     FROM syscollector_collector_types  
     WHERE name = N'Generic T-SQL Query Collector Type');  
DECLARE @params xml =   
    CONVERT(xml, N'\<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
                <Value>SELECT * FROM sys.objects</Value>  
                <OutputTable>MyOutputTable</OutputTable>  
            </Query>  
            <Databases>   
                <Database> UseSystemDatabases = "true"   
                           UseUserDatabases = "true"  
                </Database>  
            </Databases>  
         \</ns:TSQLQueryCollector>');  
  
EXEC sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid,  
    @name = 'My custom TSQL query collector item',  
    @frequency = 6000,  
    @parameters = @params,  
    @collection_item_id = @collection_item_id OUTPUT;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)   
 [sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)   
 [syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)   
 [sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
