---
title: Método RemoveURL (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- RemoveURL method
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
caps.latest.revision: 13
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: a847215e1870a7d93ee7f741c06bf9f9dcca5d65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130905"
---
# <a name="removeurl-method-wmi-msreportserverconfigurationsetting"></a>Método RemoveURL (WMI MSReportServer_ConfigurationSetting)
  Remove uma URL reservada para o servidor de relatório. Se houver várias URLs a serem removidas, isso deverá ser feito individualmente chamando-se esta API.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub RemoveURL(ByVal Application As String, _  
    ByVal UrlString As String, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveURL(string Application, string UrlString, int Lcid,   
    out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Aplicativo*  
 O nome do aplicativo do qual remover a reserva.  
  
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
 *UrlString* não inclui o nome do Diretório Virtual – o método [SetVirtualDirectory Method &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md) é fornecido para essa finalidade.  
  
 Antes de chamar o [ReserveURL](configurationsetting-method-reserveurl.md) método, você deve fornecer um valor para a propriedade de configuração VirtualDirectory o *aplicativo* parâmetro. Use o método [SetVirtualDirectory Method &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md) para definir a propriedade VirtualDirectory.  
  
 Se um Certificado SSL foi fornecido por [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e nenhuma outra URL precisar dele, ele será removido.  
  
 Este método faz com que todos os domínios de aplicativo sem-configuração façam uma reciclagem e parem de funcionar durante esta operação; os domínios de aplicativo são reiniciados após o término da operação.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  