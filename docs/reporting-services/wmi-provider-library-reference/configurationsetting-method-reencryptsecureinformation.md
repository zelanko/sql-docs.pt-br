---
title: "Método ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
- ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e7b57564600c568095ec999cf1db805437f8e630
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---reencryptsecureinformation"></a>Método ConfigurationSetting - ReencryptSecureInformation
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
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 O método ReencryptSecureInformation permite que o administrador substitua a chave de criptografia existente com uma chave nova.  
  
 Quando esse método é chamado, o servidor de relatório gera uma nova chave de criptografia e itera por meio de todo o conteúdo criptografado para criptografá-lo novamente com a nova chave de criptografia.  
  
 As extensões de entrega podem armazenar informações seguras em suas estruturas de configurações de entrega. Quando o ReencryptSecureInformation é chamado, o servidor de relatório carrega cada assinatura e a extensão de entrega correspondente para criptografar novamente as informações armazenadas nas configurações associadas.  
  
 Se esse método for executado em um computador em uma implantação de expansão, cada computador na implantação de expansão precisará ser inicializado novamente.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
