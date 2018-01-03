---
title: sys.sp_rda_test_connection (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_test_connection
- sys.sp_rda_test_connection_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_rda_test_connection stored procedure
ms.assetid: e2ba050c-d7e3-4f33-8281-c9b525b4edb4
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e7376d3b6fa4bebac0e0b176bd4144d6bec54b0c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="syssprdatestconnection-transact-sql"></a>sys.sp_rda_test_connection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Testa a conexão do SQL Server para o servidor remoto do Azure e reporta problemas que podem impedir que a migração de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EXECUTE sys.sp_rda_test_connection  
   @database_name = N'db_name',   
   @server_address = N'azure_server_fully_qualified_address',  
   @azure_username = N'azure_username',   
   @azure_password = N'azure_password',  
   @credential_name = N'credential_name'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 @database_name= N'*db_name*'  
 O nome do banco de dados do SQL Server habilitado para Stretch. Esse parâmetro é opcional.  
  
 @server_address= N'*azure_server_fully_qualified_address*'  
 O endereço totalmente qualificado do servidor do Azure.  
  
-   Se você fornecer um valor para  **@database_name** , mas o banco de dados especificado não está habilitado para Stretch, você precisa fornecer um valor para  **@server_address** .  
  
-   Se você fornecer um valor para  **@database_name** e o banco de dados especificado é habilitado para Stretch, você não precisa fornecer um valor para  **@server_address** . Se você fornecer um valor para  **@server_address** , ignora o procedimento armazenado e usa existentes de servidor do Azure já associados ao banco de dados habilitado para Stretch.  
  
 @azure_username= N'*azure_username*  
 O nome de usuário para o servidor remoto do Azure.  
  
 @azure_password= N'*azure_password*'  
 A senha para o servidor remoto do Azure.  
  
 @credential_name= N'*credential_name*'  
 Em vez de fornecer um nome de usuário e senha, você pode fornecer o nome de uma credencial armazenada no banco de dados habilitado para Stretch.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 No caso do **êxito**sp_rda_test_connection retorna erro 14855 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_SUCCEEDED) com severidade EX_INFO e código de retorno de sucesso.  
  
 No caso do **falha**, sp_rda_test_connection retorna erro 14856 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_FAILED) com severidade EX_USER e código de retorno de um erro.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|link_state|INT|Um dos valores a seguir, que correspondem aos valores de **link_state_desc**.<br /><br /> -   0<br />-   1<br />-   2<br />-   3<br />-   4|  
|link_state_desc|varchar (32)|Um dos valores a seguir, que correspondem à anterior valores para **link_state**.<br /><br /> -ÍNTEGRO<br />     O entre o SQL Server e o Azure remoto server está íntegro.<br />-ERROR_AZURE_FIREWALL<br />     O firewall do Azure está impedindo que o link entre o servidor remoto do Azure e SQL Server.<br />-ERROR_NO_CONNECTION<br />     SQL Server não pode fazer uma conexão ao servidor remoto do Azure.<br />-ERROR_AUTH_FAILURE<br />     Uma falha de autenticação está impedindo que o link entre o servidor remoto do Azure e SQL Server.<br />-ERRO<br />     Um erro que não é um problema de autenticação, um problema de conectividade ou um problema de firewall está impedindo que o link entre o servidor remoto do Azure e SQL Server.|  
|error_number|INT|O número do erro. Se não houver nenhum erro, esse campo é NULL.|  
|error_message|nvarchar(1024)|A mensagem de erro. Se não houver nenhum erro, esse campo é NULL.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissões db_owner.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>Verifique a conexão do SQL Server para o servidor remoto do Azure  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 Os resultados mostram que o SQL Server não pode se conectar ao servidor remoto do Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<número de erro relacionadas à conexão >*|*\<mensagem de erro de conexão >*|  
  
### <a name="check-the-azure-firewall"></a>Verifique o firewall do Azure  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Os resultados mostram que o firewall do Azure está impedindo o link entre o servidor remoto do Azure e SQL Server.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1|ERROR_AZURE_FIREWALL|*\<número de erro relacionada ao firewall >*|*\<mensagem de erro relacionada ao firewall >*|  
  
### <a name="check-authentication-credentials"></a>Verificar as credenciais de autenticação.  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Os resultados mostram que uma falha de autenticação está impedindo o link entre o servidor remoto do Azure e SQL Server.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<número de erro relacionadas à autenticação >*|*\<mensagem de erro relacionadas à autenticação >*|  
  
### <a name="check-the-status-of-the-remote-azure-server"></a>Verificar o status do servidor remoto do Azure  
  
```sql  
USE <SQL Server database>  
GO  
EXECUTE sys.sp_rda_test_connection   
    @server_address = N'<server name>.database.windows.net',   
    @azure_username = N'<user name>',   
    @azure_password = N'<password>'  
GO  
  
```  
  
 Os resultados mostram que a conexão está íntegro e que você pode habilitar o Stretch Database para o banco de dados especificado.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|HEALTHY|NULL|NULL|  
  
  
