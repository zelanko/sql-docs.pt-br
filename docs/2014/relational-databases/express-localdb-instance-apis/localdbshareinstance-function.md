---
title: Função LocalDBShareInstance | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- LocalDBShareInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 21eb3b9a-7d32-455b-89bb-f624198cd202
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f821bcc914846bf62fdc4640b976855226a0922d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006608"
---
# <a name="localdbshareinstance-function"></a>Função LocalDBShareInstance
  Compartilha a instância especificada do LocalDB do SQL Server Express com outros usuários do computador, usando o nome compartilhado especificado.  
  
 **Arquivo de cabeçalho:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT LocalDBShareInstance(  
           PSID pOwnerSID,  
           PCWSTR pInstancePrivateName,  
           PCWSTR pInstanceSharedName,   
           DWORD dwFlags   
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *pOwnerSID*  
 [Entrada] O SID do proprietário da instância.  
  
 *pInstancePrivateName*  
 [Entrada] O nome privado da instância de LocalDB a ser compartilhada.  
  
 *pInstanceSharedName*  
 [Entrada] O nome compartilhado da instância de LocalDB a ser compartilhada.  
  
 *dwFlags*  
 [Entrada] Reservado para uso futuro. Atualmente deve ser definido como 0.  
  
## <a name="returns"></a>Retorna  
 S_OK  
 A função foi bem-sucedida.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 O LocalDB do SQL Server Express não está instalado no computador.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Um ou mais parâmetros de entrada especificados são inválidos.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 O nome de instância especificado é inválido.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../express-localdb-error-messages/localdb-error-unknown-instance.md)  
 A instância especificada não existe.  
  
 [LOCALDB_ERROR_ADMIN_RIGHTS_REQUIRED](../express-localdb-error-messages/localdb-error-admin-rights-required.md)  
 É preciso ter privilégios de administrador para executar esta operação.  
  
 [LOCALDB_ERROR_SHARED_NAME_TAKEN](../express-localdb-error-messages/localdb-error-shared-name-taken.md)  
 O nome compartilhado especificado já está sendo utilizado.  
  
 [LOCALDB_ERROR_INSTANCE_ALREADY_SHARED](../express-localdb-error-messages/localdb-error-instance-already-shared.md)  
 A instância especificada já está compartilhada.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 Erro inesperado. Consulte o log de eventos para obter detalhes.  
  
## <a name="remarks"></a>Remarks  
 Para obter uma amostra do código que usa a API LocalDB, consulte [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](sql-server-express-localdb-header-and-version-information.md)  
  
  