---
title: "Editor do Gerenciador de Conexão do SAP BW | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwconnectionmanager.f1
ms.assetid: ec970319-e749-4753-8675-9cf76ed99669
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a9f07a79e630550d7d0599026a91ee53f5b05d05
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-connection-manager-editor"></a>Editor do Gerenciador de Conexões de SAP BW
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
  
## <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar o gerenciador de conexões, talvez precise perguntar ao administrador do SAP.  
  
 **Cliente**  
 Especifique o número de cliente do sistema.  
  
 **Idioma**  
 Especifique o idioma que o sistema usará. Por exemplo, especifique **EN** para inglês.  
  
 **Nome de usuário**  
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
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
