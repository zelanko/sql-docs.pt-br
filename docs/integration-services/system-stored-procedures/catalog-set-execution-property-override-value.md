---
title: Catalog.set_execution_property_override_value | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 20f2c882a78f5e60931b0152d5877898e1972d0a
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetexecutionpropertyoverridevalue"></a>catalog.set_execution_property_override_value
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Define o valor de uma propriedade para uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id =] *execution_id*  
 O identificador exclusivo da instância de execução. O *execution_id* é **bigint**.  
  
 [ @property_path =] *property_path*  
 O caminho para a propriedade no pacote. O *property_path* é **nvarchar (4000)**.  
  
 [ @property_value =] *property_value*  
 O valor de substituição a ser atribuído à propriedade. O *property_value* é **nvarchar (max)**.  
  
 [ @sensitive =] *confidenciais*  
 Quando o valor for 1, a propriedade será confidencial e criptografada quando for armazenada. Quando o valor for 0, a propriedade não será confidencial e o valor será armazenado em texto não criptografado. O *confidenciais* argumento é **bit**.  
  
## <a name="remarks"></a>Comentários  
 Esse procedimento executa a mesma função que o **substituições de propriedade** seção o **avançado** guia do **executar pacote** caixa de diálogo. O caminho para a propriedade é derivado de **caminho de pacote** propriedade da tarefa de pacote.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O usuário não tem as permissões apropriadas  
  
-   O identificador da execução não é válido  
  
-   O caminho da propriedade não é válido  
  
-   O tipo de dados do valor da propriedade não corresponde ao tipo de dados da propriedade  
  
## <a name="see-also"></a>Consulte também  
 [catalog.set_execution_parameter_value &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
  
