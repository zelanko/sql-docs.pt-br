---
title: Função LocalDBStartInstance | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- LocalDBStartInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: cb325f5d-10ee-4a56-ba28-db0074ab3926
caps.latest.revision: 17
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3d28685fa83098d6d5a743d06e99e21ffc8604c8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32938071"
---
# <a name="localdbstartinstance-function"></a>Função LocalDBStartInstance
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Inicia a instância especificada de LocalDB do SQL Server Express.  
  
 **Arquivo de cabeçalho:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT LocalDBStartInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           LPWSTR wszSqlConnection,   
           LPDWORD lpcchSqlConnection   
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *pInstanceName*  
 [Entrada] O nome da instância de LocalDB a ser iniciada.  
  
 *dwFlags*  
 [Entrada] Reservado para uso futuro. Atualmente deve ser definido como 0.  
  
 *wszSqlConnection*  
 [Saída] O buffer para armazenar a cadeia de conexão na instância de LocalDB.  
  
 *lpcchSqlConnection*  
 [Saída/entrada] On input contém o tamanho do buffer *wszSqlConnection* em caracteres, incluindo qualquer caractere nulo à esquerda. Na saída, se o tamanho de buffer especificado for muito pequeno, conterá o tamanho de buffer necessário em caracteres, incluindo quaisquer caracteres nulos à esquerda.  
  
## <a name="returns"></a>Retorna  
 S_OK  
 A função foi bem-sucedida.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 O LocalDB do SQL Server Express não está instalado no computador.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Um ou mais parâmetros de entrada especificados são inválidos.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 O nome de instância especificado é inválido.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-instance.md)  
 A instância não existe.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 O buffer *wszSqlConnection* especificado é muito pequeno.  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../../relational-databases/express-localdb-error-messages/localdb-error-wait-timeout.md)  
 Tempo limite esgotado durante tentativa de obtenção de bloqueios de sincronização.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 O caminho em que a instância deve estar armazenada não é maior que MAX_PATH.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 Não é possível recuperar uma pasta de perfil de usuário.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 Não é possível acessar uma pasta de instância.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 Não é possível acessar um registro de instância.  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 Não é possível modificar um registro de instância.  
  
 [LOCALDB_ERROR_CANNOT_CREATE_SQL_PROCESS](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-create-sql-process.md)  
 Não é possível criar um processo para o SQL Server.  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 Um processo do SQL Server foi iniciado, mas houve falha na inicialização do SQL Server.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Uma configuração de instância foi corrompida.  
  
 [LOCALDB_ERROR_AUTO_INSTANCE_CREATE_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-auto-instance-create-failed.md)  
 Não é possível criar uma instância automática. Consulte o log de eventos de Aplicativo do Windows para obter detalhes sobre o erro.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Erro inesperado. Consulte o log de eventos para obter detalhes.  
  
## <a name="details"></a>Detalhes  
 O argumento do buffer de conexão (*wszSqlConnection*) e o argumento do tamanho do buffer de conexão (*lpcchSqlConnection*) são opcionais. A tabela a seguir mostra opções para o uso desses argumentos e seus resultados.  
  
|Buffer|Tamanho do buffer|Fundamento|Ação|  
|------------|-----------------|---------------|------------|  
|NULL|NULL|O usuário deseja iniciar a instância e não precisa de um nome de pipe.|Inicia uma instância (sem retorno de pipe e sem retorno do tamanho de buffer necessário).|  
|NULL|Presente|O usuário solicita o tamanho do buffer de saída. (Na próxima chamada, o usuário provavelmente solicitará uma inicialização real.)|Retorna um tamanho de buffer necessário (sem inicialização e sem retorno de pipe). O resultado é S_OK.|  
|Presente|NULL|Não permitido; entrada incorreta.|O resultado retornado é LOCALDB_ERROR_INVALID_PARAMETER.|  
|Presente|Presente|O usuário deseja iniciar a instância e precisa do nome do pipe para se conectar a ela após a inicialização.|Verifica o tamanho do buffer, inicia a instância e retorna o nome do pipe no buffer. <br />O argumento de tamanho do buffer retorna o comprimento da cadeia de caracteres “server=”, sem incluir caracteres nulos de terminação.|  
  
 Para obter uma amostra do código que usa a API LocalDB, consulte [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
