---
title: Método SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
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
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 142fd8bf2116d4cc672aeb607938ea8c1c73bf8a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097992"
---
# <a name="setemailconfiguration-method-wmi-msreportserver_configurationsetting"></a>Método SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting)
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
  
## <a name="parameters"></a>parâmetros  
 *SendUsingSMTPServer*  
 Um valor Booleano que indica se o servidor deve usar o servidor SMTP para enviar email. Este valor só pode ser definido como true. O valor padrão é falso.  
  
 *SMTPServer*  
 Uma cadeia de caracteres que contém o nome ou o endereço IP de um servidor SMTP.  
  
 *SenderEmailAddress*  
 O endereço de email usado no campo 'De:' nos emails enviados do servidor de relatório.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 Quando o parâmetro *SendUsingSMTPServer* é definido como `true`, a entrada **SendUsing** no arquivo de configuração do servidor de relatório é definida como 1. Quando *SendUsingSMTPServer* é definido como `false`, a entrada **SendUsing** não é configurada.  
  
 Esse método não fornece um modo de os usuários definirem a entrada **SendUsing** no arquivo de configuração do servidor de relatório para um valor diferente de 1. Para configurar o servidor de relatório para algo diferente de e-mail SMTP, você deverá editar o arquivo de configuração manualmente.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
