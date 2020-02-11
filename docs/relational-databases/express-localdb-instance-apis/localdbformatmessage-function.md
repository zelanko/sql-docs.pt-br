---
title: Função LocalDBFormatMessage | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBFormatMessage
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d5aa59cdb3b1c59b78a0ef99fb7d375275d370e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091217"
---
# <a name="localdbformatmessage-function"></a>Função LocalDBFormatMessage
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Retorna a descrição textual localizada para o erro de LocalDB do SQL Server Express especificado.  
  
 **Arquivo de cabeçalho:** sqlncli. h  
  
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
  
## <a name="parameters"></a>parâmetros  
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
  
## <a name="returns"></a>Retornos  
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
  
## <a name="remarks"></a>Comentários  
 Para obter uma amostra do código que usa a API LocalDB, consulte [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
