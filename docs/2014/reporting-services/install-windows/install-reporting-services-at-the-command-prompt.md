---
title: Instalação de Prompt de comando do Reporting Services no modo do SharePoint e modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc1e5ae5d17d45b937a5dd44ab3ea6fe5f8620eb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108774"
---
# <a name="command-prompt-installation-of-reporting-services-sharepoint-mode-and-native-mode"></a>Instalação de prompt de comando de modo do SharePoint do Reporting Services e modo nativo
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte a uma instalação de linha de comando do programa de instalação do SQL Server. Este tópico contém vários exemplos de instalações de linha de comando que são específicas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter uma descrição completa das opções de linha de comando disponíveis para todos os componentes do SQL Server, consulte [instalar o SQL Server 2014 do Prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md). Este tópico não descreve opções de linha de comando para o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos SharePoint. Para obter informações sobre a instalação de comando do suplemento, consulte [Instalar o suplemento usando o arquivo de instalação rsSharePoint.msi](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint).  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** Modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE (modo nativo)  
 A configuração de entrada primária para a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é a configuração de entrada **/RSINSTALLMODE** . A configuração tem duas opções: **DefaultNativeMode** e **FilesOnlyMode**  
  
 Se a instalação incluir o Mecanismo de Banco de Dados do SQL Server, o RSINSTALLMODE padrão será DefaultNativeMode. Se a instalação não incluir o Mecanismo de Banco de Dados do SQL Server, o RSINSTALLMODE padrão será FilesOnlyMode. Se você escolher DefaultNativeMode, mas a instalação não incluir o Mecanismo de Banco de Dados do SQL Server, a instalação alterará automaticamente o RSINSTALLMODE para FilesOnlyMode. Para obter mais informações sobre as configurações de entrada, consulte [instalar o SQL Server 2014 do Prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
## <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE (modo do SharePoint)  
 A configuração de entrada para instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint é **/RSSHPINSTALLMODE**. A configuração de entrada tem uma opção: SharePointFilesOnlyMode. A opção instala todos os arquivos necessários para o modo do SharePoint. Entretanto, é necessário fazer a configuração após a instalação. As etapas de configuração adicional são concluídas usando a Administração Central do SharePoint. Para obter mais informações, consulte [instalar o Reporting Services SharePoint Mode para SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
## <a name="examples-of-sharepoint-mode-installation"></a>Exemplos de instalação do modo do SharePoint  
 O exemplo a seguir instala o serviço de mecanismo de banco de dados do SQL Server e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint, bem como o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para o SharePoint (RS_SHPWFE).  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 O exemplo a seguir instala apenas o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="*****" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
 O exemplo a seguir instala todos os recursos do SQL Server, inclusive o modo nativo e o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT, RS_SHP,RS_SHPWFE,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSSHPINSTALLMODE="SharePointFilesOnlyMode" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="examples-of-sharepoint-mode-upgrade"></a>Exemplos de atualização do modo do SharePoint  
 O exemplo seguinte atualiza o modo do SharePoint [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . **RSUPGRADEPASSWORD** é a senha da conta de serviço existente do Servidor de Relatórios. RSUPGRADEPASSWORD é um campo obrigatório em um cenário de atualização a menos que a conta de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] seja uma conta interna.  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[ACCOUNTPASSSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="******"  
```  
  
 O exemplo a seguir pode ser usado para atualizar uma instalação do modo SharePoint que se baseia na arquitetura de serviço compartilhado do SharePoint. O exemplo usa a opção ALLOWUPGRADEFORSSRSSHAREPOINTMODE. A opção não é necessária para atualizar versões anteriores que não se baseiam na arquitetura de serviço compartilhado:  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="****" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```  
  
## <a name="examples-of-native-mode-installation"></a>Exemplos de instalação do modo nativo  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o SQL Server 2014 do Prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Parâmetros do SysPrep](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#SysPrep)   
 [Instalar o PowerPivot pelo prompt de comando](../../sql-server/install/install-powerpivot-from-the-command-prompt.md)  
  
  
