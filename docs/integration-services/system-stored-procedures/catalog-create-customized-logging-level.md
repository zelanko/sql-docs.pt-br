---
title: Catalog.create_customized_logging_level | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 126fa0af811033bb0be035b1f4c550620c696bb3
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreatecustomizedlogginglevel"></a>Catalog.create_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Cria um novo nível de log personalizado. Para obter mais informações sobre níveis de log personalizados, consulte [Integration Services &#40; SSIS &#41; Registro em log](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @event_value = ] event_value  
    , [ @level_id = ] level_id OUT  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @level_name =] *level_name*  
 O nome do novo nível de log personalizado.  
  
 O *level_name* é **nvarchar (128)**.  
  
 [ @level_description =] *level_description*  
 A descrição existente novo nível de log personalizado.  
  
 O *level_description* é **nvarchar (1024)**.  
  
 [ @profile_value =] *profile_value*  
 As estatísticas que você deseja que o novo personalizado de nível de log para fazer logon.  
  
 Os valores válidos para as estatísticas incluem o seguinte. Esses valores correspondem aos valores no **estatísticas** guia do **personalizada de gerenciamento de nível de registro em log** caixa de diálogo.  
  
-   Execução = 0  
  
-   Volume = 1  
  
-   Desempenho = 2  
  
 O *profile_value* é um **bigint**.  
  
 [ @event_value =] *event_value*  
 Os eventos que você deseja que o novo personalizado de nível de log para fazer logon.  
  
 Os valores válidos para eventos incluem o seguinte. Esses valores correspondem aos valores no **eventos** guia do **personalizada de gerenciamento de nível de registro em log** caixa de diálogo.  
  
|Eventos sem contexto do evento|Eventos com o contexto do evento|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> Diagnóstico = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext = 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext = 48|  
  
 O *event_value* é um **bigint**.  
  
 [ @level_id =] *level_id* -OUT  
 A id do novo nível de log personalizado.  
  
 O *level_id* é um **bigint**.  
  
## <a name="remarks"></a>Comentários  
 Para combinar vários valores em Transact-SQL para o *profile_value* ou *event_value* argumento, siga este exemplo. Para capturar os eventos de DiagnosticEx (15), a fórmula para calcular e OnError (8) *event_value* é `2^8 + 2^15 = 33024`.  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (êxito)  
  
 Quando há falha no procedimento armazenado, ele gera um erro.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação na função de banco de dados **ssis_admin**  
  
-   Associação na função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve as condições que podem provocar falha no procedimento armazenado.  
  
-   O usuário não tem as permissões necessárias.  
  
  
