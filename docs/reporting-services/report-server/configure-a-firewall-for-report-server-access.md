---
title: Configurar um firewall para acesso ao servidor de relatório | Microsoft Docs
description: Saiba como configurar o Firewall do Windows para permitir o acesso a aplicativos e relatórios publicados do Servidor de Relatório que são acessados por meio de URLs.
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [Reporting Services]
- configuring servers [Reporting Services]
ms.assetid: 04dae07a-a3a4-424c-9bcb-a8000e20dc93
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 89ad4ef0d7537f1b5e8cad9349eb7aeacf0872c6
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934615"
---
# <a name="configure-a-firewall-for-report-server-access"></a>Configure a Firewall for Report Server Access
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Os aplicativos e os relatórios publicados do servidor de relatório são acessados por meio de URLs que especificam um endereço IP, uma porta e um diretório virtual. Se o Firewall do Windows estiver ativado, a porta que o servidor de relatório está configurado para usar provavelmente estará fechada. As indicações de que uma porta deve ser fechada são uma página em branco quando você tenta abrir o portal da Web de um computador cliente remoto, ou uma página da Web em branco após a solicitação em um relatório.  
  
 Para abrir uma porta, você deve usar o utilitário Firewall do Windows no computador do servidor de relatório. O Reporting Services não abrirá portas para você; é necessário executar essa etapa manualmente.  
  
 Por padrão, o servidor de relatório escuta solicitações HTTP na porta 80. Dessa forma, as instruções a seguir incluem etapas que especificam essa porta. Se você tiver configurado para que as URLs do servidor de relatório usem uma porta diferente, deverá especificar esse número de porta ao seguir as próximas instruções.  
  
 Se você estiver acessando bancos de dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em computadores externos ou se o banco de dados do servidor de relatório estiver em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] externa , você deve abrir as portas 1433 e 1434 no computador externo. Para obter mais informações, veja [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md). Para obter mais informações sobre as configurações de firewall do Windows padrão e obter uma descrição das portas TCP que afetam o [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Essas instruções supõem que você já configurou a conta de serviço, criou o banco de dados do servidor de relatório e configurou URLs do serviço Web Servidor de Relatórios e o portal da Web. Para obter mais informações, consulte [Gerenciar um servidor de relatório de modo nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
 Você também deve ter verificado se o servidor de relatório pode ser acessado por uma conexão local de navegador Web com a instância local do servidor de relatório. Essa etapa confirma que você tem uma instalação em funcionamento. Você deve verificar se a instalação está configurada corretamente antes de começar a abrir portas. Para concluir essa etapa no Windows Server, você também deve ter adicionado o site do servidor de relatório aos Sites Confiáveis. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="opening-ports-in-windows-firewall"></a>Abrindo portas no Firewall do Windows  
  
#### <a name="to-open-port-80"></a>Para abrir a porta 80  
  
1.  No menu **Iniciar** , clique em **Painel de Controle**, em **Sistema e Segurança**e, em seguida, em **Firewall do Windows**. O Painel de controle não está configurado para a exibição 'Categoria', você precisa selecionar apenas a opção **Firewall do Windows.**  
  
2.  Clique em **Configurações Avançadas**.  
  
3.  Clique em **Regras de entrada**.  
  
4.  Clique em **Nova Regra** na janela **Ações**.  
  
5.  Clique em **Tipo de Regra** de **porta.**  
  
6.  Clique em **Próximo**.  
  
7.  Na página **Protocolos e Portas** , clique em **TCP**.  
  
8.  Selecione **Portas Locais Específicas** e digite um valor de **80**.  
  
9. Clique em **Próximo**.  
  
10. Na página **Ação** , clique em **Permitir a conexão**.  
  
11. Clique em **Próximo**.  
  
12. Na página **Perfil** , clique nas opções adequadas para seu ambiente.  
  
13. Clique em **Próximo**.  
  
14. Na página **Nome** , digite o nome do**ReportServer (TCP na porta 80)**  
  
15. Clique em **Concluir**.  
  
16. Reinicie o computador.  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de abrir a porta e antes de confirmar se usuários remotos podem acessar o servidor de relatório na porta que abriu, você deverá conceder acesso de usuário ao servidor de relatório por meio de atribuições de função em Base e no nível do site. Você pode abrir uma porta corretamente e ainda ter falha de conexões do servidor de relatório se os usuários não tiverem permissões adequadas. Para obter mais informações, consulte [Conceder acesso ao usuário a um servidor de relatório](../../reporting-services/security/grant-user-access-to-a-report-server.md).  
  
 Você também pode verificar se a porta está aberta corretamente iniciando o portal da Web em um computador diferente. Para saber mais, confira o [portal da Web de um servidor de relatório](../../reporting-services/web-portal-ssrs-native-mode.md).
  
## <a name="see-also"></a>Confira também  
 [Configurar a conta de serviço do Servidor de Relatório &#40;Gerenciador de Configurações do Servidor de Relatório&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar URLs do servidor de relatório &#40;Gerenciador de Configurações do Servidor de Relatório&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Criar um banco de dados do servidor de relatório &#40;Gerenciador de Configurações do Servidor de Relatório&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [Configurar a conta de serviço do Servidor de Relatório &#40;Gerenciador de Configurações do Servidor de Relatório&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Gerenciar um servidor de relatórios de Modo Nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
