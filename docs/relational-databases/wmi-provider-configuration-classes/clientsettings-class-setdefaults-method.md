---
title: Método SetDefaults (classe ClientSettings) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ClientSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 056508f3-a5c8-467c-a196-dc1ef1f5178f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b2b079d70a8fb70a2b28c139a862f0689bd33d5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072488"
---
# <a name="clientsettings-class---setdefaults-method"></a>Classe ClientSettings – Método SetDefaults
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Define todos os valores padrão para a instância do cliente do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a opção de substituir dados existentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto **ClientSettings** que representa uma instância de cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*OverwriteAll*|Um valor booliano, que especifica se deve-se substituir valores existentes na instância do cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **true** para substituir dados existentes, ou **false** , se os dados existentes não precisarem ser substituídos.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor de retorno  
 Um valor **uint32** , que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
