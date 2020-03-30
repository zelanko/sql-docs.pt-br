---
title: Método ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4b88e5006ab772d232f65016033738c0b46848c9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65579895"
---
# <a name="configurationsetting-method---listreportserversindatabase"></a>Método de ConfigurationSetting – ListReportServersInDatabase
  Retorna a lista de instalações do servidor de relatório que estão presentes no banco de dados do servidor de relatório, independentemente de essas instalações terem acesso a informações seguras.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub ListReportServersInDatabase(ByRef MachineNames() As String, _  
    ByRef InstanceNames() As String, ByRef InstallationIDs() As String, _  
    ByRef IsInitialized() As Boolean, ByRef Length As Int32, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] MachineNames,   
    out string[] InstanceNames, out string[] InstallationIDs,   
    out Boolean[] IsInitialized,out Int32 Length, out Int32 HRESULT,    
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>parâmetros  
 *MachineNames[]*  
 [fora] Uma matriz que contém os nomes de máquina das instalações do servidor de relatório no banco de dados.  
  
 *InstanceNames[]*  
 [fora] Uma matriz que contém os nomes de instância de cada instalação do servidor de relatório no banco de dados.  
  
 *InstallationIDs[]*  
 [fora] Uma matriz que contém as IDs de instalação de cada instalação de servidor de relatório do banco de dados.  
  
 *IsInitialized[]*  
 [fora] Uma matriz que contém o status de inicialização de cada instalação de servidor de relatório do banco de dados.  
  
 *Comprimento*  
 [fora] O tamanho das matrizes retornadas pelo método. Todas as matrizes retornadas têm o mesmo tamanho.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
 *ExtendedErrors[]*  
 [fora] Uma matriz de cadeia de caracteres que contém erros adicionais retornados pela chamada.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 O ListReportServersInDatabase lista as instalações do servidor de relatório que estão presentes no banco de dados do servidor de relatório, independentemente de terem acesso a informações seguras e retorna um conjunto de matrizes correspondentes contendo informações sobre cada instalação.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
