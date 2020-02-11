---
title: Método SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ede290f794ab61dac62c39bc47b80516385474fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097962"
---
# <a name="setsecureconnectionlevel-method-wmi-msreportserver_configurationsetting"></a>Método SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting)
  Define o nível de conexão segura do servidor de relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub SetSecureConnectionLevel(Level as Integer, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Int32 Level,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>parâmetros  
 *Nível*  
 Um valor de inteiro que representa um nível de conexão segura.  
  
 *RESULTADO*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 Quando chamada, a propriedade SecureConnectionLevel do servidor de relatório será definida como o valor especificado. Um valor de 0 indica que o SSL está desativado. Um valor maior que ou igual a 1indica que o SSL está ligado.  
  
-   Quando o valor é definido, o elemento SecureConnectionLevel no arquivo de configuração do servidor de relatório é alterado e `URLRoot` o elemento no arquivo de configuração é definido para usar "https://" se o *nível* especificado for maior ou igual a 1, ou "http://" se o *nível* especificado for 0.  
  
 Em [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], transforma-se SecureConnectionLevel em uma opção ativado/desativado, cujo valor padrão é 0. Para qualquer valor maior ou igual a 1 passado pela API de método de SetSecureConnectionLevel, o SSL é considerado ativado e a propriedade de configuração SecureConnectionLevel é definida de forma condizente no arquivo rsreportserver.config. Os valores 2 e 3 ainda são permitidos para compatibilidade com versões anteriores.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
