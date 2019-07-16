---
title: Método SetDefaults (classe CInstance) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (CInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: ed9e99c2-3e28-4ee8-bc20-61ca05984973
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2b89f082105b0723e3e9b725d2f7941502e16d04
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044324"
---
# <a name="cinstance-class---setdefaults-method"></a>Classe CInstance – Método SetDefaults
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Define todos os valores padrão para a instância do cliente do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a opção de substituir dados existentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [class CInstance](../../relational-databases/wmi-provider-configuration-classes/cinstance-class.md) que representa uma instância do cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*OverwriteAll*|Um valor booliano que especifica se é necessário substituir os valores existentes na instância das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente: **verdadeira** para substituir dados existentes, ou **false** se os dados existentes não são substituído.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor de retorno  
 Um valor **uint32** , que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
