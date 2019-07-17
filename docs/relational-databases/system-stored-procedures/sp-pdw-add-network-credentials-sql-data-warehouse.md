---
title: sp_pdw_add_network_credentials (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: da1ba0db4467526ef2b54650020a899f88788648
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008947"
---
# <a name="sppdwaddnetworkcredentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Isso armazena as credenciais de rede em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e os associa a um servidor. Por exemplo, usar esse procedimento armazenado para dar [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] apropriado de permissões de leitura/gravação para realizar backup de banco de dados e restaurar operações em um servidor de destino ou para criar um backup de um certificado usado para a TDE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  
  
## <a name="arguments"></a>Argumentos  
 '*target_server_name*'  
 Especifica o nome de host do servidor de destino ou endereço IP. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] acessarão este servidor usando as credenciais de nome de usuário e senha passadas para esse procedimento armazenado.  
  
 Para se conectar por meio da rede InfiniBand, use o endereço IP do InfiniBand do servidor de destino.  
  
 *target_server_name* é definido como nvarchar(337).  
  
 '*user_name*'  
 Especifica o user_name que tem permissões para acessar o servidor de destino. Se as credenciais já existirem para o servidor de destino, eles serão atualizados para as novas credenciais.  
  
 *user_name* é definido como nvarchar (513).  
  
 '*senha*ꞌ  
 Especifica a senha para *user_name*.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer **ALTER SERVER STATE** permissão.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Ocorrerá um erro se não for bem-sucedida adicionando as credenciais no nó de controle e todos os nós de computação.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Esse procedimento armazenado adiciona credenciais de rede para a conta do NetworkService para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. A conta NetworkService é executado a cada instância do SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no nó de controle e os nós de computação. Por exemplo, quando uma operação de backup é executado, o nó de controle e cada nó de computação usará as credenciais da conta NetworkService para obter a leitura e a permissão de gravação para o servidor de destino.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>A. Adicionar credenciais para executar um backup de banco de dados  
 O exemplo a seguir associa as credenciais de nome e a senha do usuário para o seattle\david de usuário de domínio com um servidor de destino que tenha o endereço IP 10.172.63.255. Seattle\david o usuário tem permissões de leitura/gravação para o servidor de destino. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] armazenará essas credenciais e usá-los para ler e gravar para e do servidor de destino, conforme necessário para backup e restaurar operações.  
  
```  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 O comando de backup exige que o nome do servidor ser inserido como um endereço IP.  
  
> [!NOTE]  
>  Para executar o backup do banco de dados através de InfiniBand, certifique-se de usar o endereço IP do InfiniBand do servidor de backup.  
  
## <a name="see-also"></a>Consulte também  
 [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

