---
title: catalog.set_execution_property_override_value | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4a12576e083a30a939964803687198ae0842fb73
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715846"
---
# <a name="catalogsetexecutionpropertyoverridevalue"></a>catalog.set_execution_property_override_value 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Define o valor de uma propriedade para uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id = ] *execution_id*  
 O identificador exclusivo da instância de execução. O *execution_id* é **bigint**.  
  
 [ @property_path = ] *property_path*  
 O caminho para a propriedade no pacote. O *property_path* é **nvarchar(4000)**.  
  
 [ @property_value = ] *property_value*  
 O valor de substituição a ser atribuído à propriedade. O *property_value* é **nvarchar(max)**.  
  
 [ @sensitive = ] *sensitive*  
 Quando o valor for 1, a propriedade será confidencial e criptografada quando for armazenada. Quando o valor for 0, a propriedade não será confidencial e o valor será armazenado em texto não criptografado. O argumento *sensitive* é **bit**.  
  
## <a name="remarks"></a>Remarks  
 Este procedimento executa a mesma função que a seção **Substituições de propriedade** na guia **Avançado** da caixa de diálogo **Executar Pacote**. O caminho para a propriedade é derivado da propriedade **Caminho do Pacote** da tarefa de pacote.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O usuário não tem as permissões apropriadas  
  
-   O identificador da execução não é válido  
  
-   O caminho da propriedade não é válido  
  
-   O tipo de dados do valor da propriedade não corresponde ao tipo de dados da propriedade  
  
## <a name="see-also"></a>Consulte Também  
 [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
  
