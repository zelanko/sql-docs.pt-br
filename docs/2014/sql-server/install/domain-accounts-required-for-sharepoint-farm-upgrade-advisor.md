---
title: Contas de domínio necessárias para o farm do SharePoint (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 90cd6d3e-a271-4cb8-81f2-fc555b2d3cab
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c4079ea4213d7ecbec0165c32c82b3449bbb5aee
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952516"
---
# <a name="domain-accounts-required-for-sharepoint-farm-upgrade-advisor"></a>Contas de domínio necessárias ao farm do SharePoint (Supervisor de Atualização)
  Os produtos do SharePoint configurados para um ambiente de farm requerem o uso de contas de domínio.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRS](../../includes/ssrs.md)]  
  
### <a name="description"></a>Descrição  
 Os produtos do SharePoint configurados para um ambiente de farm requerem o uso de contas de domínio para conexões de serviços e bancos de dados. Isso inclui a conta especificada para a conta de serviço do Reporting Services.  
  
 Você encontrará problemas nas páginas de Administração Central do SharePoint 2010 se não estiver usando uma conta de usuário de domínio para o Reporting Services. Ao tentar configurar a integração do Reporting Services, você verá uma mensagem de erro similar ao seguinte:  
  
 "O servidor de relatório está sendo executado em uma conta NT AUTHORITY\NETWORK interna, que não tem suporte em uma instalação de farm do SharePoint. Reconfigure o servidor de relatório para ser executado em uma conta de domínio."  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versões anteriores, use a Gerenciador de Configurações do Reporting Services para alterar a conta atribuída como a conta de serviço do servidor de relatório.  
  
#### <a name="to-change-the-service-account-from-configuration-manager"></a>Para alterar a conta de serviço no Gerenciador de Configuração  
  
1.  No menu **Iniciar** , selecione **todos os programas**e, em seguida, clique em **Microsoft SQL Server 2008 R2**.  
  
2.  Selecione **ferramentas de configuração**e, em seguida, clique em **Gerenciador de configurações do Reporting Services**.  
  
3.  Em Configuration Manager, selecione a guia **conta de serviço** .  
  
4.  Selecione **usar outra conta** e insira as credenciais para uma conta de domínio.  
  
5.  Clique em **Aplicar**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  
