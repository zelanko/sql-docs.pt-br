---
title: Método ListInstalledSharePointVersions (WMI) | Microsoft Docs
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
- ListInstalledSharePointVersions method
ms.assetid: 8f0a5e9f-23f1-41e5-9a90-dfec19ef1df7
caps.latest.revision: 13
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 7d84b3ce6a3277c6dc0eb51321e4e071c6d76f14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007431"
---
# <a name="listinstalledsharepointversions-method-wmi"></a>Método ListInstalledSharePointVersions (WMI)
  Retorna um conjunto de tokens que representam as versões do Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que estão instaladas no mesmo computador que o servidor de relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub ListInstalledSharePointVersions(ByRef VersionTokens() _  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] VersionTokens,   
    out Int32 Length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *VersionTokens[]*  
 [fora] Uma matriz que contém os tokens que representam a versão de um produto do SharePoint ou tecnologia que é compatível com o servidor de relatório instalado.  
  
 *Comprimento*  
 [fora] O tamanho da matriz de tokens da versão.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Remarks  
 Cada token retornado representa uma versão do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] ou [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] que é compatível com o servidor de relatório atualmente instalado. Se uma versão específica do SharePoint for compatível com versões anteriores do SharePoint, serão retornados tokens de cada versão compatível do SharePoint.  
  
 A seguir é apresentada uma tabela dos tokens do SharePoint que são retornados.  
  
|**Tokens da versão**|**Descrição**|  
|------------------------|---------------------|  
|WSS_V2_Compatible|É executada uma instalação do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] , que é compatível com o [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 2.0.|  
|WSS_V3_Compatible|É executada uma instalação do [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que é compatível com o [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0.|  
|WSS_V4_Compatible|É executada uma instalação do [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que é compatível com o Office 14.|  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  