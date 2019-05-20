---
title: Configurar o acesso ao Construtor de Relatórios | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.date: 03/14/2017
ms.openlocfilehash: 2f99729717d291b241418b12142a5be8cfa67a03
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774443"
---
# <a name="configure-report-builder-access"></a>Configurar o acesso ao Construtor de Relatórios
O Construtor de Relatórios é uma ferramenta de criação de relatórios ad hoc instalada com um servidor de relatório do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para o modo nativo ou o modo de integração no SharePoint.  

O acesso ao Construtor de Relatórios depende dos seguintes fatores:  

- As propriedades de servidor que determinam se o Construtor de Relatórios está disponível no servidor de relatório.  

- As atribuições de função ou permissões que disponibilizam o Construtor de Relatórios para usuários individuais ou grupos.  

- As configurações de autenticação que determinam se as credenciais de usuário podem ser transmitidas através do servidor de relatório ou se o acesso anônimo está configurado nos arquivos de aplicativo.

## <a name="prerequisites"></a>Prerequisites

O Construtor de Relatórios não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [Recursos com suporte nas edições do SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md).  

O computador cliente deve ter o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 instalado. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornece a infraestrutura para executar aplicativos [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] .  

Você deve usar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 6.0 ou posterior.  

O Construtor de Relatórios sempre é executado no modo de confiança total; você não pode configurá-lo para ser executado em confiança parcial. Nas versões anteriores, era possível executar o Construtor de Relatórios em confiança parcial, mas essa opção não é suportada no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores.  

## <a name="enabling-and-disabling-report-builder"></a>Habilitando e desabilitando o Construtor de Relatórios  

O Construtor de Relatórios é habilitado por padrão. Os administradores de servidor de relatório têm a opção de desabilitar o recurso Construtor de Relatórios, definindo a propriedade de sistema do servidor de relatório **EnableReportDesignClientDownload** como **false**. A definição dessa propriedade desabilitará os downloads do Construtor de Relatórios para esse servidor de relatório.  

Para definir propriedades de sistema do servidor de relatório, você pode usar o Management Studio ou script:  

- Para usar o Management Studio, conecte-se ao servidor de relatório e use a página Propriedades Avançadas do Servidor para definir **EnableReportDesignClientDownload** como **false**. Para obter mais informações sobre como abrir essa página, consulte [Definir as propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).  

- Para ver um exemplo de script que define uma propriedade de servidor de relatório, consulte [Implantação de script e tarefas administrativas](../../reporting-services/tools/script-deployment-and-administrative-tasks.md).  

## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>Atribuições de função que concedem o acesso ao Construtor de Relatórios em um servidor de relatório no modo nativo  

Em um servidor de relatório no modo nativo, crie atribuições de função de usuário que incluem tarefas para usar o Construtor de Relatórios. Você deve ser Gerenciador de Conteúdo e Administrador de Sistema para criar ou modificar definições de função e atribuições de função em itens e no nível de site.  

As instruções a seguir presumem que você está usando funções predefinidas. Se você tiver modificado as definições de função ou feito a atualização a partir do SQL Server 2000, verifique se as funções contêm as tarefas necessárias. Para obter mais informações sobre como criar atribuições de função, consulte [Conceder acesso ao usuário a um servidor de relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md).  

Depois que você criar as atribuições de função, os usuários terão permissão para fazer o seguinte:  

- Os usuários com as funções Usuário do Sistema e Navegador podem exibir os relatórios publicados do Construtor de Relatórios em um servidor de relatório, sem precisar iniciar o Construtor de Relatórios.  

- Os usuários com as funções Usuário do Sistema e Construtor de Relatórios podem gerar modelos, iniciar o Construtor de Relatórios e criar relatórios, além de salvá-los no servidor de relatório.  

- Os usuários com as funções Usuário do Sistema e Publicador podem publicar modelos do Designer de Modelo no servidor de relatório. Os modelos são usados como fontes de dados no Construtor de Relatórios.  

- Os usuários com as funções Administrador do Sistema e Gerenciador de Conteúdo têm permissões completas para criar, exibir e gerenciar relatórios do Construtor de Relatórios.  

### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>Para verificar se as tarefas necessárias estão nas definições de função  

1. Inicie o Management Studio e conecte-se ao servidor de relatório.  

2. Abra a pasta **Segurança** .  

3. Abra a pasta **Funções do Sistema** .  

4. Clique com o botão direito do mouse em **Administrador do Sistema**e selecione **Propriedades**.  

5. Selecione **Executar definições de relatórios** e clique em **OK**.  

6. Clique com o botão direito do mouse em **Usuário do Sistema**e selecione **Propriedades**.  

7. Selecione **Executar definições de relatórios** e clique em **OK**.  

8. Abra a pasta **Funções** .  

9. Clique com o botão direito do mouse em **Navegador**e selecione **Propriedades**.  

10. Selecione **Exibir modelos** e clique em **OK**.  

11. Clique com o botão direito do mouse em **Gerenciador de Conteúdo**e selecione **Propriedades**.  

12. Selecione **Exibir modelos**, **Gerenciar modelos**, **Relatórios de consumo**e clique em **OK**.  

13. Clique com o botão direito do mouse em **Publicador**e selecione **Propriedades**.  

14. Selecione **Gerenciar modelos** e clique em **OK**.  

15. Se não existir, crie a função do Construtor de Relatórios:  

    1. Abra a pasta **Segurança** .  

    2. Clique com o botão direito do mouse em **Funções**e selecione **Nova Função**.  

    3. Em Nome, digite **Construtor de Relatórios**.  

    4. Em Descrição, insira uma descrição para a função de modo que os usuários do Gerenciador de Relatórios saibam de que se trata a função.  

    5. Adicione as seguintes tarefas: **Relatórios de consumo**, **Exibir relatórios**, **Exibir modelos**, **Exibir recursos**, **Exibir pastas**e **Gerenciar assinaturas individuais**.  

    6. Clique em **OK** para salvar a função.  

#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>Para criar atribuições de função que concedem acesso ao Construtor de Relatórios  

1. Inicie o Gerenciador de Relatórios.  

2. Clique em **Configurações de Site**.  

3. Clique em **Segurança**.  

4. Se uma atribuição de função já existir para o usuário ou grupo para o qual deseja configurar o acesso do Construtor de Relatórios, clique em **Editar**.  
Caso contrário, clique em **Atribuição de Nova Função**. Em Grupo ou usuário, insira uma conta de usuário ou grupo de domínio do Windows neste formato: \<domain>\\<account\>. Se estiver usando a autenticação de formulários ou a segurança personalizada, especifique a conta de usuário ou grupo no formato correto de sua implantação.  

5. Selecione **Usuário do Sistema**e clique em **OK**.  

6. Clique em **Página inicial**.  

7. Clique na guia **Configurações de Pasta** .  

8. Clique na guia **Segurança** .  

9. Se uma atribuição de função já existir para o usuário ou grupo para o qual deseja configurar o acesso do Construtor de Relatórios, clique em **Editar**.  

    Caso contrário, clique em **Atribuição de Nova Função**. Em Grupo ou usuário, insira uma conta de usuário ou grupo de domínio do Windows neste formato: \<domain>\\<account\>. Se estiver usando a autenticação de formulários ou a segurança personalizada, especifique a conta de usuário ou grupo no formato correto de sua implantação.  

10. Selecione **Construtor de Relatórios**e clique em **Aplicar**.  

11. Repita o procedimento para criar ou modificar atribuições de função para usuários ou grupos adicionais.  

## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>Permissões que concedem acesso ao Construtor de Relatórios em um servidor de relatório no modo integrado do SharePoint  

Em um servidor de relatório no modo integrado do SharePoint, o acesso ao Construtor de Relatórios é concedido aos usuários do SharePoint que têm os níveis de permissão Colaboração ou Controle Total.  

Se você usar níveis de permissão personalizados, inclua Adicionar Itens e Editar Itens no nível de permissão. Para obter mais informações sobre o acesso ao Construtor de Relatórios por meio de níveis de permissão internos, consulte [Usar a segurança interna no Windows SharePoint Services para itens do servidor de relatório](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md). Para obter mais informações sobre requisitos de permissão para níveis de permissão personalizados, consulte [Definir permissões para operações do servidor de relatório em um aplicativo Web do SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  

## <a name="authentication-considerations-and-credential-reuse"></a>Considerações de autenticação e reutilização de credenciais  

- O Construtor de Relatórios abre sua própria conexão com um servidor de relatório. Se não estiver usando a segurança integrada do Windows com logon único, os usuários devem digitar novamente suas credenciais para conectar o Construtor de Relatórios com o servidor de relatório.  

A tabela a seguir descreve os tipos de autenticação suportados pelo servidor de relatório e informa se alguma configuração adicional é necessária para acessar o Construtor de Relatórios.  

## <a name="see-also"></a>Confira também  

- [Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)
- [Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
- [Iniciar o Construtor de Relatórios](../../reporting-services/report-builder/start-report-builder.md)
- [&#40;Modo nativo SSRS&#41; do Gerenciador de Relatórios](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)- [Conectar a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)
- [Propriedades do sistema do Servidor de Relatório](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)