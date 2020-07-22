---
title: catalog.set_environment_variable_value (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 1d493dad-9d9c-4f0a-87e2-20a2d4a35f99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fa933da5806b916cc200881c880f49ccaa01d746
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912838"
---
# <a name="catalogset_environment_variable_value-ssisdb-database"></a>catalog.set_environment_variable_value (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Define o valor de uma variável de ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_environment_variable_value [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable _name  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o ambiente. O *folder_name* é **nvarchar(128)** .  
  
 [ @environment_name = ] *environment_name*  
 O nome do ambiente. O *environment_name* é **nvarchar(128)** .  
  
 [ @variable_name = ] *variable_name*  
 O nome da variável de ambiente. O *variable _name* é **nvarchar(128)** .  
  
 [ @value = ] *value*  
 O valor da variável de ambiente. O *value* é **sql_variant**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no ambiente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome da pasta não é válido  
  
-   O nome do ambiente não é válido  
  
-   O nome da variável de ambiente não é válido  
  
-   O usuário não tem as permissões adequadas  
  
  
