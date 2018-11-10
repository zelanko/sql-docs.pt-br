---
title: Propriedade ErrorControl (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ErrorControl Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 436c26aa6fffcfc364b47cbfbc8cf3c32e145849
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217574"
---
# <a name="errorcontrol-property-sqlservice-class"></a>Propriedade ErrorControl (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém ou define a gravidade do erro se o serviço não for iniciado durante a inicialização.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor da cadeia de caracteres que especifica a gravidade de erro informada se o serviço falhar durante a inicialização. A tabela a seguir mostra os valores possíveis.  
  
 Ignorar  
 O usuário não é notificado.  
  
 Normal  
 O usuário é notificado.  
  
 Severo  
 Sistema é reiniciado com a última configuração bem-sucedida conhecida.  
  
 Crítico  
 O sistema tenta reiniciar com uma configuração adequada.  
  
 Unknown (desconhecido)  
 A gravidade é desconhecida.  
  
## <a name="remarks"></a>Comentários  
 O valor indicará a ação tomada pelo programa de inicialização se ocorrer uma falha. Todos os erros são anotados pelo sistema de computador.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
