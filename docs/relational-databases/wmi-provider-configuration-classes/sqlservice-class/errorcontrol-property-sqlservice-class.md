---
title: Propriedade ErrorControl (classe SqlService) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ErrorControl Property (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 58f1064b96d21a6361d122fc5c92f945bea46dce
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="errorcontrol-property-sqlservice-class"></a>Propriedade ErrorControl (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Obtém ou define a gravidade do erro se o serviço falhar durante a inicialização.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
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
  
  
