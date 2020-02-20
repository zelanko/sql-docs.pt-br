---
title: Instalar o Reporting Services 2016 no prompt de comando – SSRS | Microsoft Docs
ms.date: 01/09/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- command line
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7c4597a19b3fbcde0a5b4f6a82cb2398b6776128
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "62513668"
---
# <a name="install-reporting-services-2016-at-the-command-prompt"></a>Instalar o Reporting Services 2016 no prompt de comando

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte a uma instalação de linha de comando do programa de instalação do SQL Server. Este tópico contém vários exemplos de instalações de linha de comando que são específicas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter uma descrição completa das opções de linha de comando disponíveis para todos os componentes do SQL Server, consulte [Instalar o SQL Server por meio do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Este tópico não descreve opções de linha de comando para o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos SharePoint. Para obter informações sobre a instalação de comando do suplemento, consulte [Instalar o suplemento usando o arquivo de instalação rsSharePoint.msi](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint).

##  <a name="bkmk_native_mode"></a> Reporting Services no modo Nativo

### <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE (modo nativo)
 A configuração de entrada primária para a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é a configuração de entrada **/RSINSTALLMODE** . A configuração tem duas opções: **DefaultNativeMode** e **FilesOnlyMode**  
  
 Se a instalação incluir o Mecanismo de Banco de Dados do SQL Server, o RSINSTALLMODE padrão será DefaultNativeMode. Se a instalação não incluir o Mecanismo de Banco de Dados do SQL Server, o RSINSTALLMODE padrão será FilesOnlyMode. Se você escolher DefaultNativeMode, mas a instalação não incluir o Mecanismo de Banco de Dados do SQL Server, a instalação alterará automaticamente o RSINSTALLMODE para FilesOnlyMode. Para obter mais informações sobre as configurações de entrada, confira [Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).

### <a name="examples-of-native-mode-installation"></a>Exemplos de instalação do modo nativo

 O exemplo a seguir instala o seguinte e configura as contas para:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em modo Nativo.  
  
-   O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   SQL Server Agent, que é necessário para os recursos de assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
```  
Setup.exe /q /IACCEPTSQLSERVERLICENSETERMS /ACTION="install" /ERRORREPORTING=1 /UPDATEENABLED="False" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Adv_SSMS,RS" /RSINSTALLMODE="DefaultNativeMode" /SQLSVCACCOUNT="[DOMAIN\ACCOUNT]" /SQLSVCPASSWORD="[PASSWORD]" /AGTSVCACCOUNT="[DOMAIN\ACCOUNT]" /AGTSVCPASSWORD="[PASSWORD]" /SQLSYSADMINACCOUNTS="[DOMAIN\ACCOUNT]"  
```  
  
##  <a name="bkmk_sharepoint_mode"></a> Reporting Services no modo SharePoint  
  
### <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE (modo do SharePoint)  
 A configuração de entrada para instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint é **/RSSHPINSTALLMODE**. A configuração de entrada tem uma opção: SharePointFilesOnlyMode. A opção instala todos os arquivos necessários para o modo do SharePoint. Entretanto, é necessário fazer a configuração após a instalação. As etapas de configuração adicional são concluídas usando a Administração Central do SharePoint. Para saber mais, confira [Instalar o primeiro servidor de relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md).  
  
### <a name="examples-of-sharepoint-mode-installation"></a>Exemplos de instalação do modo do SharePoint  
 O exemplo a seguir instala o serviço de mecanismo de banco de dados do SQL Server e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint, bem como o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para o SharePoint (RS_SHPWFE).  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 O exemplo a seguir instala apenas o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="[PASSWORD]" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
### <a name="examples-of-sharepoint-mode-upgrade"></a>Exemplos de atualização do modo do SharePoint  
 O exemplo seguinte atualiza o modo do SharePoint [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . **RSUPGRADEPASSWORD** é a senha da conta de serviço existente do Servidor de Relatórios. RSUPGRADEPASSWORD é um campo obrigatório em um cenário de atualização a menos que a conta de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] seja uma conta interna.  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="[PASSWORD]"  
```  
  
 O exemplo a seguir pode ser usado para atualizar uma instalação do modo SharePoint que se baseia na arquitetura de serviço compartilhado do SharePoint. O exemplo usa a opção ALLOWUPGRADEFORSSRSSHAREPOINTMODE. A opção não é necessária para atualizar versões anteriores que não se baseiam na arquitetura de serviço compartilhado:  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```

## <a name="next-steps"></a>Próximas etapas

[Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
[Parâmetros do SysPrep](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#SysPrep)   
[Instalar o Power Pivot pelo prompt de comando](https://msdn.microsoft.com/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
