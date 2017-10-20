---
title: Catalog. set_environment_reference_type (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b79e3a06-22c0-40e5-8933-1b3414db3329
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e83d9979ee4736528efb4851848ea3eac717fab8
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetenvironmentreferencetype-ssisdb-database"></a>catalog.set_environment_reference_type (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Define o tipo de referência e o nome de ambiente associados a uma referência de ambiente existente para um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_environment_reference_location [ @reference_id = reference_id  
    , [ @reference_type = ] reference_type  
 [  , [ @environment_folder_name = ] environment_folder_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @reference_id =] *reference_id*  
 O identificador exclusivo da referência de ambiente que deve ser atualizada. O *reference_id* é **bigint**.  
  
 [ @reference_type =] *reference_type*  
 Indica se o ambiente pode ser localizado na mesma pasta do projeto (referência relativa) ou em uma pasta diferente (referência absoluta). Use o valor `R` para indicar uma referência relativa. Use o valor `A` para indicar uma referência absoluta. O *reference_type* é **char (1)**.  
  
 [ @environment_folder_name =] *environment_folder_name*  
 A pasta na qual o ambiente está localizado. Esse valor é necessário para referências absolutas. O *environment_folder_name* é **nvarchar (128)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY no projeto e permissão READ no ambiente  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O nome de pasta, o nome de ambiente ou o ID de referência não é válido  
  
-   O usuário não as permissões adequadas  
  
-   Uma referência absoluta é especificada usando o `A` caractere o *reference_location* parâmetro, mas o nome da pasta não foi especificado com o *environment_folder_name* parâmetro.  
  
## <a name="remarks"></a>Comentários  
 Um projeto pode ter referências de ambiente relativas ou absolutas. As referências relativas fazem referência ao ambiente pelo nome e requerem que ele resida na mesma pasta do projeto. As referências absolutas fazem referência ao ambiente por nome e pasta. Elas podem fazer referência a ambientes que residam em uma pasta diferente da pasta do projeto. Um projeto pode fazer referência a vários ambientes.  
  
> [!IMPORTANT]  
>  Se uma referência relativa for especificada, o *environment_folder_name* o valor do parâmetro não é usado e o nome da pasta de ambiente é definido automaticamente como **nulo**. Se uma referência absoluta for especificada, o nome da pasta de ambiente deve ser fornecido no *environment_folder_name* parâmetro.  
  
  
