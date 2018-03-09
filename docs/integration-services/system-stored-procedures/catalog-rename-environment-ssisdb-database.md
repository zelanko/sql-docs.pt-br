---
title: catalog.rename_environment (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: c73d7452-31c5-4f4e-afcc-e9eca760c826
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07839e0dbe6e15d096cb56c655b71d7bc56086be
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="catalogrenameenvironment-ssisdb-database"></a>catalog.rename_environment (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Renomeia um ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.rename_environment [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @new_environment_name= ] new_environment_name  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta que contém o ambiente. O *folder_name* é **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 O nome original da variável de ambiente. O *environment_name* é **nvarchar(128)**.  
  
 [ @new_environment_name = ] *new_environment_name*  
 O novo nome do ambiente. O *new_environment_name* é **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões MODIFY no ambiente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome ambiente original não é válido  
  
-   O novo nome já foi usado em um ambiente existente  
  
## <a name="remarks"></a>Remarks  
 As referências de ambiente de projetos não são atualizadas automaticamente quando você renomeia o ambiente. As referências de ambiente devem ser atualizadas de forma correspondente. Esse procedimento armazenado terá êxito mesmo que as referências de ambiente sejam desfeitas com a alteração do nome do ambiente. As referências de ambiente devem ser atualizadas depois da conclusão desse procedimento armazenado.  
  
> [!NOTE]  
>  Quando uma referência de ambiente não for válida, a validação e a execução dos pacotes correspondentes que usam essas referências falharão.  
  
  
