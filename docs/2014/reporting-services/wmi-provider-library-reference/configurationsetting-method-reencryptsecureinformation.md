---
title: Método ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: faf998f4d9d3cbd3c45de4c1a0b214ba1de2152e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62646824"
---
# <a name="reencryptsecureinformation-method-wmi-msreportserverconfigurationsetting"></a>Método ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting)
  Gera uma nova chave de criptografia e criptografa novamente todas as informações seguras no catálogo usando essa nova chave.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub ReencryptSecureInformation(ByRef HRESULT as Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ReencryptSecureInformation (out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parâmetros  
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
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
