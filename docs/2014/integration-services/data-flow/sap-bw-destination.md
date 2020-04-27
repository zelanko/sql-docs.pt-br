---
title: Destino SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a612ed91-b89b-4173-a0b1-0bce381e1e28
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1cac8403327ecf3888439290554f059bb00bce2c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770848"
---
# <a name="sap-bw-destination"></a>Destino SAP BW
  O destino SAP BW é o componente de destino do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW. Portanto, o destino do SAP BW carrega dados do fluxo de dados em um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um sistema SAP Netweaver BW versão 7.  
  
 Esse destinos tem uma entrada e uma saída de erro.  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 Para usar o destino SAP BW, faça o seguinte:  
  
-   [Prepare os objetos do SAP Netweaver BW](#bkmk_Prepare_Objects)  
  
-   [Conecte-se ao sistema SAP Netweaver BW](#bkmk_Connect_Database)  
  
-   [Configure o destino SAP BW](#bkmk_Configure_Destination)  
  
##  <a name="preparing-the-sap-netweaver-bw-objects-that-the-destination-requires"></a><a name="bkmk_Prepare_Objects"></a> Preparando os objetos do SAP Netweaver BW que o destino exige  
 O destino SAP BW exige que determinados objetos estejam no sistema SAP Netweaver BW antes que o destino possa funcionar. Se esses objetos ainda não existirem, siga estas etapas para criar e configurar esses objetos do sistema SAP Netweaver BW.  
  
> [!NOTE]  
>  Para obter detalhes adicionais sobre esses objetos e essas etapas de configuração, consulte a documentação do SAP Netweaver BW.  
  
1.  Criar um novo sistema de origem:  
  
    1.  Selecione o tipo, **"Third Party/Staging BAPIs" (Terceiros/BAPIs de preparo)** .  
  
    2.  Para **Communication Type with Target System (Tipo de Comunicação com o Sistema de Destino)** , selecione **Non-Unicode (Inactive MDMP Settings) (Não Unicode (configurações de MDMP inativo))** .  
  
    3.  Atribuir uma ID de programa apropriada  
  
2.  Atribua o sistema de origem a um InfoSource.  
  
3.  Crie um InfoPackage.  
  
     O InfoPackage é o objeto mais importante que é exigido pelo destino SAP BW.  
  
 Você também pode criar InfoObjects, InfoCubes, InfoSources e InfoPackages adicionais que são necessários para oferecer suporte ao carregamento de dados no sistema SAP Netweaver BW.  
  
##  <a name="connecting-to-the-sap-netweaver-bw-system"></a><a name="bkmk_Connect_Database"></a> Conectando-se ao sistema SAP Netweaver BW  
 Para conectar-se ao sistema SAP Netweaver BW versão 7, o destino do SAP BW usará o gerenciador de conexões do SAP BW que faz parte do pacote do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW. O gerenciador de conexões do SAP BW é o único gerenciador de conexões do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que o destino do SAP BW pode usar.  
  
 Para obter mais informações sobre o gerenciador de conexões do SAP BW, consulte [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md).  
  
##  <a name="configuring-the-sap-bw-destination"></a><a name="bkmk_Configure_Destination"></a> Configurando o destino SAP BW  
 É possível configurar o destino do SAP BW das seguintes maneiras:  
  
-   Pesquise e selecione o InfoPackage a ser usado para carregar dados.  
  
-   Mapeie cada coluna no fluxo de dados para o InfoObject apropriado no InfoPackage.  
  
-   Especifique quantas linhas de dados serão transferidas de cada vez configurando a propriedade `PackageSize`.  
  
-   Escolha para aguardar até que o carregamento dos dados esteja concluído pelo sistema SAP Netweaver BW.  
  
-   Escolha não acionar o InfoPackage, mas aguardar a notificação que o sistema SAP Netweaver BW iniciou o carregamento dos dados.  
  
-   Opcionalmente, acione uma outra cadeia de processo depois que o carregamento dos dados estiver concluído.  
  
-   Opcionalmente, crie os objetos do SAP Netweaver BW exigidos pelo destino. Isso inclui a criação de InfoObjects, InfoCubes, InfoSources e InfoPackages.  
  
-   Teste o carregamento de dados com as opções que você selecionou.  
  
 Você também pode habilitar o log das chamadas de função de RFC pelo destino. (Esse log é separado do log opcional que você pode habilitar em pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .) Você habilita o log das chamadas de função de RFC quando configura o gerenciador de conexões do SAP BW que o destino usará. Para obter mais informações sobre como configurar o gerenciador de conexões do SAP BW, consulte [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md).  
  
 Se você não souber todos os valores necessários para configurar o destino, talvez precise perguntar ao administrador do SAP.  
  
 Para obter um passo a passo que demonstre como configurar e usar o gerenciador de conexões do SAP BW, a origem e o destino, consulte o white paper [Usando o SQL Server 2008 Integration Services com SAP BI 7.0](https://go.microsoft.com/fwlink/?LinkID=137090). Este white paper também mostra como configurar os objetos necessários no SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-destination"></a>Usando o Designer SSIS para configurar o destino  
 Para obter mais informações sobre as propriedades do destino do SAP BW que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos tópicos a seguir:  
  
-   [Editor de Destino SAP BW &#40;Página Gerenciador de Conexões&#41;](sap-bw-destination-editor-connection-manager-page.md)  
  
-   [Editor de Destino SAP BW &#40;Página Mapeamentos&#41;](sap-bw-destination-editor-mappings-page.md)  
  
-   [Editor de Destino SAP BW &#40;Página Saída de Erro&#41;](sap-bw-destination-editor-error-output-page.md)  
  
-   [Editor de Destino SAP BW &#40;Página Avançado&#41;](sap-bw-destination-editor-advanced-page.md)  
  
 Quando você estiver configurando o destino do SAP BW, também poderá usar várias caixas de diálogo para pesquisar ou criar objetos do SAP Netweaver BW. Para obter mais informações sobre essas caixas de diálogo, clique em um dos seguintes tópicos:  
  
-   [Pesquisar InfoPackage](look-up-infopackage.md)  
  
-   [Criar novo InfoObject](create-new-infoobject.md)  
  
-   [Criar InfoCube para os dados da transação](create-infocube-for-transaction-data.md)  
  
-   [Pesquisar InfoObject](look-up-infoobject.md)  
  
-   [Criar InfoSource](create-infosource.md)  
  
-   [Criar InfoSource para os dados da transação](create-infosource-for-transaction-data.md)  
  
-   [Criar InfoSource para dados mestre](create-infosource-for-master-data.md)  
  
-   [Criar InfoPackage](create-infopackage.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Componentes do Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-components.md)  
  
  
