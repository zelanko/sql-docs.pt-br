---
title: Função LocalDBStopInstance | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBStopInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 4bd73187-0aac-4f03-ac54-2b78e41917e5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 89db6e2a85e502b675db2006a682ff6b35fb4491
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022063"
---
# <a name="localdbstopinstance-function"></a>Função LocalDBStopInstance
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Interrompe a execução da instância especificada de LocalDB do SQL Server Express.  
  
 **Arquivo de cabeçalho:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT LocalDBStopInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           ULONG ulTimeout   
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *pInstanceName*  
 [Entrada] O nome da instância de LocalDB a ser interrompida.  
  
 *dwFlags*  
 [Entrada] Uma ou uma combinação dos valores de sinalizador que especificam o modo de parar a instância.  
  
 Sinalizadores disponíveis:  
  
 LOCALDB_SHUTDOWN_KILL_PROCESS  
 Desligue imediatamente usando o comando do sistema operacional de eliminar processo.  
  
 LOCALDB_SHUTDOWN_WITH_NOWAIT  
 Desligue usando a opção WITH NOWAIT do comando Transact-SQL.  
  
 Se nenhum dos sinalizadores estiver definido, a instância de LocalDB será desligada usando o comando Transact-SQL SHUTDOWN. Se ambos os sinalizadores estiverem definidos, o sinalizador LOCALDB_SHUTDOWN_KILL_PROCESS terá precedência.  
  
 *ulTimeout*  
 [Entrada] O tempo em segundos que deve ser aguardado para essa operação ser concluída. Se este valor for 0, esta função retornará imediatamente sem aguardar que a instância LocalDB pare.  
  
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
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../../relational-databases/express-localdb-error-messages/localdb-error-wait-timeout.md)  
 Tempo limite esgotado durante tentativa de obtenção de bloqueios de sincronização.  
  
 [LOCALDB_ERROR_INSTANCE_STOP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-instance-stop-failed.md)  
 A operação de interrupção não foi concluída no tempo determinado.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 O caminho em que a instância deve estar armazenada não é maior que MAX_PATH.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 Não é possível recuperar uma pasta de perfil de usuário.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 Não é possível acessar uma pasta de instância.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 Não é possível acessar um registro de instância.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Uma configuração de instância está corrompida.  
  
 [LOCALDB_ERROR_CALLER_IS_NOT_OWNER](../../relational-databases/express-localdb-error-messages/localdb-error-caller-is-not-owner.md)  
 O chamador de API não é proprietário da instância de LocalDB.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Erro inesperado. Consulte o log de eventos para obter detalhes.  
  
## <a name="remarks"></a>Comentários  
 Para obter uma amostra do código que usa a API LocalDB, consulte [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
