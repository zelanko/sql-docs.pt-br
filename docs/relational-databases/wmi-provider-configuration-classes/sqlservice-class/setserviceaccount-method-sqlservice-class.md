---
title: "Método SetServiceAccount (classe SqlService) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SetServiceAccount Method (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c0cec37d97f91da803a7d071aabfdd664878862f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="setserviceaccount-method-sqlservice-class"></a>Método SetServiceAccount (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Tentativas de alterar o nome de usuário e senha que a instância do serviço é executado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
#### <a name="parameters"></a>Parâmetros  
 *ServiceStartName*  
 Um valor da cadeia de caracteres que especifica o nome de conta com a qual o serviço é executado. Dependendo do tipo de serviço, o nome da conta pode estar no formulário de DomainName\Username. Quando for executado, o processo de serviço será registrado usando-se um dos dois formulários:  
  
-   Se a conta pertencer ao domínio interno, \Username poderá ser especificado.  
  
-   Se NULL for especificado, o serviço será registrado como o **LocalSystem** conta.  
  
 Para o kernel ou drivers em nível de sistema, *StartName* contém o nome do objeto de driver, \FileSystem\Rdr ou \Driver\Xns, que usa o sistema de e/s ao carregar o driver de dispositivo. Se NULL for especificado, o driver será executado com o nome do objeto padrão criado pelo sistema de E/S com base no nome do serviço, por exemplo DWDOM\Admin.  
  
 *ServiceStartPassword*  
 Um valor de cadeia de caracteres que especifica a senha para o nome da conta no *StartName* parâmetro. Especifique NULL se você não estiver alterando a senha. Especifique uma cadeia de caracteres vazia se o serviço não tiver nenhuma senha.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **uint32** , que é 0 se o serviço tiver sido modificado com êxito ou 1 se a solicitação não tiver suporte. Qualquer outro número indica um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
