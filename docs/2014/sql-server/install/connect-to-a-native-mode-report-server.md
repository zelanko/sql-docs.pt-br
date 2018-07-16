---
title: Conectar a um servidor de relatório do modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.connectiondialog.F1
helpviewer_keywords:
- report servers [Reporting Services], configuring
ms.assetid: 8b9ea8d3-827c-4011-9e02-be2eac3bb364
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 27b2d2d93d83057fd2de408b4a0cb61dd1cd0771
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321776"
---
# <a name="connect-to-a-native-mode-report-server"></a>Conectar-se a um servidor de relatório no modo nativo
  Use essa caixa de diálogo para se conectar a um local ou remota [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instância do servidor de relatório. Você não pode usar essa ferramenta para se conectar a versões anteriores do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidores de relatório. Você só pode se conectar a uma instância por vez.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
>  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager não é usado para configurar e administrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint. Use a Administração Central do SharePoint e os scripts do PowerShell para configurar um servidor de relatório em modo SharePoint. Para obter mais informações, consulte [instalar o Reporting Services SharePoint Mode para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
> [!TIP]  
>  O[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (RSConfigTool.exe) do Configuration Manager é instalado com um nível de privilégio de "highestAvailable". Este comportamento ocorre por design. O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige a comunicação com APIs do WMI do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Algumas comunicações de WMI do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exigem um nível mais alto ou administrativo de privilégios.  
  
-   Para conectar-se a uma instância local do servidor de relatório, use os valores padrão e clique em **Conectar**. O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece o nome do servidor local e detecta a instância padrão. Na maioria dos casos, você pode clicar em **Conectar** sem precisar alterar os valores. Se você instalou mais de uma instância, deverá selecionar aquela que deseja usar.  
  
-   Para conectar-se a uma instância remota do servidor de relatório, digite o nome do servidor, clique em **Localizar**, selecione a instância e clique em **Conectar**.  
  
 Para abrir essa caixa de diálogo, inicie o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do Configuration Manager. Essa caixa de diálogo aparecerá imediatamente quando você iniciar a ferramenta. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **Nome do servidor**  
 Insira o nome da rede do computador no qual [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está instalado. Digite somente o nome do computador; não inclua prefixo nem barras.  
  
 **Localizar**  
 Localizar o computador especificado em **Nome do Servidor**.  
  
 **Instância do servidor de relatório**  
 Selecione a qual instância irá se conectar se várias instâncias de servidor de relatório estiverem instaladas. Somente instâncias válidas estão disponíveis para seleção. Se você estiver executando versões mais antigas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] lado a lado um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da instância, aquelas instâncias não aparecerão na lista.  
  
 **Connect**  
 Conectar ao servidor e à instância que você especificou.  
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
