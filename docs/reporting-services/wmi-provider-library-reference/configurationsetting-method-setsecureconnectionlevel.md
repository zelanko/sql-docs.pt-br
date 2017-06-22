---
title: "Método SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 219112996b6fd0c2fb1cb6eff5baca29b65e86d2
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="configurationsetting-method---setsecureconnectionlevel"></a>Método ConfigurationSetting - SetSecureConnectionLevel
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
  
## <a name="parameters"></a>Parâmetros  
 *Nível*  
 Um valor de inteiro que representa um nível de conexão segura.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 Quando chamada, a propriedade SecureConnectionLevel do servidor de relatório será definida como o valor especificado. Um valor de 0 indica que o SSL está desativado. Um valor maior que ou igual a 1indica que o SSL está ligado.  
  
-   Quando o valor for definido, o elemento SecureConnectionLevel no arquivo de configuração do servidor de relatório será alterado e o elemento **URLRoot** no arquivo de configuração será definido para usar “https://” se *Level* especificado for maior, ou igual a 1 ou “http://” se *Level* especificado for 0.  
  
 Em [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], transforma-se SecureConnectionLevel em uma opção ativado/desativado, cujo valor padrão é 0. Para qualquer valor maior ou igual a 1 passado pela API de método de SetSecureConnectionLevel, o SSL é considerado ativado e a propriedade de configuração SecureConnectionLevel é definida de forma condizente no arquivo rsreportserver.config. Os valores 2 e 3 ainda são permitidos para compatibilidade com versões anteriores.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
