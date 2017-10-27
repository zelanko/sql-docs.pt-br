---
title: Instalar o SQL Server Reporting Services | Microsoft Docs
ms.date: 10/10/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 52c2f8fae79884b025e067b7d628cd3154ba93f4
ms.openlocfilehash: 5ce83ff18d6908441a3eaaf05599068ec5876308
ms.contentlocale: pt-br
ms.lasthandoff: 10/10/2017

---
# <a name="install-sql-server-reporting-services"></a>Instale o SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

A instalação do SQL Server Reporting Services envolve componentes do servidor para armazenar itens de relatório, renderização de relatórios e processamento de assinaturas e outros serviços de relatório.  Saiba como instalar o servidor de relatório do Power BI.

Para baixar o SQL Server de 2017 Reporting Services, vá para o [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55252).

> [!NOTE]
> Procurando o servidor de relatórios de BI de energia? Consulte [instalar o servidor de relatórios de BI Power](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).

## <a name="before-you-begin"></a>Antes de começar

Antes de instalar o Reporting Services, revise o [requisitos de Hardware e software para instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).

## <a name="install-your-report-server"></a>Instalar o servidor de relatório

Instalando um servidor de relatório é muito simples. Há apenas algumas etapas para instalar os arquivos.

> [!NOTE]
> Não é necessário um servidor de mecanismo de banco de dados do SQL Server disponível no momento da instalação. Será necessário configurar o Reporting Services após a instalação.

1. Localizar o local do SQLServerReportingServices.exe e inicie o instalador.

2. Selecione **instalar o Reporting Services**.

    ![Instalar o Reporting Services](media/install-reporting-services/report-server-install.png)

3. Escolher uma edição para instalar e, em seguida, selecione **próximo**.

    ![Escolha a edição](media/install-reporting-services/report-server-install-edition.png)

    Você pode escolher Evaluation ou Developer edition na lista para baixo.

    ![Edições de avaliação ou desenvolvedor](media/install-reporting-services/report-server-install-edition-select.png)

    Caso contrário, você pode inserir uma chave do produto.

4. Ler e concordar com os termos e condições e, em seguida, selecione **próximo**.

5. Você precisa ter um mecanismo de banco de dados disponível para armazenar o banco de dados do servidor de relatório. Selecione **próximo** para instalar o servidor de relatório.

    ![Não é necessário para a instalação do banco de dados](media/install-reporting-services/report-server-install-db-engine.png)

6. Especifique o local de instalação do servidor de relatório. Selecione **instalar** para continuar.

    ![Especifique o caminho de instalação](media/install-reporting-services/report-server-install-file-path.png)

    > [!NOTE]
    > O caminho padrão é C:\Program Files\Microsoft SQL Server Reporting Services.

7. Após uma instalação bem-sucedida, selecione **configurar servidor de relatório** para iniciar o Gerenciador de configuração do Reporting Services.

    ![Configurar o servidor de relatório](media/install-reporting-services/report-server-install-configure.png)

## <a name="configuration-your-report-server"></a>Configuração de seu servidor de relatório

Depois de selecionar **configurar servidor de relatório** na instalação, você verá **Gerenciador de configuração do servidor de relatório**. Para obter mais informações, consulte [Gerenciador de configuração do servidor de relatório](reporting-services-configuration-manager-native-mode.md).

Você precisa [criar um banco de dados do servidor de relatório](ssrs-report-server-create-a-report-server-database.md) para concluir a configuração inicial do Reporting Services. Um servidor de banco de dados do SQL Server é necessário para concluir esta etapa.

### <a name="creating-a-database-on-a-different-server"></a>Criando um banco de dados em um servidor diferente

Se você estiver criando o banco de dados do servidor de relatório em um servidor de banco de dados em um computador diferente, você precisa alterar a conta de serviço do servidor de relatório para uma credencial que é reconhecida no servidor de banco de dados.

Por padrão, o servidor de relatório usa a conta de serviço virtual. Se você tentar criar um banco de dados em um servidor diferente, você poderá receber o seguinte erro durante a etapa de direitos de conexão de aplicação.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

Para solucionar o erro, você pode alterar a conta de serviço para o serviço de rede ou uma conta de domínio. Alterar a conta de serviço para serviço de rede se aplica direitos no contexto da conta da máquina do servidor de relatório.

Para obter mais informações, consulte [configurar a conta de serviço do servidor de relatório](configure-the-report-server-service-account-ssrs-configuration-manager.md).

## <a name="windows-service"></a>Serviço do Windows

Um serviço do windows é criado como parte da instalação. Ele será exibido como **SQL Server Reporting Services**. O nome do serviço é **SQLServerReportingServices**.

## <a name="default-url-reservations"></a>Reservas de URL padrão

As reservas de URL são compostas de um prefixo, nome de host, porta e diretório virtual:

|Parte|Descrição|
|----------|-----------------|
|Prefixo|O prefixo padrão é HTTP. Se você instalou anteriormente um certificado Secure Sockets Layer (SSL), a instalação tentará criar reservas de URL que usem o prefixo HTTPS.|
|Nome do host|O nome de host padrão é um curinga forte (+). Especifica o servidor de relatório aceitará qualquer solicitação HTTP na porta designada para qualquer nome de host resolvido para o computador, incluindo `http://<computername>/reportserver`, `http://localhost/reportserver`, ou`http://<IPAddress>/reportserver.`|
|Porta|A porta padrão é 80. Se você usar qualquer porta diferente da porta 80, você precisa adicioná-la explicitamente à URL quando você abrir o portal da web em uma janela do navegador.|
|Diretório virtual|Por padrão, os diretórios virtuais são criados no formato do ReportServer para o serviço Web do servidor de relatório e os relatórios para o portal da web. Para o serviço Web Servidor de Relatórios, o diretório virtual padrão é **reportserver**. Para o portal da web, o diretório virtual padrão é **relatórios**.|

Um exemplo de cadeia de caracteres de URL completa poderia ser como segue:

- `http://+:80/reportserver`, fornece acesso ao servidor de relatório.

- `http://+:80/reports`, fornece acesso ao portal da web.

## <a name="firewall"></a>Firewall

Se você estiver acessando o servidor de relatório de um computador remoto, você deseja certificar-se de que você configurou as regras de firewall se houver um firewall.

Você precisa abrir a porta TCP que você configurou para a URL do serviço Web e a URL do Portal da Web. Por padrão, eles são configurados na porta TCP 80.

## <a name="additional-configuration"></a>Configuração adicional

- Para configurar a integração com o serviço do Power BI para que você pode fixar itens de relatório em um painel do Power BI, consulte [integrar com o serviço do Power BI](power-bi-report-server-integration-configuration-manager.md).

- Para configurar o email para processamento de assinaturas, consulte [configurações de email](e-mail-settings-reporting-services-native-mode-configuration-manager.md) e [entrega em um servidor de relatório de email](../subscriptions/e-mail-delivery-in-reporting-services.md).

- Para configurar o portal da web para que você pode acessá-lo em um computador remoto para exibir e gerenciar relatórios, consulte [configurar um firewall para acesso ao servidor de relatório](../report-server/configure-a-firewall-for-report-server-access.md) e [configurar um servidor de relatório para administração remota](../report-server/configure-a-report-server-for-remote-administration.md) .

## <a name="related-information"></a>Informações relacionadas

Para obter informações sobre como instalar o SQL Server 2016 Reporting Services no modo nativo, consulte [servidor de relatório de modo nativo de instalar o Reporting Services](install-reporting-services-native-mode-report-server.md). Para obter informações sobre como instalar o SQL Server 2016 Reporting Services no modo de integração do SharePoint, consulte [instalar o primeiro servidor de relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md).

## <a name="next-steps"></a>Próximas etapas

Com o servidor de relatório instalado, começar a criar relatórios e implante-as no servidor de relatório. Para obter informações sobre como iniciar o construtor de relatórios, consulte [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md).

Para criar relatórios usando o SQL Server Data Tools, [baixar o SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714).

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)

