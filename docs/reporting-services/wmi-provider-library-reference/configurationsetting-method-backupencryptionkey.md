---
title: Método BackupEncryptionKey (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- BackupEncryptionKey Method (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- BackupEncryptionKey method
ms.assetid: da1d5dae-2517-448e-96fb-5379c93222ea
caps.latest.revision: 21
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf7285b9ffc79a4ad878c3533fad6fdf757f4abf
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---backupencryptionkey"></a>Método de ConfigurationSetting – BackupEncryptionKey
  Efetua backup da chave de criptografia da instância do servidor de relatório especificada. A chave de criptografia é armazenada criptografada com uma senha.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub BackupEncryptionKey(Password as String, _  
    ByRef KeyFile() as Integer, ByRef Length as Int32, _  
    ByRef HRESULT as Int32, ByRef ExtendedErrors() as String)  
  
```  
  
```csharp  
public void BackupEncryptionKey(string Password, out Byte[] KeyFile,   
    out Int32 Length, out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Senha*  
 Uma cadeia de caracteres usada para criptografar a chave de criptografia antes de ela ser retornada.  
  
 *KeyFile[]*  
 [fora] Uma matriz que contém a chave de criptografia criptografada.  
  
 *Comprimento*  
 [fora] O tamanho da matriz retornada pelo método.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
 *ExtendedErrors[]*  
 [fora] Uma matriz de cadeia de caracteres que contém erros adicionais retornados pela chamada.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
