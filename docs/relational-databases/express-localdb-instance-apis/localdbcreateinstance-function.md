---
title: "Função LocalDBCreateInstance | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- LocalDBCreateInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 3eebb485-8a53-4a79-82a9-57b8de9f8e84
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c044ceddef837aa063ea84c071081417c17f415a
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="localdbcreateinstance-function"></a>Função LocalDBCreateInstance
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Cria uma nova instância de LocalDB do SQL Server Express.  
  
 **Arquivo de cabeçalho:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT LocalDBCreateInstance(  
           PCWSTR wszVersion,  
           PCWSTR pInstanceName,   
           DWORD dwFlags   
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *wszVersion*  
 [Entrada] A versão LocalDB, por exemplo 11.0 ou 11.0.1094.2.  
  
 *pInstanceName*  
 [Entrada] O nome para a instância de LocalDB ser criada.  
  
 *dwFlags*  
 [Entrada] Reservado para uso futuro. Atualmente deve ser definido como 0.  
  
## <a name="returns"></a>Retorna  
 S_OK  
 A função foi bem-sucedida.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 O LocalDB do SQL Server Express não está instalado no computador.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Um ou mais parâmetros de entrada especificados são inválidos.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 O nome de instância especificado é inválido.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 O caminho em que a instância deve estar armazenada não é maior que MAX_PATH.  
  
 [LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-instance-exists-with-lower-version.md)  
 A instância especificada já existe, mas sua versão é inferior à solicitada.  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-version.md)  
 A versão especificada não está disponível.  
  
 [LOCALDB_ERROR_VERSION_REQUESTED_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-version-requested-not-installed.md)  
 O nível de patch especificado não está instalado.  
  
 [LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-create-instance-folder.md)  
 Uma pasta não pode ser criada abaixo de %userprofile%.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 Não é possível recuperar uma pasta de perfil de usuário.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 Não é possível acessar uma pasta de instância.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 Não é possível acessar um registro de instância.  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 Não é possível modificar um registro de instância.  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 Um processo do SQL Server foi iniciado, mas houve falha na inicialização do SQL Server.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Uma configuração de instância está corrompida.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Erro inesperado. Consulte o log de eventos para obter detalhes.  
  
## <a name="remarks"></a>Remarks  
 Se uma instância de LocalDB completamente funcional com o nome especificado já existir e sua versão for igual a ou mais alta que a solicitada, o resultado será S_OK.  
  
 Em casos em que uma instância existente torna-se corrompida, chamadas subsequentes para a API do método **LocalDBCreateInstance** falharão. As instâncias corrompidas devem ser corrigidas manualmente ou explicitamente excluídas antes de poderem ser usadas novamente.  
  
 Para obter uma amostra do código que usa a API LocalDB, consulte [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
