---
title: Gerenciador de Conexões de SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
caps.latest.revision: 10
f1_keywords:
- sql13.dts.designer.sapbwconnectionmanager.f1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 57e563e0078face8a4fc40c38b9cc568f9ee38ce
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403478"
---
# <a name="sap-bw-connection-manager"></a>Gerenciador de Conexões SAP BW
  O gerenciador de conexões SAP BW é o componente de gerenciador de conexões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW. Portanto, o gerenciador de conexões do SAP BW fornece a conectividade para um sistema SAP Netweaver BW versão 7 que os componentes de origem e destino do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW precisam. (A origem e o destino SAP BW que fazem parte do pacote do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW são os únicos componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que usam o gerenciador de conexões do SAP BW.)  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 Quando você adiciona um gerenciador de conexões do SAP BW a um pacote, a propriedade **ConnectionManagerType** do gerenciador de conexões é definida como **SAPBI**.  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>Configurando o gerenciador de conexões SAP BW  
 Você pode configurar um gerenciador de conexões SAP BW de uma das seguintes formas:  
  
-   Forneça o cliente, o nome de usuário, a senha e o idioma para a conexão.  
  
-   Escolha se deseja se conectar a um único servidor de aplicativos ou um grupo de servidores com balanceamento de carga.  
  
-   Forneça o host e o número do sistema para um único servidor de aplicativos ou forneça o servidor de mensagens, o grupo e o SID para um grupo de servidores com balanceamento de carga.  
  
-   Habilite o log personalizado das chamadas de função de RFC para os componentes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW. (Esse log é separado do log opcional que você pode habilitar em pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].) Para habilitar o log das chamadas de função de RFC, você especifica um diretório no qual armazenar os arquivos de log que são criados antes e depois de cada chamada de função de RFC. (Esse recurso de registro cria muitos arquivos de log em formato XML. Como esses arquivos de log também contêm todas as linhas de dados que são transferidas, esses arquivos de log podem consumir uma grande quantidade de espaço em disco.) Se você não selecionar um diretório de log, o registro em log não será habilitado.  
  
    > [!IMPORTANT]  
    >  Se os dados que são transferidos contêm informações confidenciais, os arquivos de log também conterão essas informações confidenciais.  
  
-   Use os valores que você inseriu para testar a conexão.  
  
 Se você não souber todos os valores necessários para configurar o gerenciador de conexões, talvez precise perguntar ao administrador do SAP.  
  
 Para obter um passo a passo que demonstre como configurar e usar o gerenciador de conexões do SAP BW, a origem e o destino, consulte o white paper [Usando o SQL Server 2008 Integration Services com SAP BI 7.0](http://go.microsoft.com/fwlink/?LinkID=137090). Este white paper também mostra como configurar os objetos necessários no SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>Usando o Designer SSIS para configurar a origem  
 Para obter mais informações sobre as propriedades do gerenciador de conexões do SAP BW que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Editor do Gerenciador de Conexões de SAP BW](../../integration-services/connection-manager/sap-bw-connection-manager-editor.md)  
  
## <a name="sap-bw-connection-manager-editor"></a>Editor do Gerenciador de Conexões de SAP BW
  Use **Editor do Gerenciador de Conexões do SAP BW** para especificar as propriedades a serem usadas para se conectar a um sistema SAP Netweaver BW versão 7.  
  
 O gerenciador de conexões do SAP BW fornece conectividade para um sistema SAP Netweaver BW 7 para o uso pela origem ou destino do SAP BW. Para saber mais sobre o gerenciador de conexões do SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Gerenciador de conexões SAP BW](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir o Gerenciador de Conexões do SAP BW**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o gerenciador de conexões do SAP BW.  
  
2.  Na área Gerenciadores de Conexões na guia **Fluxo de Controle** , execute uma das seguintes etapas:  
  
    -   Clique duas vezes no gerenciador de conexões SAP BW.  
  
         — ou —  
  
    -   Clique com o botão direito do mouse no gerenciador de conexões SAP BW e selecione **Editar**.  
  
### <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar o gerenciador de conexões, talvez precise perguntar ao administrador do SAP.  
  
 **Cliente**  
 Especifique o número de cliente do sistema.  
  
 **Idioma**  
 Especifique o idioma que o sistema usará. Por exemplo, especifique **EN** para inglês.  
  
 **User name**  
 Especifique o nome de usuário que será usado para conexão com o sistema.  
  
 **Senha**  
 Especifique a senha que será usada com o nome de usuário.  
  
 **Usar servidor de aplicativo único**  
 Conecte-se a um único servidor de aplicativos.  
  
 Para se conectar a um grupo de servidores com balanceamento de carga, use a opção **Usar balanceamento de carga** .  
  
 **Host**  
 Se estiver se conectando a um único servidor de aplicativos, especifique o nome do host.  
  
> [!NOTE]  
>  Esta opção só estará disponível se você tiver selecionado a opção **Usar servidor de aplicativo único** .  
  
 **Número do sistema**  
 Se estiver se conectando a um único servidor de aplicativos, especifique o número do sistema.  
  
> [!NOTE]  
>  Esta opção só estará disponível se você tiver selecionado a opção **Usar servidor de aplicativo único** .  
  
 **Usar balanceamento de carga**  
 Conecte-se a um grupo de servidores com balanceamento de carga.  
  
 Para conectar-se a um único servidor de aplicativos, use a opção **Usar servidor de aplicativo único** .  
  
 **Servidor de mensagens**  
 Se estiver se conectando a um grupo de servidores com balanceamento de carga, especifique o nome do servidor de mensagens.  
  
> [!NOTE]  
>  Esta opção só estará disponível se você tiver selecionado a opção **Usar balanceamento de carga** .  
  
 **Agrupar**  
 Se estiver se conectando a um grupo de servidores com balanceamento de carga, especifique o nome do grupo de servidores.  
  
> [!NOTE]  
>  Esta opção só estará disponível se você tiver selecionado a opção **Usar balanceamento de carga** .  
  
 **SID**  
 Se estiver se conectando a um grupo de servidores com balanceamento de carga, especifique a ID do sistema para a conexão.  
  
> [!NOTE]  
>  Esta opção só estará disponível se você tiver selecionado a opção **Usar balanceamento de carga** .  
  
 **Diretório de log**  
 Habilite o log para os componentes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW.  
  
 Para habilitar o log, especifique um diretório para os arquivos de log que são criados antes e depois de cada chamada de função de RFC. (Esse recurso de registro cria muitos arquivos de log em formato XML. Como esses arquivos de log também contêm todas as linhas de dados que são transferidas, esses arquivos de log podem consumir uma grande quantidade de espaço em disco.)  
  
> [!IMPORTANT]  
>  Se os dados que são transferidos contêm informações confidenciais, os arquivos de log também conterão essas informações confidenciais.  
  
 Para especificar o diretório de log, você pode digitar o caminho de diretório manualmente ou clicar em **Procurar** e navegue até o diretório de log.  
  
 Se você não selecionar um diretório de log, o registro em log não será habilitado.  
  
 **Procurar**  
 Procurar para selecionar uma pasta para o diretório de log.  
  
 **Testar Conexão**  
 Teste a conexão usando os valores que você forneceu. Depois de clicar em **Testar Conexão**, uma caixa de mensagem aparecerá e indicará se a conexão foi bem-sucedida ou falhou.  
  
## <a name="see-also"></a>Consulte Também  
 [Componentes do Microsoft Connector 1.1 para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  
