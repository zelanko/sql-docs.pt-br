---
title: Contas de domínio necessárias para o farm do SharePoint (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 90cd6d3e-a271-4cb8-81f2-fc555b2d3cab
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: fd013ae4f7266604dde798aa76393612cd578bad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116287"
---
# <a name="domain-accounts-required-for-sharepoint-farm-upgrade-advisor"></a>Contas de domínio necessárias ao farm do SharePoint (Supervisor de Atualização)
  Os produtos do SharePoint configurados para um ambiente de farm requerem o uso de contas de domínio.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRS](../../includes/ssrs-md.md)]  
  
### <a name="description"></a>Description  
 Os produtos do SharePoint configurados para um ambiente de farm requerem o uso de contas de domínio para conexões de serviços e bancos de dados. Isso inclui a conta especificada para a conta de serviço do Reporting Services.  
  
 Você encontrará problemas nas páginas de Administração Central do SharePoint 2010 se não estiver usando uma conta de usuário de domínio para o Reporting Services. Ao tentar configurar a integração do Reporting Services, você verá uma mensagem de erro similar ao seguinte:  
  
 "O servidor de relatório está sendo executado em uma conta NT AUTHORITY\NETWORK interna, que não tem suporte em uma instalação de farm do SharePoint. Reconfigure o servidor de relatório para ser executado em uma conta de domínio."  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versões anteriores, use o Gerenciador de configuração do Reporting Services para alterar a conta que está atribuída como a conta de serviço do servidor de relatório.  
  
#### <a name="to-change-the-service-account-from-configuration-manager"></a>Para alterar a conta de serviço no Gerenciador de Configuração  
  
1.  Do **iniciar** menu, selecione **todos os programas**e, em seguida, clique em **Microsoft SQL Server 2008 R2**.  
  
2.  Selecione **ferramentas de configuração**e, em seguida, clique em **Reporting Services Configuration Manager**.  
  
3.  No Gerenciador de configuração, selecione o **conta de serviço** guia.  
  
4.  Selecione **usar outra conta** e insira as credenciais para uma conta de domínio.  
  
5.  Clique em **Aplicar**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  