---
title: catalog.create_environment_reference (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 48069bea-31cb-4a0e-9849-a07edc94088f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 73871d69a8fbdc56b2359aa888cbc08e572a6107
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65716914"
---
# <a name="catalogcreateenvironmentreference-ssisdb-database"></a>catalog.create_environment_reference (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Cria uma referência de ambiente para um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.create_environment_reference [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @environment_name = ] environment_name  
     , [ @reference_location = ] reference_location  
  [  , [ @environment_folder_name = ] environment_folder_name ]  
  [  , [ @reference_id = ] reference_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 O nome da pasta do projeto que está referenciando o ambiente. O *folder_name* é **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 O nome do projeto que está referenciando o ambiente. O *project_name* é **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 O nome do ambiente que está sendo referenciado. O *environment_name* é **nvarchar(128)**.  
  
 [ @reference_location = ] *reference_location*  
 Indica se o ambiente pode ser localizado na mesma pasta do projeto (referência relativa) ou em uma pasta diferente (referência absoluta). Use o valor `R` para indicar uma referência relativa. Use o valor `A` para indicar uma referência absoluta. O *reference_location* é **char(1)**.  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 O nome da pasta na qual o ambiente que está sendo referenciado está localizado. Esse valor é necessário para referências absolutas. O *environment_folder_name* é **nvarchar(128)**.  
  
 [ @reference_id = ] *reference_id*  
 Retorna o identificador exclusivo da nova referência. Esse parâmetro é opcional. O *reference_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no projeto e permissão READ no ambiente  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome da pasta não é válido  
  
-   O nome do projeto não é válido  
  
-   O usuário não tem as permissões adequadas  
  
-   Uma referência absoluta está especificada usando o caractere `A` no parâmetro *reference_location*, mas o nome da pasta não foi especificado com o parâmetro *environment_folder_name*.  
  
## <a name="remarks"></a>Remarks  
 Um projeto pode ter referências de ambiente relativas ou absolutas. As referências relativas fazem referência ao ambiente pelo nome e requerem que ele resida na mesma pasta do projeto. As referências absolutas fazem referência ao ambiente por nome e pasta. Elas podem fazer referência a ambientes que residam em uma pasta diferente da pasta do projeto. Um projeto pode fazer referência a vários ambientes.  
  
  
