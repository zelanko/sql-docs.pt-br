---
title: catalog.move_project (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: ef3b0325-d8e9-472b-bf11-7d3efa6312ff
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c79df90c6093ed93668e504e574c712a2ba2146a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65716024"
---
# <a name="catalogmoveproject---ssisdb-database"></a>catalog.move_project – Banco de Dados SSISDB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Move um projeto de uma pasta para outra no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.move_project [ @source_folder = ] source_folder  
    , [ @project_name = ] project_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @source_folder = ] *source_folder*  
 O nome da pasta de origem, onde o projeto reside antes da movimentação. O *source_folder* é **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 O nome do projeto a ser movido. O *project_name* é **nvarchar(128)**.  
  
 [ @destination_folder = ] *destination_folder*  
 O nome da pasta de destino, onde o projeto reside após a movimentação. O *destination_folder* é **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   As permissões READ e MODIFY no projeto que você deseja mover e a permissão CREATE_OBJECTS na pasta de destino  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem levar este procedimento armazenado a gerar um erro:  
  
-   O projeto não existe  
  
-   A pasta de origem não existe  
  
-   A pasta de destino não existe ou a pasta de destino já contém um projeto com o mesmo nome  
  
-   O usuário não tem as permissões apropriadas  
  
## <a name="remarks"></a>Remarks  
 Quando um projeto é movido de uma pasta de origem para uma pasta de destino, o projeto na pasta de origem e as referências de ambiente correspondentes são excluídos. Na pasta de destino, um projeto idêntico e referências de ambiente são criados. As referências de ambiente serão resolvidas como uma pasta diferente depois da movimentação. As referências absolutas serão resolvidas como a mesma pasta após a movimentação.  
  
> [!NOTE]  
>  Um projeto pode ter referências de ambiente relativas ou absolutas. As referências relativas fazem referência ao ambiente pelo nome. Essas referências requerem que o ambiente resida na mesma pasta do projeto. As referências absolutas fazem referência ao ambiente por nome e pasta. Essas referências fazem referência a ambientes que residam em uma pasta diferente da pasta do projeto.  
  
  
