---
title: Origem SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 749afb64-3567-4dc9-8431-783d650c25db
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 49912f010400e81fb120c5f8abd0dbc94718b999
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773574"
---
# <a name="sap-bw-source"></a>Origem SAP BW
  A fonte SAP BW é o componente de fonte do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW. Assim, a origem do SAP BW extrai dados de um sistema SAP Netweaver BW versão 7 e torna estes dados disponíveis para o fluxo de dados em um pacote do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Essa fonte tem uma saída e uma saída de erro.  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
 Para usar a origem do SAP BW, faça o seguinte:  
  
-   [Prepare os objetos do SAP Netweaver BW](#bkmk_Prepare_Objects)  
  
-   [Conecte-se ao sistema SAP Netweaver BW](#bkmk_Connect_Database)  
  
-   [Configure a origem do SAP BW](#bkmk_Configure_Source)  
  
##  <a name="bkmk_Prepare_Objects"></a> Preparando os objetos do SAP Netweaver BW que a origem exige  
 A origem do SAP BW exige que determinados objetos estejam no sistema SAP Netweaver BW antes que a origem possa funcionar. Se esses objetos ainda não existirem, siga estas etapas para criar e configurar esses objetos do sistema SAP Netweaver BW.  
  
> [!NOTE]  
>  Para obter detalhes adicionais sobre esses objetos e essas etapas de configuração, consulte a documentação do SAP Netweaver BW.  
  
1.  Faça logon como SAP Netweaver BW com a GUI do SAP, digite o código de transação SM59 e crie um destino de RFC:  
  
    1.  Para **Tipo de conexão**, selecione **TCP/IP**.  
  
    2.  Para **Tipo de Ativação**, selecione **Programa de Servidor Registrado**.  
  
    3.  Para **Communication Type with Target System (Tipo de Comunicação com o Sistema de Destino)**, selecione **Non-Unicode (Inactive MDMP Settings) (Não Unicode (configurações de MDMP inativo))**.  
  
    4.  Atribuir uma ID de programa apropriada  
  
2.  Crie um destino do Open Hub:  
  
    1.  Vá para o Administrator Workbench (código de transação RSA1) e, no painel esquerdo, selecione **Destino do Open Hub**.  
  
    2.  No painel central, clique com o botão direito do mouse em uma InfoArea e selecione **“Criar o destino do Open Hub”**.  
  
    3.  Para **Tipo de Destino**, selecione **“Ferramenta de Terceiros”** e insira o destino de RFC criado anteriormente.  
  
    4.  Salve e ative o novo destino do Open Hub.  
  
3.  Crie um processo de transferência de dados (DTP):  
  
    1.  No painel central da InfoArea, clique com o botão direito do mouse no destino criado anteriormente e selecione **“Criar o processo de transferência de dados”**.  
  
    2.  Configurar, salvar e ativar o DTP.  
  
    3.  No menu, clique em **Ir para**e clique em **Configurações do Gerenciador de Lotes**.  
  
    4.  Atualizar **Número de Processos** para 1 para o processamento em série.  
  
4.  Crie uma cadeia de processo:  
  
    1.  Ao configurar a cadeia de processo, selecione **Iniciar usando a cadeia ou a API de metadados** como **Opções de Agendamento** de **Iniciar Processo**e adicione o DTP criado anteriormente como o nó subsequente.  
  
    2.  Salvar e ativar a cadeia do processo.  
  
     A origem do SAP BW pode chamar a cadeia de processo para ativar o processo de transferência de dados.  
  
##  <a name="bkmk_Connect_Database"></a> Conectando-se ao sistema SAP Netweaver BW  
 Para conectar-se ao sistema SAP Netweaver BW versão 7, a origem do SAP BW usará o gerenciador de conexões do SAP BW que faz parte do pacote do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW. O gerenciador de conexões do SAP BW é o único gerenciador de conexões do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que a origem do SAP BW pode usar.  
  
 Para obter mais informações sobre o gerenciador de conexões do SAP BW, consulte [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
##  <a name="bkmk_Configure_Source"></a> Configurando a origem do SAP BW  
 Você pode configurar a origem do SAP BW das seguintes formas:  
  
-   Pesquise e selecione o destino do OHS (Open Hub Service) a ser usado para extrair dados.  
  
-   Selecione um dos seguintes métodos para extrair dados:  
  
    -   Disparar uma cadeia de processo. Nesse caso, o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inicia o processo de extração.  
  
    -   Aguarde a notificação do sistema SAP Netweaver BW para iniciar uma extração. Nesse caso, o sistema do SAP Netweaver BW inicia o processo de extração.  
  
    -   Recupere os dados associados a uma ID de solicitação específica Nesse caso, o sistema SAP Netweaver BW já extraiu os dados para uma tabela interna e o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] apenas lê os dados.  
  
-   Dependendo do método selecionado para extrair dados, forneça as seguintes informações adicionais:  
  
    -   Para a opção **P - Disparar Cadeia de Processo** , forneça o nome do host do gateway, o nome do serviço de gateway, a ID do programa para o destino do RFC e o nome da cadeia do processo.  
  
    -   Para a opção **A - Aguardar Notificação** , forneça o nome do host do gateway, o nome do servidor do gateway e a ID do programa para o destino do RFC. Você também pode especificar o tempo limite (em segundos). O tempo limite é o período de tempo máximo que a origem aguardará para ser notificada.  
  
    -   Para a opção **E - Extrair Somente** , forneça a ID da solicitação.  
  
-   Especifique as regras para conversão de cadeia de caracteres. (Por exemplo, converter todas as cadeias de caracteres dependendo se o sistema SAP Netweaver BW é Unicode ou não, ou converter todas as cadeias de caracteres para **varchar** ou **nvarchar**).  
  
-   Use as opções que você selecionou para visualizar os dados que serão extraídos.  
  
 Você também pode habilitar o log das chamadas de função de RFC pela origem. (Esse log é separado do log opcional que você pode habilitar em pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].) Você habilita o log das chamadas de função de RFC quando configura o gerenciador de conexões do SAP BW que a origem usará. Para obter mais informações sobre como configurar o gerenciador de conexões do SAP BW, consulte [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
 Se você não souber todos os valores necessários para configurar a origem, talvez precise perguntar ao administrador do SAP.  
  
 Para obter um passo a passo que demonstre como configurar e usar o gerenciador de conexões do SAP BW, a origem e o destino, consulte o white paper [Usando o SQL Server 2008 Integration Services com SAP BI 7.0](http://go.microsoft.com/fwlink/?LinkID=137090). Este white paper também mostra como configurar os objetos necessários no SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>Usando o Designer SSIS para configurar a origem  
 Para obter mais informações sobre as propriedades da origem do SAP BW que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos tópicos a seguir:  
  
-   [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)  
  
-   [Editor de Origem SAP BW &#40;Página Colunas&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)  
  
-   [Editor de Origem SAP BW &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)  
  
-   [Editor de Origem SAP BW &#40;Página Avançado&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)  
  
 Quando você estiver configurando a origem do SAP BW, também poderá usar várias caixas de diálogo para pesquisar objetos do SAP Netweaver BW ou visualizar os dados da origem. Para obter mais informações sobre essas caixas de diálogo, clique em um dos seguintes tópicos:  
  
-   [Pesquisar destino RFC](../../integration-services/data-flow/look-up-rfc-destination.md)  
  
-   [Pesquisar cadeia de processo](../../integration-services/data-flow/look-up-process-chain.md)  
  
-   [Log de solicitações](../../integration-services/data-flow/request-log.md)  
  
-   [Visualização](../../integration-services/data-flow/preview.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Componentes do Microsoft Connector 1.1 para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  
