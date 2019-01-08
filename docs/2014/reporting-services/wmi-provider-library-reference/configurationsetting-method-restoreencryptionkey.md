---
title: Método RestoreEncryptionKey (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- RestoreEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- RestoreEncryptionKey method
ms.assetid: 37e949f5-15af-4858-848a-f482ee94fcd9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: acdd99c590f05fbe21777416dcd56234a6a797d0
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417437"
---
# <a name="restoreencryptionkey-method-wmi-msreportserverconfigurationsetting"></a>Método RestoreEncryptionKey (WMI MSReportServer_ConfigurationSetting)
  Reaplica a chave de criptografia especificada para o banco de dados do servidor de relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub RestoreEncryptionKey(ByRef KeyFile() As Integer, _  
    ByRef Length As Int32, ByVal Password As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void RestoreEncryptionKey(out Byte[] KeyFile, out Int32 Length,   
            string Password, out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *KeyFile[]*  
 [fora] Uma matriz que contém a chave de criptografia criptografada.  
  
 *Comprimento*  
 [fora] O tamanho da matriz retornada pelo método.  
  
 *Senha*  
 Uma cadeia de caracteres usada para criptografar a chave de criptografia.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
 *ExtendedErrors[]*  
 [fora] Uma matriz de cadeia de caracteres que contém erros adicionais retornados pela chamada.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 Se uma entrada já existir para o servidor de relatório no banco de dados do servidor de relatório, ela será excluída. A nova entrada será criada com a chave de criptografia especificada e a chave pública do servidor de relatório.  
  
 O método é mais efetivo quando chamado após o método [DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md) , que desmarca a lista de chaves de criptografia.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
