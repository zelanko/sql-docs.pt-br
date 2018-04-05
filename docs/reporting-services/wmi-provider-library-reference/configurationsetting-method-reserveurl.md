---
title: Método ReserveURL (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ReservedURL method
ms.assetid: b9008a62-3edd-4f8a-99f2-7598c2133899
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f94910ca666c8a48c68921895723d6da004b742f
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---reserveurl"></a>Método de ConfigurationSetting – ReserveURL
  Adiciona uma reserva de URL para um determinado aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub ReserveURL(Application as String, _  
    UrlString as String, Lcid as Int32, _   
    ByRef [Error] as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ReserveURL(string Application, string UrlString, int Lcid,   
    out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Aplicativo*  
 O nome do aplicativo para o qual reservar a URL.  
  
 *URLString*  
 A URL para a reserva.  
  
 *lcid*  
 A localidade a ser usada para as mensagens de erro retornadas.  
  
 *Erro*  
 [fora] A descrição do erro ocorrido.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## <a name="remarks"></a>Remarks  
 *UrlString* não inclui o nome do diretório virtual. O método [SetVirtualDirectory](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) é disponibilizado para essa finalidade.  
  
 As reservas de URL são criadas para a conta atual de serviço do Windows. Para alterar a conta de serviço do Windows, é necessário atualizar todas as reservas de URL manualmente.  
  
 Este método faz com que todos os domínios de aplicativo façam uma reciclagem agressiva. Os domínios de aplicativo são reiniciados após o término desta operação.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
