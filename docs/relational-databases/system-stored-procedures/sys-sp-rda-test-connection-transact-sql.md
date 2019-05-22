---
title: sys.sp_rda_test_connection (Transact-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cdf171c66c19d87ea4919eeb55dca65f14b89ebd
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65982873"
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
 @database_name = N'*db_name*'  
 O nome do banco de dados do SQL Server habilitados para Stretch. Esse parâmetro é opcional.  
  
 @server_address = N'*azure_server_fully_qualified_address*'  
 O endereço totalmente qualificado do servidor do Azure.  
  
-   Se você fornecer um valor para **@database_name**, mas o banco de dados especificado não está habilitado para Stretch, em seguida, você precisa fornecer um valor para **@server_address**.  
  
-   Se você fornecer um valor para **@database_name**e o banco de dados especificado está habilitado para Stretch, em seguida, você não precisa fornecer um valor para **@server_address**. Se você fornecer um valor para **@server_address**, o procedimento armazenado ignorá-la e usa existentes já o servidor do Azure associados com o banco de dados habilitados para Stretch.  
  
 @azure_username = N'*azure_username*  
 O nome de usuário para o servidor remoto do Azure.  
  
 @azure_password = N'*azure_password*'  
 A senha para o servidor remoto do Azure.  
  
 @credential_name = N'*credential_name*'  
 Em vez de fornecer um nome de usuário e senha, você pode fornecer o nome de uma credencial armazenada no banco de dados habilitados para Stretch.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 No caso de **sucesso**, sp_rda_test_connection retorna erro 14855 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_SUCCEEDED) com severidade EX_INFO e código de retorno de um sucesso.  
  
 No caso de **falha**, sp_rda_test_connection retorna erro 14856 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_FAILED) com severidade EX_USER e código de retorno de um erro.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|link_state|INT|Um dos valores a seguir, que correspondem aos valores para **link_state_desc**.<br /><br /> -   0<br />-   1<br />-   2<br />-   3<br />-   4|  
|link_state_desc|varchar(32)|Um dos valores a seguir, que correspondem aos anterior valores para **link_state**.<br /><br /> -ÍNTEGRO<br />     O entre o SQL Server e o Azure remoto server está íntegro.<br />-   ERROR_AZURE_FIREWALL<br />     O firewall do Azure está impedindo que o link entre o SQL Server e o servidor remoto do Azure.<br />-   ERROR_NO_CONNECTION<br />     SQL Server não pode fazer uma conexão ao servidor remoto do Azure.<br />-   ERROR_AUTH_FAILURE<br />     Uma falha de autenticação está impedindo que o link entre o SQL Server e o servidor remoto do Azure.<br />-   ERROR<br />     Um erro que não é um problema de autenticação, um problema de conectividade ou um problema de firewall está impedindo que o link entre o SQL Server e o servidor remoto do Azure.|  
|error_number|INT|O número do erro. Se não houver nenhum erro, esse campo é NULL.|  
|error_message|nvarchar(1024)|A mensagem de erro. Se não houver nenhum erro, esse campo é NULL.|  
  
## <a name="permissions"></a>Permissões  
 Exige permissões db_owner.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>Verifique a conexão do SQL Server para o servidor remoto do Azure  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 Os resultados mostram que o SQL Server não pode se conectar ao servidor remoto do Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<número de erro relacionadas à conexão >*|*\<mensagem de erro relacionadas à conexão >*|  
  
### <a name="check-the-azure-firewall"></a>Verifique o firewall do Azure  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Os resultados mostram que o firewall do Azure está impedindo o link entre o SQL Server e o servidor remoto do Azure.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1|ERROR_AZURE_FIREWALL|*\<número de erro relacionados ao firewall >*|*\<mensagem de erro relacionados ao firewall >*|  
  
### <a name="check-authentication-credentials"></a>Verifique as credenciais de autenticação  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 Os resultados mostram que uma falha de autenticação está impedindo o link entre o SQL Server e o servidor remoto do Azure.  
  
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
  
  
