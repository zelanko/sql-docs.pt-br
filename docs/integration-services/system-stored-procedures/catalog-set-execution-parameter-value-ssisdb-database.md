---
title: catalog.set_execution_parameter_value (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 055d86c9-befd-4e63-acb1-6dfe833549d2
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 12b0e55b44eb10b08f263a49475b2e37a6e3cbba
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogsetexecutionparametervalue-ssisdb-database"></a>catalog.set_execution_parameter_value (Banco de Dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Define o valor de um parâmetro para uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Um valor de parâmetro não pode ser alterado após o início da execução da instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_execution_parameter_value [ @execution_id = execution_id  
    , [ @object_type = ] object_type  
    , [ @parameter_name = ] parameter_name  
    , [ @parameter_value = ] parameter_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id = ] *execution_id*  
 O identificador exclusivo da instância de execução. O *execution_id* é **bigint**.  
  
 [ @object_type = ] *object_type*  
 O tipo do parâmetro.  
  
 Para os parâmetros a seguir, defina *object_type* como 50  
  
-   LOGGING_LEVEL  
  
-   CUSTOMIZED_LOGGING_LEVEL  
  
-   DUMP_ON_ERROR  
  
-   DUMP_ON_EVENT  
  
-   DUMP_EVENT_CODE  
  
-   CALLER_INFO  
  
-   SYNCHRONIZED  
  
 Use o valor `20` para indicar um parâmetro de projeto ou o valor `30` para indicar um parâmetro de pacote.  
  
 O *object_type* é **smallint**.  
  
 [ @parameter_name = ] *parameter_name*  
 O nome do parâmetro. O *parameter_name* é **nvarchar(128)**.  
  
 [ @parameter_value = ] *parameter_value*  
 O valor do parâmetro. O *parameter_value* é **sql_variant**.  
  
## <a name="remarks"></a>Remarks  
 Para descobrir os valores de parâmetros que foram usados para uma determinada execução, consulte a exibição catalog.execution_parameter_values.  
  
 Para especificar o escopo das informações registradas em log durante uma execução de pacote, defina *parameter_name* como LOGGING_LEVEL e *parameter_value* como um dos valores a seguir.  
  
 Defina o parâmetro *object_type* como 50.  
  
|Valor|Description|  
|-----------|-----------------|  
|0|Nenhum<br /><br /> O log está desativado. Apenas o status da execução do pacote é registrado em log.|  
|1|Basic<br /><br /> Todos os eventos são registrados em log, menos personalizados e de diagnóstico. Este é o valor padrão.|  
|2|Desempenho<br /><br /> Apenas estatísticas de desempenho e eventos OnError e OnWarning são registrados em log.|  
|3|Detalhado<br /><br /> Todos os eventos são registrados em log, inclusive eventos personalizados e de diagnóstico. <br />Eventos personalizados incluem os que são registrados em log por meio de tarefas do Integration Services. Para obter mais informações, consulte [Custom Messages for Logging](../../integration-services/performance/integration-services-ssis-logging.md#custom_messages) (Mensagens personalizadas para criação de log)|  
|4|Linhagem de tempo de execução<br /><br /> Coleta os dados necessários para rastrear a linhagem no fluxo de dados.|  
|100|Nível de registro em log personalizado<br /><br /> Especifique as configurações no parâmetro CUSTOMIZED_LOGGING_LEVEL. Para obter mais informações sobre os valores que você pode especificar, consulte [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md).<br /><br /> Para obter mais informações sobre níveis de log personalizados, veja [Habilitar o log para a execução do pacote no servidor SSIS](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).|  
  
 Para especificar que o servidor do Integration Services gera arquivos de despejo quando ocorre qualquer erro durante a execução de um pacote, defina os valores dos parâmetros a seguir para uma instância de execução que não foi executada.  
  
|Parâmetro|Valor|  
|---------------|-----------|  
|*execution_id*|O identificador exclusivo da instância de execução|  
|*object_type*|50|  
|*parameter_name*|‘DUMP_ON_ERROR|  
|*parameter_value*|1|  
  
 Para especificar que o servidor do Integration Services gera arquivos de despejo quando ocorrem eventos durante a execução de um pacote, defina os valores dos parâmetros a seguir para uma instância de execução que não foi executada.  
  
|Parâmetro|Valor|  
|---------------|-----------|  
|*execution_id*|O identificador exclusivo da instância de execução|  
|*object_type*|50|  
|*parameter_name*|'DUMP_ON_EVENT|  
|*parameter_value*|1|  
  
 Para especificar os eventos, durante a execução de um pacote, que fazem com que o servidor do Integration Services gere arquivos de despejo, defina os valores dos parâmetros a seguir para uma instância de execução que não foi executada. Separe vários códigos de eventos com um ponto e vírgula.  
  
|Parâmetro|Valor|  
|---------------|-----------|  
|*execution_id*|O identificador exclusivo da instância de execução|  
|*object_type*|50|  
|*parameter_name*|DUMP_EVENT_CODE|  
|*parameter_value*|Um ou mais códigos de evento|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir especifica que o servidor do Integration Services gera arquivos de despejo quando ocorre um erro durante a execução de um pacote.  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_ERROR',1  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir especifica que o servidor do Integration Services gera arquivos de despejo quando ocorrem eventos durante a execução de um pacote e especifica o evento que faz com que o servidor gere os arquivos.  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_EVENT',1  
  
declare @event_code nvarchar(50)  
set @event_code = '0xC020801C'  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_EVENT_CODE', @event_code  
```  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O usuário não tem as permissões apropriadas  
  
-   O identificador da execução não é válido  
  
-   O nome do parâmetro não é válido  
  
-   O tipo de dados do valor do parâmetro não corresponde ao tipo de dados do parâmetro  
  
## <a name="see-also"></a>Consulte Também  
 [catalog.execution_parameter_values &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)   
 [Gerar arquivos de despejo para execução de pacote](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
