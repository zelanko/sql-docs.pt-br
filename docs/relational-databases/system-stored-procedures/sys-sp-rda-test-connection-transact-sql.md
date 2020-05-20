---
title: sys. sp_rda_test_connection (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_test_connection
- sys.sp_rda_test_connection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_test_connection stored procedure
ms.assetid: e2ba050c-d7e3-4f33-8281-c9b525b4edb4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ab377b42943c943f710d83661642423cfc070949
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814501"
---
# <a name="syssp_rda_test_connection-transact-sql"></a>sys. sp_rda_test_connection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Testa a conexão de SQL Server para o servidor remoto do Azure e relata problemas que podem impedir a migração de dados.  
  
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
 @database_name= N '*db_name*'  
 O nome do banco de dados de SQL Server habilitado para Stretch. Esse parâmetro é opcional.  
  
 @server_address= N '*azure_server_fully_qualified_address*'  
 O endereço totalmente qualificado do servidor do Azure.  
  
-   Se você fornecer um valor para ** \@ database_name**, mas o banco de dados especificado não estiver habilitado para Stretch, você precisará fornecer um valor para ** \@ server_address**.  
  
-   Se você fornecer um valor para ** \@ database_name**e o banco de dados especificado estiver habilitado para Stretch, você não precisará fornecer um valor para ** \@ server_address**. Se você fornecer um valor para ** \@ server_address**, o procedimento armazenado o ignorará e usará o servidor do Azure existente já associado ao banco de dados habilitado para Stretch.  
  
 @azure_username= N '*azure_username*  
 O nome de usuário para o servidor remoto do Azure.  
  
 @azure_password= N '*azure_password*'  
 A senha do servidor remoto do Azure.  
  
 @credential_name= N '*credential_name*'  
 Em vez de fornecer um nome de usuário e senha, você pode fornecer o nome de uma credencial armazenada no banco de dados habilitado para Stretch.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 No caso de **sucesso**, sp_rda_test_connection retorna o erro 14855 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_SUCCEEDED) com EX_INFO de severidade e um código de retorno de sucesso.  
  
 Em caso de **falha**, sp_rda_test_connection retorna o erro 14856 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_FAILED) com EX_USER de severidade e um código de retorno de erro.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|link_state|int|Um dos valores a seguir, que correspondem aos valores de **link_state_desc**.<br /><br /> -0<br />-1<br />-2<br />-3<br />-4|  
|link_state_desc|varchar (32)|Um dos valores a seguir, que correspondem aos valores anteriores para **link_state**.<br /><br /> -ÍNTEGRO<br />     O entre SQL Server e o servidor remoto do Azure está íntegro.<br />-ERROR_AZURE_FIREWALL<br />     O Firewall do Azure está impedindo o vínculo entre SQL Server e o servidor remoto do Azure.<br />-ERROR_NO_CONNECTION<br />     SQL Server não pode estabelecer uma conexão com o servidor remoto do Azure.<br />-ERROR_AUTH_FAILURE<br />     Uma falha de autenticação está impedindo o vínculo entre SQL Server e o servidor remoto do Azure.<br />-ERRO<br />     Um erro que não é um problema de autenticação, um problema de conectividade ou um problema de firewall está impedindo o vínculo entre SQL Server e o servidor remoto do Azure.|  
|error_number|int|O número do erro. Se não houver nenhum erro, esse campo será nulo.|  
|error_message|nvarchar(1024)|A mensagem de erro. Se não houver nenhum erro, esse campo será nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer db_owner permissões.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>Verifique a conexão de SQL Server para o servidor remoto do Azure  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 Os resultados mostram que SQL Server não pode se conectar ao servidor remoto do Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<número de erro relacionado à conexão>*|*\<mensagem de erro relacionada à conexão>*|  
  
### <a name="check-the-azure-firewall"></a>Verificar o Firewall do Azure  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Os resultados mostram que o Firewall do Azure está impedindo o vínculo entre SQL Server e o servidor remoto do Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1|ERROR_AZURE_FIREWALL|*\<número de erro relacionado ao firewall>*|*\<mensagem de erro relacionada ao firewall>*|  
  
### <a name="check-authentication-credentials"></a>Verificar credenciais de autenticação  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Os resultados mostram que uma falha de autenticação está impedindo o vínculo entre SQL Server e o servidor remoto do Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<número de erro relacionado à autenticação>*|*\<mensagem de erro relacionada à autenticação>*|  
  
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
  
 Os resultados mostram que a conexão está íntegra e que você pode habilitar Stretch Database para o banco de dados especificado.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|HEALTHY|NULO|NULO|  
  
  
