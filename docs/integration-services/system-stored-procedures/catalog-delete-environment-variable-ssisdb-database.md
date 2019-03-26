---
title: catalog.delete_environment_variable (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 894b3bdb-aa34-463e-aba4-1b68ad96a0ef
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fecf77944ef9c3601c40405def1641604ddb3b0f
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58276475"
---
# <a name="catalogdeleteenvironmentvariable-ssisdb-database"></a>catalog.delete_environment_variable (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exclui uma variável de um ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
delete_environment_variable [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o ambiente. O *folder_name* é **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 O nome do ambiente que contém a variável. O *environment_name* é **nvarchar(128)**.  
  
 [ @variable_name = ] *variable_name*  
 O nome da variável que deve ser excluída. O *variable_name* é **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no ambiente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome do ambiente não é válido  
  
-   A variável de ambiente não existe  
  
  
