---
title: "Método GetDatabaseVersionDisplayName (WMI) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GetDatabaseVersionDisplayName method
ms.assetid: e1286424-7043-4f12-a7ad-1cf69e81baa4
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b4743439f2edf3f3cfb253aa981af83350f5aff7
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="configurationsetting-method---getdatabaseversiondisplayname"></a>Método ConfigurationSetting - GetDatabaseVersionDisplayName
  Obtém o nome para exibição para uma determinada cadeia de caracteres da versão do banco de dados do servidor de relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub GetDatabaseVersionDisplayName(Version As String, DisplayName As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetDatabaseVersionDisplayName(string Version, string DisplayName, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Versão*  
 Uma cadeia de caracteres que contém a cadeia de caracteres de versão para um banco de dados do servidor de relatório.  
  
 *DisplayName*  
 [fora] Uma cadeia de caracteres que contém o nome para exibição que corresponde à versão fornecida.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir mostra o mapeamento da versão do banco de dados para exibir a cadeia de caracteres.  
  
|**Versão**|**Versão**|**Nome de Exibição**|  
|-----------------|-----------------|----------------------|  
|RS 2005 SP2|@DBVersion= 'C.0.8.54'|SQL Server 2005 SP2|  
|RS 2005 SP1|@DBVersion= 'C.0.8.43'|SQL Server 2005 SP1|  
|RS 2005 RTM|@DBVersion= 'C.0.8.40'|SQL Server 2005|  
|RS 2000 SP2|@DBVersion= '0.6.54'|SQL Server 2000 SP2|  
|RS 2000 SP1|@DBVersion= 'C.0.6.51'|SQL Server 2000 SP1|  
|RS 2000 RTM|@DBVersion= 'C.0.6.43'|SQL Server 2000|  
|Hotfix||Versão mais próxima aplicável|  
  
 Para uma *Versão* anterior ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000, é retornado um HRESULT de ACT_E_BAD_VERSION.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
