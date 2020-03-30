---
title: Método ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 84265b1a72d93a2d8de8332e0309093a9a506ea0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65571437"
---
# <a name="configurationsetting-method---reencryptsecureinformation"></a>Método de ConfigurationSetting – ReencryptSecureInformation
  Gera uma nova chave de criptografia e criptografa novamente todas as informações seguras no catálogo usando essa nova chave.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub ReencryptSecureInformation(ByRef HRESULT as Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ReencryptSecureInformation (out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>parâmetros  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
 *ExtendedErrors[]*  
 [fora] Uma matriz de cadeia de caracteres que contém erros adicionais retornados pela chamada.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 O método ReencryptSecureInformation permite que o administrador substitua a chave de criptografia existente com uma chave nova.  
  
 Quando esse método é chamado, o servidor de relatório gera uma nova chave de criptografia e itera por meio de todo o conteúdo criptografado para criptografá-lo novamente com a nova chave de criptografia.  
  
 As extensões de entrega podem armazenar informações seguras em suas estruturas de configurações de entrega. Quando o ReencryptSecureInformation é chamado, o servidor de relatório carrega cada assinatura e a extensão de entrega correspondente para criptografar novamente as informações armazenadas nas configurações associadas.  
  
 Se esse método for executado em um computador em uma implantação de expansão, cada computador na implantação de expansão precisará ser inicializado novamente.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
