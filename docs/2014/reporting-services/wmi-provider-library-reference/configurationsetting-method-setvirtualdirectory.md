---
title: Método SetVirtualDirectory (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SetVirtualDirectory method
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e68bb7c70d08fb07d3079436fafe5fd61ae104f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097915"
---
# <a name="setvirtualdirectory-method-wmi-msreportserverconfigurationsetting"></a>Método SetVirtualDirectory (WMI MSReportServer_ConfigurationSetting)
  Define o nome do diretório virtual de um dado aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub SetVirtualDirectory(ByVal Application As String, _  
    ByVal VirtualDirectory As String, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetVirtualDirectory(string Application, string VirtualDirectory,   
       int Lcid,out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Aplicativo*  
 O nome do aplicativo para o qual é necessário definir o diretório virtual.  
  
 *VirtualDirectory*  
 O nome do diretório virtual.  
  
 *lcid*  
 A identificação de localidade do diretório virtual.  
  
 *Erro*  
 [fora] A descrição do erro ocorrido.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método foi bem-sucedida; um código de erro indica que a chamada não foi bem-sucedida.  
  
## <a name="remarks"></a>Comentários  
 Um aplicativo pode ter somente um nome de diretório virtual para todas as reservas de URL.  
  
 VirtualDirectory deve seguir as convenções de nomenclatura para diretórios virtuais. VirtualDirectory não pode ser uma cadeia de caracteres vazia nem ficar em branco.  
  
 Atualiza o valor do elemento \Configuration\URLReservations\Application\VirtualDirectory. É bem-sucedido mesmo que nenhuma reserva de URL tenha sido criada.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
