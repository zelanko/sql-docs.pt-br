---
title: catalog.rename_folder (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 336ab467-c32f-4d2e-a79c-174dc6fab75e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 25772e438e819032ec4742f58404a6a4beeceeee
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277335"
---
# <a name="catalogrenamefolder-ssisdb-database"></a>catalog.rename_folder (Banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Renomeia uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.rename_folder [ @old_name = ] old_name , [ @new_name = ] new_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @old_name = ] *old_name*  
 O nome original da pasta. O *old_name* é **nvarchar(128)**.  
  
 [ @new_name = ] *new_name*  
 O novo nome da pasta. O *new_name* é **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome original da pasta não é válido  
  
-   O novo nome já foi usado em uma pasta existente  
  
  
