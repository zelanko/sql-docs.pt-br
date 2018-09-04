---
title: Método RemoveURL (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- RemoveURL method
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 415b3ecf57bf6fba36ffd10bcb6db2deebebf6f6
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43282337"
---
# <a name="configurationsetting-method---removeurl"></a>Método de ConfigurationSetting – RemoveURL
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
 *UrlString* não inclui o nome do Diretório Virtual – o método [SetVirtualDirectory Method &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) é fornecido para essa finalidade.  
  
 Antes de chamar o método [ReserveURL](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md) , forneça um valor para a propriedade de configuração VirtualDirectory do parâmetro *Application* . Use o método [SetVirtualDirectory Method &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) para definir a propriedade VirtualDirectory.  
  
 Se um Certificado SSL foi fornecido por [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e nenhuma outra URL precisar dele, ele será removido.  
  
 Este método faz com que todos os domínios de aplicativo sem-configuração façam uma reciclagem e parem de funcionar durante esta operação; os domínios de aplicativo são reiniciados após o término da operação.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
