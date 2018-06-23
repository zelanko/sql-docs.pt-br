---
title: Método ReserveURL (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ReservedURL method
ms.assetid: b9008a62-3edd-4f8a-99f2-7598c2133899
caps.latest.revision: 14
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 1cd5ef5a1e4a29b70d742e858a30ab9912cce6bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121632"
---
# <a name="reserveurl-method-wmi-msreportserverconfigurationsetting"></a>Método ReserveURL (WMI MSReportServer_ConfigurationSetting)
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
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## <a name="remarks"></a>Remarks  
 *UrlString* não inclui o nome do diretório virtual. O [SetVirtualDirectory](configurationsetting-method-setvirtualdirectory.md) método é fornecido para essa finalidade.  
  
 As reservas de URL são criadas para a conta atual de serviço do Windows. Para alterar a conta de serviço do Windows, é necessário atualizar todas as reservas de URL manualmente.  
  
 Este método faz com que todos os domínios de aplicativo façam uma reciclagem agressiva. Os domínios de aplicativo são reiniciados após o término desta operação.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  