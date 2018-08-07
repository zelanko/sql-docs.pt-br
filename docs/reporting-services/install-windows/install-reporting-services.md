---
title: Instalar o SQL Server Reporting Services (2017 e posterior) | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.reviewer: ''
ms.suite: pro-bi
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
author: markingmyname
ms.author: maghan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 571e6eaa55fe685d1236d8e35cb7c64b1d3a3cc8
ms.sourcegitcommit: 2e038db99abef013673ea6b3535b5d9d1285c5ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2018
ms.locfileid: "39400619"
---
# <a name="install-sql-server-reporting-services-2017-and-later"></a>Instalar o SQL Server Reporting Services (2017 e posterior)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

A instalação do SQL Server Reporting Services envolve componentes do servidor para armazenar itens de relatório, renderizar relatórios, processar assinaturas e outros serviços de relatório. 

Para baixar o SQL Server 2017 Reporting Services, acesse o [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=55252).

> [!NOTE]
> Procurando o Servidor de Relatórios do Power BI? Consulte [Instalar o Servidor de Relatórios do Power BI](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).

## <a name="before-you-begin"></a>Antes de começar

Antes de instalar o Reporting Services, examine os [Requisitos de hardware e software para instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).

## <a name="install-your-report-server"></a>Instalar o servidor de relatório

A instalação de um servidor de relatório é simples. Há apenas algumas etapas para instalar os arquivos.

> [!NOTE]
> Não é necessário ter um servidor do Mecanismo de Banco de Dados do SQL Server disponível no momento da instalação. Você precisará de um para configurar o Reporting Services após a instalação.

1. Encontre o local do SQLServerReportingServices.exe e inicie o instalador.

2. Selecione **Instalar o Reporting Services**.

    ![Instalar o Reporting Services](media/install-reporting-services/report-server-install.png)

3. Escolha uma edição a ser instalada e, em seguida, selecione **Avançar**.

    ![Escolher a edição](media/install-reporting-services/report-server-install-edition.png)

    Para obter uma edição gratuita, escolha Evaluation ou Developer na lista suspensa.

    ![Evaluation ou Developer Editions](media/install-reporting-services/report-server-install-edition-select.png)

    Caso contrário, insira uma chave do produto (Product Key). [Localizar a chave do produto (Product Key) para o SQL Server 2017 Reporting Services](find-reporting-services-product-key-ssrs.md).

4. Leia e concorde com os termos e condições de licença e, em seguida, selecione **Avançar**.

5. É necessário ter um Mecanismo de Banco de Dados disponível para armazenar o banco de dados do servidor de relatório. Selecione **Avançar** para instalar somente o servidor de relatório.

    ![O banco de dados não é necessário para a instalação](media/install-reporting-services/report-server-install-db-engine.png)

6. Especifique o local de instalação do servidor de relatório. Selecione **Instalar** para continuar.

    ![Especificar o caminho de instalação](media/install-reporting-services/report-server-install-file-path.png)

    > [!NOTE]
    > O caminho padrão é C:\Program Files\Microsoft SQL Server Reporting Services.

7. Após uma instalação bem-sucedida, selecione **Configurar Servidor de Relatório** para iniciar o Gerenciador de Configurações do Reporting Services.

    ![Configurar o servidor de relatório](media/install-reporting-services/report-server-install-configure.png)

## <a name="configuration-your-report-server"></a>Configurando o servidor de relatório

Depois de selecionar **Configurar Servidor de Relatório** na instalação, você verá o **Gerenciador de Configurações do Servidor de Relatório**. Para obter mais informações, consulte [Gerenciador de Configurações do Servidor de Relatório](reporting-services-configuration-manager-native-mode.md).

É necessário [criar um banco de dados do servidor de relatório](ssrs-report-server-create-a-report-server-database.md) para concluir a configuração inicial do Reporting Services. Um servidor de Banco de Dados do SQL Server é necessário para concluir esta etapa.

### <a name="creating-a-database-on-a-different-server"></a>Criando um banco de dados em outro servidor

Caso você esteja criando o banco de dados do servidor de relatório em um servidor de banco de dados em outro computador, precisará alterar a conta de serviço do servidor de relatório para uma credencial que é reconhecida no servidor de banco de dados.

Por padrão, o servidor de relatório usa a conta de serviço virtual. Se você tentar criar um banco de dados em outro servidor, poderá receber o erro a seguir durante a etapa Aplicando direitos de conexão.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

Para solucionar o erro, altere a conta de serviço para Serviço de Rede ou uma conta de domínio. A alteração da conta de serviço para Serviço de Rede aplica os direitos no contexto da conta do computador do servidor de relatório.

Para obter mais informações, consulte [Configurar a conta de serviço do servidor de relatório](configure-the-report-server-service-account-ssrs-configuration-manager.md).

## <a name="windows-service"></a>Serviço Windows

Um serviço Windows é criado como parte da instalação. Ele é exibido como **SQL Server Reporting Services**. O nome do serviço é **SQLServerReportingServices**.

## <a name="default-url-reservations"></a>Reservas de URL padrão

As reservas de URL são compostas de um prefixo, nome de host, porta e diretório virtual:

|Parte|Descrição|
|----------|-----------------|
|Prefixo|O prefixo padrão é HTTP. Se você instalou anteriormente um certificado de protocolo SSL, a Instalação tentará criar reservas de URL que usam o prefixo HTTPS.|
|Nome do host|O nome de host padrão é um curinga forte (+). Ele especifica que o servidor de relatório aceita qualquer solicitação HTTP na porta designada para qualquer nome do host resolvido para o computador, incluindo `http://<computername>/reportserver`, `http://localhost/reportserver` ou `http://<IPAddress>/reportserver.`|
|Porta|A porta padrão é 80. Se você usar qualquer porta que não seja a 80, precisará adicioná-la explicitamente à URL quando abrir o portal da Web em uma janela do navegador.|
|Diretório virtual|Por padrão, os diretórios virtuais são criados no formato de ReportServer para o serviço Web Servidor de Relatórios e Reports para o portal da Web. Para o serviço Web Servidor de Relatórios, o diretório virtual padrão é **reportserver**. Para o portal da Web, o diretório virtual padrão é **reports**.|

Um exemplo de cadeia de caracteres de URL completa poderia ser como segue:

- `http://+:80/reportserver`, fornece acesso ao servidor de relatório.

- `http://+:80/reports`, fornece acesso ao portal da Web.

## <a name="firewall"></a>Firewall

Se estiver acessando o servidor de relatório em um computador remoto, é recomendável verificar se você configurou regras de firewall caso haja um firewall presente.

Você precisa abrir a porta TCP configurada para a URL do Serviço Web e a URL do Portal da Web. Por padrão, elas são configuradas na porta TCP 80.

## <a name="additional-configuration"></a>Configuração adicional

- Para configurar a integração com o serviço do Power BI, de modo que você possa fixar itens de relatório em um painel do Power BI, consulte [Integrar com o serviço do Power BI](power-bi-report-server-integration-configuration-manager.md).

- Para configurar o email para o processamento de assinaturas, consulte [Configurações de email](e-mail-settings-reporting-services-native-mode-configuration-manager.md) e [Entrega de email em um servidor de relatório](../subscriptions/e-mail-delivery-in-reporting-services.md).

- Para configurar o portal da Web para que você possa acessá-lo em um computador remoto a fim de exibir e gerenciar relatórios, consulte [Configurar um firewall para acesso ao servidor de relatório](../report-server/configure-a-firewall-for-report-server-access.md) e [Configurar um servidor de relatório para administração remota](../report-server/configure-a-report-server-for-remote-administration.md).

## <a name="related-information"></a>Informações relacionadas

Para obter informações sobre como instalar o SQL Server 2016 Reporting Services no modo nativo, consulte [Instalar o servidor de relatório no modo nativo do Reporting Services](install-reporting-services-native-mode-report-server.md). Para obter informações sobre como instalar o SQL Server 2016 Reporting Services no modo de integração do SharePoint, consulte [Instalar o primeiro Servidor de Relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md).

## <a name="next-steps"></a>Próximas etapas

Com o servidor de relatório instalado, comece a criar relatórios e implante-os no servidor de relatório. Para obter informações sobre como começar a usar o Construtor de Relatórios, consulte [Instalar o Construtor de Relatórios](../../reporting-services/install-windows/install-report-builder.md).

Para criar relatórios usando o SQL Server Data Tools, [baixe o SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714).

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
