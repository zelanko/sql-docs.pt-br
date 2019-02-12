---
title: Método ListIPAddresses (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListIPAddresses method
ms.assetid: 7e7cf182-fba0-4604-a474-098461e23e9d
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1c6854194122dbc4ab5e1781ea62de119f7a09e9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56029047"
---
# <a name="listipaddresses-method-wmi-msreportserverconfigurationsetting"></a>Método ListIPAddresses (WMI MSReportServer_ConfigurationSetting)
  Lista os endereços IP do computador do servidor de relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub ListIPAddresses (ByRef IPAddress() as String, _  
    ByRef IPVersion()as String, ByRef IsDhcpEnabled () as Boolean, _   
    ByRef Length as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListIPAddresses (out string[] IPAddress,   
    out string[] IPVersion, out bool[] isDhcpEnabled, out int length,   
    out int HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *IPAddress[]*  
 [fora] A lista de endereços IP do computador.  
  
 *IPVersion[]*  
 [out] A versão dos endereços IP.  
  
 *IsDhcpEnabled[]*  
 [fora] Indica se os endereços IP são habilitados por DHCP.  
  
 *Comprimento*  
 [fora] O tamanho da matriz retornada pelo método.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## <a name="remarks"></a>Comentários  
 As cadeias de caracteres*IPVersion* são V4, V6.  
  
 Se *IsDhcpEnabled* é `True`, o *IPAddress* é dinâmico. Não deve ser usado para associações SSL.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
