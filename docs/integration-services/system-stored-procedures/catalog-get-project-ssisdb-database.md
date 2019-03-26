---
title: catalog.get_project (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f263c9e4-a7db-4888-a458-70ae99b1f729
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 28fe8cd113404d2a5672daa249c80f3b3d91620c
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275016"
---
# <a name="cataloggetproject-ssisdb-database"></a>catalog.get_project (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Recupera o fluxo binário de um projeto que foi implantado no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.get_project [ @folder_name = ] folder_name , [ @project_name = ] project_name   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o projeto. *folder_name* é **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 O nome do projeto. *project_name* é **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O fluxo binário do projeto é retornado como **varbinary(MAX)**. Nenhum resultado será retornado se a pasta ou o projeto não for localizado.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ no projeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem fazer com que o procedimento armazenado get_project gere um erro:  
  
-   O projeto não existe  
  
-   A pasta não existe  
  
-   O usuário não tem as permissões apropriadas  
  
  
