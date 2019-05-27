---
title: Conectar a um servidor de relatório do modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.connectiondialog.F1
helpviewer_keywords:
- report servers [Reporting Services], configuring
ms.assetid: 8b9ea8d3-827c-4011-9e02-be2eac3bb364
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6fd7ff677fdbbfa91b616fd6a561d3eb48c2de57
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096056"
---
# <a name="connect-to-a-native-mode-report-server"></a>Conectar-se a um servidor de relatório no modo nativo
  Use essa caixa de diálogo para se conectar a uma instância local ou remota do servidor de relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou posterior. Você não pode usar essa ferramenta para se conectar a versões anteriores de servidores de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você só pode se conectar a uma instância por vez.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
>  O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não é usado para configurar e administrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo SharePoint. Use a Administração Central do SharePoint e os scripts do PowerShell para configurar um servidor de relatório em modo SharePoint. Para obter mais informações, consulte [Instalar o Reporting Services no Modo do SharePoint para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
> [!TIP]  
>  O[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (RSConfigTool.exe) do Configuration Manager é instalado com um nível de privilégio de "highestAvailable". Este comportamento ocorre por design. O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige a comunicação com APIs do WMI do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Algumas comunicações de WMI do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exigem um nível mais alto ou administrativo de privilégios.  
  
-   Para conectar-se a uma instância local do servidor de relatório, use os valores padrão e clique em **Conectar**. O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece o nome do servidor local e detecta a instância padrão. Na maioria dos casos, você pode clicar em **Conectar** sem precisar alterar os valores. Se você instalou mais de uma instância, deverá selecionar aquela que deseja usar.  
  
-   Para conectar-se a uma instância remota do servidor de relatório, digite o nome do servidor, clique em **Localizar**, selecione a instância e clique em **Conectar**.  
  
 Para abrir essa caixa de diálogo, inicie o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Essa caixa de diálogo aparecerá imediatamente quando você iniciar a ferramenta. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **Nome do servidor**  
 Insira o nome de rede do computador no qual o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou posterior está instalado. Digite somente o nome do computador; não inclua prefixo nem barras.  
  
 **localizar**  
 Localizar o computador especificado em **Nome do Servidor**.  
  
 **Instância do servidor de relatório**  
 Selecione a qual instância irá se conectar se várias instâncias de servidor de relatório estiverem instaladas. Somente instâncias válidas estão disponíveis para seleção. Se você estiver executando versões mais antigas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] lado a lado com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , aquelas instâncias não aparecerão na lista.  
  
 **Connect**  
 Conectar ao servidor e à instância que você especificou.  
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
