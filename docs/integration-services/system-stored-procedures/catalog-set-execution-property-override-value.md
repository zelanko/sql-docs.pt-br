---
title: catalog.set_execution_property_override_value | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8e561e94e3dee033941c5defade34d28b1ac89c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="catalogsetexecutionpropertyoverridevalue"></a>catalog.set_execution_property_override_value
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
  
## <a name="remarks"></a>Comentários  
 Este procedimento executa a mesma função que a seção **Substituições de propriedade** na guia **Avançado** da caixa de diálogo **Executar Pacote**. O caminho para a propriedade é derivado da propriedade **Caminho do Pacote** da tarefa de pacote.  
  
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
  
  
