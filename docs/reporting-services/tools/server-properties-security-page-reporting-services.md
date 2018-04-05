---
title: Propriedades do servidor (página Segurança) – Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9fd7681e1628b493fa7c1864d2b6010e7d78d62d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="server-properties-security-page---reporting-services"></a>Propriedades do Servidor (página Segurança) - Reporting Services
  Use esta página [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] para desativar recursos que podem comprometer um servidor de relatório potencialmente. A desativação desse recurso limitará algumas funcionalidades, mas pode aprimorar a segurança geral do servidor de relatório, reduzindo ameaças específicas.  
  
 Para abrir esta página:
 1) Inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Conecte-se a uma instância do servidor de relatório.
 3) Clique com o botão direito do mouse no nome do servidor de relatório e selecione **Propriedades**. 
 4) Clique em **Segurança** para abrir essa página.  
  
## <a name="options"></a>Opções  
 **Habilitar a segurança integrada do Windows para as fontes de dados do relatório**  
 Especifique se uma conexão com uma fonte de dados de relatório pode ser feita usando o token de segurança do Windows do usuário que solicitou o relatório.  
  
 Se esse recurso for desativado, o recurso de Segurança Integrada do Windows nas páginas de propriedades das fontes de dados do relatório se tornará indisponível. Se as fontes de dados do relatório estiverem configuradas para segurança integrada do Windows e você subsequentemente desativar esse recurso, o servidor de relatório atualizará imediatamente todas as propriedades de conexão da fonte de dados para solicitar credenciais.  
  
 **Habilitar Relatórios Ad Hoc**  
 Especifique se os usuários podem executar consultas ad hoc de um relatório do Construtor de Relatórios, onde novos relatórios são automaticamente gerados quando um usuário clica nos dados de interesse.  
  
 A definição dessa opção determina se a propriedade **EnableLoadReportDefinition** no servidor de relatório é definida como **True** ou **False**. Se você desmarcar esta opção, a propriedade será definida como **False** e o servidor de relatório não gerará relatórios de clickthrough criados durante a exploração dos dados. Todas as chamadas para o método **LoadReportDefinition** serão bloqueadas.  
  
 A desativação dessa opção reduz uma ameaça de que um usuário mal-intencionado inicie um ataque de negação de serviço, carregando o servidor de relatório com solicitações de **LoadReportDefinition** .  
  
## <a name="see-also"></a>Consulte Também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
