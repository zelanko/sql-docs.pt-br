---
title: Método SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8365b0718f389e6417f8f7e1a76cf403e268b574
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48081816"
---
# <a name="setemailconfiguration-method-wmi-msreportserverconfigurationsetting"></a>Método SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting)
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
  
## <a name="remarks"></a>Comentários  
 Quando o *SendUsingSMTPServer* parâmetro for definido como `true`, o **SendUsing** entrada no arquivo de configuração do servidor de relatório é definida como 1. Quando *SendUsingSMTPServer* é definido como `false`, o **SendUsing** entrada não está configurada.  
  
 Esse método não fornece um modo de os usuários definirem a entrada **SendUsing** no arquivo de configuração do servidor de relatório para um valor diferente de 1. Para configurar o servidor de relatório para algo diferente de e-mail SMTP, você deverá editar o arquivo de configuração manualmente.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
