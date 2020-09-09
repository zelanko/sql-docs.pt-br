---
description: Função LocalDBGetVersionInfo
title: Função LocalDBGetVersionInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBGetVersionInfo
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6776f1ce1d5cb92bba4d570a53c95f351b501960
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542924"
---
# <a name="localdbgetversioninfo-function"></a>Função LocalDBGetVersionInfo
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Retorna informações sobre a versão de LocalDB do SQL Server Express especificada, como se existe ou não, e o número da versão total do LocalDB (incluindo números de versão e compilação).  
  
 As informações são retornadas na forma de um **struct** chamado **LocalDBVersionInfo**, que tem a definição a seguir.  
  
```  
typedef struct _LocalDBVersionInfo  
{  
      // Contains the size of the LocalDBVersionInfo struct  
      DWORD  cbLocalDBVersionInfoSize;  
  
      // Holds the version name  
      TLocalDBVersionwszVersion;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
} LocalDBVersionInfo;  
  
```  
  
 **Arquivo de cabeçalho:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT LocalDBGetVersionInfo(  
           PCWSTR wszVersionName,           PLocalDBVersionInfo pVersionInfo,           DWORD dwVersionInfoSize);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *wszVersionName*  
 [Entrada] O nome de versão de LocalDB.  
  
 *pVersionInfo*  
 [Saída] O buffer para armazenar as informações sobre a versão de LocalDB.  
  
 *dwVersionInfoSize*  
 Entrada Mantém o tamanho do buffer *VERSIONINFO* .  
  
## <a name="returns"></a>Retornos  
 S_OK  
 A função foi bem-sucedida.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 O LocalDB do SQL Server Express não está instalado no computador.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Um ou mais parâmetros de entrada especificados são inválidos.  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-version.md)  
 A versão de LocalDB especificada não existe.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Erro inesperado. Consulte o log de eventos para obter detalhes.  
  
## <a name="details"></a>Detalhes  
 A lógica por trás da introdução do argumento de tamanho de **struct** (*lpVersionInfoSize*) é permitir que a API retorne versões diferentes do **LocalDBVersionInfostruct**, habilitando efetivamente a compatibilidade com versões posteriores e anteriores.  
  
 Se o argumento de tamanho de **struct** (*lpVersionInfoSize*) corresponder ao tamanho de uma versão conhecida do **LocalDBVersionInfostruct**, essa versão do **struct** será retornada. Caso contrário, LOCALDB_ERROR_INVALID_PARAMETER será retornado.  
  
 Um exemplo típico de uso da API **LocalDBGetVersionInfo** é semelhante ao seguinte:  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>Comentários  
 Para obter uma amostra do código que usa a API LocalDB, consulte [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
