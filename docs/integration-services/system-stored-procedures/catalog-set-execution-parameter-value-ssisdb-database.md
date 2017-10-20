---
title: Catalog. set_execution_parameter_value (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 055d86c9-befd-4e63-acb1-6dfe833549d2
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 7b13e7b1c28bad6e573e829183372da4bb62f92d
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="catalogsetexecutionparametervalue-ssisdb-database"></a>catalog.set_execution_parameter_value (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Define o valor de um parâmetro para uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Um valor de parâmetro não pode ser alterado após o início da execução da instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
set_execution_parameter_value [ @execution_id = execution_id  
    , [ @object_type = ] object_type  
    , [ @parameter_name = ] parameter_name  
    , [ @parameter_value = ] parameter_value  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id =] *execution_id*  
 O identificador exclusivo da instância de execução. O *execution_id* é **bigint**.  
  
 [ @object_type =] *object_type*  
 O tipo de parâmetro.  
  
 Para os seguintes parâmetros, definir *object_type* como 50  
  
-   LOGGING_LEVEL  
  
-   CUSTOMIZED_LOGGING_LEVEL  
  
-   DUMP_ON_ERROR  
  
-   DUMP_ON_EVENT  
  
-   DUMP_EVENT_CODE  
  
-   CALLER_INFO  
  
-   SYNCHRONIZED  
  
 Use o valor `20` para indicar um parâmetro de projeto ou o valor `30` para indicar um parâmetro de pacote.  
  
 O *object_type* é **smallint**.  
  
 [ @parameter_name =] *parameter_name*  
 O nome do parâmetro. O *parameter_name* é **nvarchar (128)**.  
  
 [ @parameter_value =] *parameter_value*  
 O valor do parâmetro. O *parameter_value* é **sql_variant**.  
  
## <a name="remarks"></a>Comentários  
 Para descobrir os valores de parâmetros que foram usados para uma determinada execução, consulte a exibição catalog.execution_parameter_values.  
  
 Para especificar o escopo das informações que são registrados durante a execução de um pacote, defina *parameter_name* como LOGGING_LEVEL e *parameter_value* para um dos valores a seguir.  
  
 Definir o *object_type* parâmetro como 50.  
  
|Value|Descrição|  
|-----------|-----------------|  
|0|Nenhuma<br /><br /> O log está desativado. Apenas o status da execução do pacote é registrado em log.|  
|1|Basic<br /><br /> Todos os eventos são registrados em log, menos personalizados e de diagnóstico. Este é o valor padrão.|  
|2|Desempenho<br /><br /> Apenas estatísticas de desempenho e eventos OnError e OnWarning são registrados em log.|  
|3|detalhado<br /><br /> Todos os eventos são registrados em log, inclusive eventos personalizados e de diagnóstico. <br />Eventos personalizados incluem os que são registrados em log por meio de tarefas do Integration Services. Para obter mais informações, consulte [mensagens personalizadas para registro em log](../../integration-services/performance/integration-services-ssis-logging.md#custom_messages)|  
|4|Linhagem de tempo de execução<br /><br /> Coleta os dados necessários para rastrear a linhagem no fluxo de dados.|  
|100|Nível de log personalizado<br /><br /> Especifique as configurações no parâmetro CUSTOMIZED_LOGGING_LEVEL. Para obter mais informações sobre os valores que você pode especificar, consulte [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md).<br /><br /> Para obter mais informações sobre níveis de log personalizados, consulte [Habilitar log de execução do pacote no servidor do SSIS](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).|  
  
 Para especificar que o servidor do Integration Services gera arquivos de despejo quando ocorre qualquer erro durante a execução de um pacote, defina os valores dos parâmetros a seguir para uma instância de execução que não foi executada.  
  
|Parâmetro|Value|  
|---------------|-----------|  
|*execution_id*|O identificador exclusivo da instância de execução|  
|*object_type*|50|  
|*parameter_name*|‘DUMP_ON_ERROR|  
|*parameter_value*|1|  
  
 Para especificar que o servidor do Integration Services gera arquivos de despejo quando ocorrem eventos durante a execução de um pacote, defina os valores dos parâmetros a seguir para uma instância de execução que não foi executada.  
  
|Parâmetro|Value|  
|---------------|-----------|  
|*execution_id*|O identificador exclusivo da instância de execução|  
|*object_type*|50|  
|*parameter_name*|'DUMP_ON_EVENT|  
|*parameter_value*|1|  
  
 Para especificar os eventos, durante a execução de um pacote, que fazem com que o servidor do Integration Services gere arquivos de despejo, defina os valores dos parâmetros a seguir para uma instância de execução que não foi executada. Separe vários códigos de eventos com um ponto e vírgula.  
  
|Parâmetro|Value|  
|---------------|-----------|  
|*execution_id*|O identificador exclusivo da instância de execução|  
|*object_type*|50|  
|*parameter_name*|DUMP_EVENT_CODE|  
|*parameter_value*|Um ou mais códigos de evento|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir especifica que o servidor do Integration Services gera arquivos de despejo quando ocorre um erro durante a execução de um pacote.  
  
```  
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_ERROR',1  
  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir especifica que o servidor do Integration Services gera arquivos de despejo quando ocorrem eventos durante a execução de um pacote e especifica o evento que faz com que o servidor gere os arquivos.  
  
```  
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_EVENT',1  
  
declare @event_code nvarchar(50)  
set @event_code = '0xC020801C'  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_EVENT_CODE', @event_code  
```  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY na instância de execução  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O usuário não tem as permissões apropriadas  
  
-   O identificador da execução não é válido  
  
-   O nome do parâmetro não é válido  
  
-   O tipo de dados do valor do parâmetro não corresponde ao tipo de dados do parâmetro  
  
## <a name="see-also"></a>Consulte também  
 [Catalog. execution_parameter_values &#40; Banco de dados SSISDB &#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)   
 [Gerando arquivos de despejo para execução de pacote](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
