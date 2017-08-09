---
title: "Método ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2bdc6ca4ca42bc8c66ebfbb292dff8c022e3cdf2
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---listreportserversindatabase"></a>Método ConfigurationSetting - ListReportServersInDatabase
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
  
## <a name="parameters"></a>Parâmetros  
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
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Comentários  
 O ListReportServersInDatabase lista as instalações do servidor de relatório que estão presentes no banco de dados do servidor de relatório, independentemente de terem acesso a informações seguras e retorna um conjunto de matrizes correspondentes contendo informações sobre cada instalação.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
