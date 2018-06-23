---
title: Função LocalDBGetVersionInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- LocalDBGetVersionInfo
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 03e8e4a07dfed1dc2430f020ad221bfb494eb41f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120794"
---
# <a name="localdbgetversioninfo-function"></a>Função LocalDBGetVersionInfo
  Retorna informações sobre a versão de LocalDB do SQL Server Express especificada, como se existe ou não, e o número da versão total do LocalDB (incluindo números de versão e compilação).  
  
 As informações são retornadas na forma de um `struct` chamado **LocalDBVersionInfo**, que tem a seguinte definição.  
  
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
 [Entrada] Mantém o tamanho do *VersionInfo* buffer.  
  
## <a name="returns"></a>Retorna  
 S_OK  
 A função foi bem-sucedida.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 O LocalDB do SQL Server Express não está instalado no computador.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Um ou mais parâmetros de entrada especificados são inválidos.  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../express-localdb-error-messages/localdb-error-unknown-version.md)  
 A versão de LocalDB especificada não existe.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 Erro inesperado. Consulte o log de eventos para obter detalhes.  
  
## <a name="details"></a>Detalhes  
 A lógica por trás da introdução do `struct` argumento de tamanho (*lpVersionInfoSize*) é permitir que a API retorne versões diferentes do **LocalDBVersionInfostruct**, efetivamente Habilitando a compatibilidade com versões anteriores e posteriores.  
  
 Se o `struct` argumento de tamanho (*lpVersionInfoSize*) corresponde ao tamanho de uma versão conhecida do **LocalDBVersionInfostruct**, essa versão do `struct` será retornado. Caso contrário, LOCALDB_ERROR_INVALID_PARAMETER será retornado.  
  
 Um exemplo típico de **LocalDBGetVersionInfo** uso da API tem esta aparência:  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L”11.0”, &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>Remarks  
 Para obter uma amostra do código que usa a API LocalDB, consulte [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](sql-server-express-localdb-header-and-version-information.md)  
  
  