---
title: Método SetValue (classe ServerSettingsGeneralFlag) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetValue Method (ServerSettingsGeneralFlag Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetValue method
ms.assetid: a889feac-c0e0-4635-b506-843863d86967
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fa86683367b35522b45d87a652c6d9d65d1c15ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63135432"
---
# <a name="setvalue-method-serversettingsgeneralflag-class"></a>Método SetValue (classe ServerSettingsGeneralFlag)
  Define todos os valores do sinalizador referenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetValue(  
Value  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe ServerSettingsGeneralFlag](serversettingsgeneralflag-class.md) que representa um sinalizador geral para as configurações de servidor.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*Value*|Um valor booliano que especifica o valor do sinalizador.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
