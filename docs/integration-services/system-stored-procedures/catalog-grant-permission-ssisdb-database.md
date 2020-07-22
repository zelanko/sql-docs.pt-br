---
title: catalog.grant_permission (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- grant_permission stored procedure [Integration Services]
- catalog.grant_permission stored procedure [Integration Services]
ms.assetid: e72cfd52-de66-45e9-98b9-b8580ac7b956
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4eb835fb8f5d81d5c15ecc0bf3c6911c2dfb05ef
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912973"
---
# <a name="cataloggrant_permission-ssisdb-database"></a>catalog.grant_permission (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Concede uma permissão em um objeto protegível no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
catalog.grant_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @object_type = ] *object_type*  
 O tipo de objeto protegível. Os tipos de objetos protegíveis incluem pasta (`1`), projeto (`2`), ambiente (`3`) e operação (`4`). O *object_type* é **smallint** _._  
  
 [ @object_id = ] *object_id*  
 O ID (identificador exclusivo) do objeto protegível. O *object_id* é **bigint**.  
  
 [ @principal_id = ] *principal_id*  
 O ID da entidade de segurança que receberá a permissão. O *principal_id* é **int**.  
  
 [ @permission_type = ] *permission_type*  
 O tipo de permissão a ser concedido. O *permission_type* é **smallint**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito)  
  
 1 (object_class é inválido)  
  
 2 (object_id não existe)  
  
 3 (a entidade de segurança não existe)  
  
 4 (a permissão é inválida)  
  
 5 (outro erro)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões ASSIGN_PERMISSIONS no objeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  

Esse procedimento não pode ser chamado por logons que foram autenticados pelo SQL Server. Ele não pode ser chamado pelo logon de sa.
  
## <a name="remarks"></a>Comentários  
 Este procedimento armazenado permite que você conceda os tipos de permissão descritos na seguinte tabela:  
  
|Valor de permission_type|Nome da permissão|Descrição da permissão|Tipos de objeto aplicáveis|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|Permite que a entidade de segurança leia informações consideradas parte do objeto, como as propriedades. Não permite que a entidade de segurança enumere ou leia o conteúdo de outros objetos contidos no objeto.|Pasta, projeto, ambiente, operação|  
|`2`|MODIFY|Permite que a entidade de segurança modifique informações consideradas parte do objeto, como as propriedades. Não permite que a entidade de segurança modifique outros objetos contidos no objeto.|Pasta, projeto, ambiente, operação|  
|`3`|Execute|Permite que a entidade de segurança execute todos os pacotes no projeto.|Project|  
|`4`|MANAGE_PERMISSIONS|Permite que a entidade de segurança atribua permissões a objetos.|Pasta, projeto, ambiente, operação|  
|`100`|CREATE_OBJECTS|Permite que a entidade de segurança crie objetos na pasta.|Pasta|  
|`101`|READ_OBJECTS|Permite que a entidade de segurança leia todos os objetos na pasta.|Pasta|  
|`102`|MODIFY_OBJECTS|Permite que a entidade de segurança modifique todos os objetos na pasta.|Pasta|  
|`103`|EXECUTE_OBJECTS|Permite que a entidade de segurança execute todos os pacotes de todos os projetos na pasta.|Pasta|  
|`104`|MANAGE_OBJECT_PERMISSIONS|Permite que a entidade de segurança gerencie permissões em todos os objetos na pasta.|Pasta|  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 Consulte a seção Valores de código de retorno para mensagens e erros relevantes.  
  
  
