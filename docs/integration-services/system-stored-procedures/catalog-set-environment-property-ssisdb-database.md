---
title: catalog.set_environment_property (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a345675b-d32e-4624-96cf-ec656730b114
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 71d673ddb0ebb66b22cee7651bc74bd44cf7e089
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912878"
---
# <a name="catalogset_environment_property-ssisdb-database"></a>catalog.set_environment_property (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Define a propriedade de um ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_environment_property [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o ambiente. O *folder_name* é **nvarchar(128)** .  
  
 [ @environment_name = ] *environment_name*  
 O nome do ambiente. O *environment_name* é **nvarchar(128)** .  
  
 [ @property_name = ] *property_name*  
 O nome de uma propriedade de ambiente. O *property_name* é **nvarchar(128)** .  
  
 [ @property_value = ] *property_value*  
 O valor da propriedade de ambiente. O *property_value* é **nvarchar(1024)** .  
  
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
  
-   O nome da propriedade não é válido  
  
-   O nome do ambiente não é válido  
  
## <a name="remarks"></a>Comentários  
 Nesta versão, somente a propriedade `Description` pode ser definida. O valor da propriedade `Description` não pode exceder 4000 caracteres.  
  
  
