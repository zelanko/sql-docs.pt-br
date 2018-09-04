---
title: Método SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 72223544c4fc461f99413658df5ae15b5404b0b5
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43279118"
---
# <a name="configurationsetting-method---setemailconfiguration"></a>Método de ConfigurationSetting – SetEmailConfiguration
  Configura a extensão de entrega de email usada pelo servidor de relatório para enviar email.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub SetEmailConfiguration(ByVal SendUsingSMTPServer As Boolean, _  
    ByVal SMTPServer As String, ByVal SenderEmailAddress As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetEmailConfiguration (Boolean SendUsingSMTPServer,   
   string SMTPServer, string SenderEmailAddress,   
   out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *SendUsingSMTPServer*  
 Um valor Booleano que indica se o servidor deve usar o servidor SMTP para enviar email. Este valor só pode ser definido como true. O valor padrão é false.  
  
 *SMTPServer*  
 Uma cadeia de caracteres que contém o nome ou o endereço IP de um servidor SMTP.  
  
 *SenderEmailAddress*  
 O endereço de email usado no campo 'De:' nos emails enviados do servidor de relatório.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Remarks  
 Quando o parâmetro *SendUsingSMTPServer* for definido como **true**, a entrada **SendUsing** no arquivo de configuração do servidor de relatório será definida como 1. Quando *SendUsingSMTPServer* é definido como **false**, a entrada **SendUsing** não está configurada.  
  
 Esse método não fornece um modo de os usuários definirem a entrada **SendUsing** no arquivo de configuração do servidor de relatório para um valor diferente de 1. Para configurar o servidor de relatório para algo diferente de e-mail SMTP, você deverá editar o arquivo de configuração manualmente.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
