---
title: Função LocalDBFormatMessage | Microsoft Docs
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
- LocalDBFormatMessage
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c787218996e72c3953243f24fb103ccaa8879720
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="localdbformatmessage-function"></a>Função LocalDBFormatMessage
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Retorna a descrição textual localizada para o erro de LocalDB do SQL Server Express especificado.  
  
 **Arquivo de cabeçalho:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT LocalDBFormatMessage(  
           HRESULT hrLocalDB,  
           DWORD dwFlags,   
           DWORD dwLanguageId,   
           LPWSTR wszMessage,   
           LPDWORD lpcchMessage   
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *hrLocalDB*  
 [Entrada] O código de erro de LocalDB.  
  
 *dwFlags*  
 [Entrada] Os sinalizadores que especificam o comportamento desta função.  
  
 Sinalizadores disponíveis:  
  
 LOCALDB_TRUNCATE_ERR_MESSAGE  
 Se o buffer de entrada for muito curto, a mensagem de erro será truncada para ajustar o buffer.  
  
 *dwLanguageId*  
 [Entrada] O idioma desejado (LANGID) ou 0, nesse caso, a ordem do idioma de Win32 FormatMessage é usada.  
  
 *wszMessage*  
 [Saída] O buffer para armazenar a mensagem de erro de LocalDB.  
  
 *lpcchMessage*  
 [Entrada/Saída] Na entrada contém o tamanho do buffer *wszMessage* em caracteres. Na saída, se o tamanho de buffer especificado for muito pequeno, conterá o tamanho de buffer necessário em caracteres, incluindo quaisquer caracteres nulos à esquerda. Se a função tiver sucesso, ela conterá o número de caracteres na mensagem, excluindo os caracteres nulos à direita.  
  
## <a name="returns"></a>Retorna  
 S_OK  
 A função foi bem-sucedida.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 O LocalDB do SQL Server Express não está instalado no computador.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Um ou mais parâmetros de entrada especificados são inválidos.  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 A mensagem solicitada não existe.  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 A mensagem não está disponível no idioma solicitado.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 O buffer de entrada *wszMessage* é muito curto e o truncamento não foi solicitado.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Erro inesperado. Consulte o log de eventos para obter detalhes.  
  
## <a name="remarks"></a>Remarks  
 Para obter uma amostra do código que usa a API LocalDB, consulte [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
