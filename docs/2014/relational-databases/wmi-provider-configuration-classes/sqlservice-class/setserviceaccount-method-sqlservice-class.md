---
title: Método SetServiceAccount (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- SetServiceAccount Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 363859fb4b1a680ff8f665a552bf4373fdc8adeb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063177"
---
# <a name="setserviceaccount-method-sqlservice-class"></a>Método SetServiceAccount (classe SqlService)
  Tenta alterar o nome de usuário e senha com os quais o serviço é executado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetServiceAccount(  
ServiceStartName , ServiceStartPassword  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
#### <a name="parameters"></a>Parâmetros  
 *ServiceStartName*  
 Um valor da cadeia de caracteres que especifica o nome de conta com a qual o serviço é executado. Dependendo do tipo de serviço, o nome da conta pode estar no formulário de DomainName\Username. Quando for executado, o processo de serviço será registrado usando-se um dos dois formulários:  
  
-   Se a conta pertencer ao domínio interno, \Username poderá ser especificado.  
  
-   Se NULL for especificado, o serviço será registrado como o **LocalSystem** conta.  
  
 Para drivers de nível de sistema ou núcleo *StartName* contém o nome de objeto do driver, \FileSystem\Rdr ou \Driver\Xns, que o sistema de e/s usa para carregar o driver de dispositivo. Se NULL for especificado, o driver será executado com o nome do objeto padrão criado pelo sistema de E/S com base no nome do serviço, por exemplo DWDOM\Admin.  
  
 *ServiceStartPassword*  
 Um valor de cadeia de caracteres que especifica a senha para o nome da conta de *StartName* parâmetro. Especifique NULL se você não estiver alterando a senha. Especifique uma cadeia de caracteres vazia se o serviço não tiver nenhuma senha.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito ou 1 se a solicitação não tiver suporte. Qualquer outro número indica um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
