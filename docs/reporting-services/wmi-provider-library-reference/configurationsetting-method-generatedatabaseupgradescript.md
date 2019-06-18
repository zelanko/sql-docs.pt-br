---
title: Método GenerateDatabaseUpgradeScript (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- GenerateDatabaseUpgradeScript (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- GenerateDatabaseUpgradeScript method
ms.assetid: 88534e8e-2877-41cd-b5c2-b1d33a0fd203
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0ffd8985175c7ad2d8acacc95d85bd15ccba1e34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579955"
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
  
## <a name="return-value"></a>Valor retornado  
 Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor 0 indica que a chamada do método teve êxito. Um valor diferente de zero indica que ocorreu um erro.  
  
## <a name="remarks"></a>Remarks  
 O script gerado dá suporte ao [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]e ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
