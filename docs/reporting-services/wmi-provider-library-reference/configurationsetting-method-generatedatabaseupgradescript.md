---
title: Método GenerateDatabaseUpgradeScript (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- GenerateDatabaseUpgradeScript (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- GenerateDatabaseUpgradeScript method
ms.assetid: 88534e8e-2877-41cd-b5c2-b1d33a0fd203
caps.latest.revision: 22
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f97761fb6966de21dee53779869128b521f49840
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---generatedatabaseupgradescript"></a>Método de ConfigurationSetting – GenerateDatabaseUpgradeScript
  Gera um script que pode ser usado para atualizar o banco de dados do servidor de relatório para o esquema do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Sub GenerateDatabaseUpgradeScript(DatabaseName as String, _  
    ServerVersion as String, ByRef Script as String, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void GenerateDatabaseUpgradeScript (string DatabaseName,   
    string ServerVersion, out string Script,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Databasename*  
 Uma cadeia de caracteres que contém o nome do banco de dados do servidor de relatório a ser atualizado.  
  
 *ServerVersion*  
 Uma cadeia de caracteres que contém a versão do servidor de relatório.  
  
 *Script*  
 [fora] Uma cadeia de caracteres que contém o script SQL gerado.  
  
 *HRESULT*  
 [out] Valor que indica se a chamada obteve êxito ou falhou.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Remarks  
 O script gerado dá suporte ao [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]e ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
