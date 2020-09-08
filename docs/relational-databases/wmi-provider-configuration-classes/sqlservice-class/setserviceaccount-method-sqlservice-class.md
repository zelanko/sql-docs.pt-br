---
description: Método SetServiceAccount (classe SqlService)
title: Método SetServiceAccount (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetServiceAccount Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cbd892624ec888635439d19311d9ba823ee52c98
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89519924"
---
# <a name="setserviceaccount-method-sqlservice-class"></a>Método SetServiceAccount (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Tenta alterar o nome de usuário e senha com os quais o serviço é executado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
#### <a name="parameters"></a>Parâmetros  
 *Instart*  
 Um valor da cadeia de caracteres que especifica o nome de conta com a qual o serviço é executado. Dependendo do tipo de serviço, o nome da conta pode estar no formulário de DomainName\Username. Quando for executado, o processo de serviço será registrado usando-se um dos dois formulários:  
  
-   Se a conta pertencer ao domínio interno, \Username poderá ser especificado.  
  
-   Se NULL for especificado, o serviço será conectado como a conta **LocalSystem** .  
  
 Para drivers de nível de kernel ou de sistema, o *StartName* contém o nome do objeto de driver, \FileSystem\Rdr ou \Driver\Xns, que o sistema de e/s usa para carregar o driver de dispositivo. Se NULL for especificado, o driver será executado com o nome do objeto padrão criado pelo sistema de E/S com base no nome do serviço, por exemplo DWDOM\Admin.  
  
 *ServiceStartPassword*  
 Um valor de cadeia de caracteres que especifica a senha para o nome da conta no parâmetro *StartName* . Especifique NULL se você não estiver alterando a senha. Especifique uma cadeia de caracteres vazia se o serviço não tiver nenhuma senha.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **uint32** , que é 0 se o serviço tiver sido modificado com êxito ou 1 se a solicitação não tiver suporte. Qualquer outro número indica um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
