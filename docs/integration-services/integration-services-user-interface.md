---
title: Interface do usuário do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- tools [Integration Services], SSIS Designer
- SSIS Designer
- SSIS, SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: d2c48cff-46f4-4c70-b1f3-c88f9b8757f3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 183c95bf39c504c7444f1604206f5acef517a53d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71284164"
---
# <a name="integration-services-user-interface"></a>Interface do usuário do Integration Services

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Além das superfícies de design nas guias do Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] , a interface do usuário fornece acesso às seguintes janelas e caixas de diálogo para adicionar recursos a pacotes e configurar as propriedades de objetos do pacote:  
  
-   As caixas de diálogo e janelas usadas para adicionar funcionalidades, como log e configurações, a pacotes.  
  
-   Os editores personalizados para configurar as propriedades de objetos de pacote. Quase todo tipo de contêiner, tarefa e componente de fluxo de dados tem seu próprio editor personalizado.  
  
-   A caixa de diálogo **Editor Avançado** , um editor genérico que fornece opções de configuração mais detalhadas para muitos componentes de fluxo de dados.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] também fornece janelas e caixas de diálogo para configurar o ambiente e trabalhar com pacotes.  
  
## <a name="dialog-boxes-and-windows"></a>Caixas de diálogo e janelas  
 Depois que você abre um pacote ou cria um novo pacote no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , as caixas de diálogo e janelas a seguir se tornam disponíveis.  
  
 Esta tabela relaciona as caixas de diálogo disponíveis no menu **SSIS** e as superfícies de design do Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
|Caixa de diálogo|Finalidade|Acesso|  
|----------------|-------------|------------|  
|**Introdução**|Acesse exemplos, tutoriais e vídeos.|Na superfície de design da guia **Fluxo de Controle** ou da guia **Fluxo de Dados** , clique com o botão direito do mouse e clique em **Guia de Introdução**.<br /><br /> Para exibir automaticamente a janela **Guia de Introdução** ao criar um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selecione **Sempre mostrar no novo projeto** na parte inferior da janela.|  
|**Configurar Logs de SSIS**|Configure o log de um pacote e suas tarefas com a adição de logs e a definição dos detalhes do log.|No menu **SSIS** , clique em **Registrar em Log**.<br /><br /> -ou-<br /><br /> Clique com o botão direito do mouse na superfície de design da guia **Fluxo de Controle** e clique em **Log**.|  
|**Organizador de Configurações do Pacote**|Adicionar e editar configurações de pacote. Você executa o Assistente de Configuração de Pacotes nesta caixa de diálogo.|No menu **SSIS** , clique em **Configurações do Pacote**.<br /><br /> -ou-<br /><br /> Clique com o botão direito do mouse em qualquer lugar na superfície de design da guia **Fluxo de Controle** e clique em **Configurações de Pacote**.|  
|**Assinatura Digital**|Assine um pacote ou remova a assinatura do pacote.|No menu **SSIS** , clique em **Assinatura Digital**.<br /><br /> -ou-<br /><br /> Clique com o botão direito do mouse em qualquer lugar na superfície de design da guia **Fluxo de Controle** e clique em **Assinatura Digital**.|  
|**Definir pontos de interrupção**|Habilite pontos de interrupção em tarefas e defina propriedades do ponto de interrupção.|Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse em uma tarefa ou um contêiner e clique em **Editar Pontos de Interrupção**. Para definir pontos de interrupção no pacote, clique com o botão direito do mouse em qualquer lugar da superfície de design da guia **Fluxo de Controle** e clique em **Editar Pontos de Interrupção**.|  
  
 A janela **Guia de Introdução** fornece links para exemplos, tutoriais e vídeos. Para adicionar links para conteúdo adicional, modifique o arquivo SamplesSites.xml fornecido com a versão atual do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. É recomendável não modificar o valor do elemento \<GettingStartedSamples> que especifica a URL do RSS Feed. O arquivo está localizado na pasta *\<unidade>* :\Arquivos de Programas\Microsoft SQL Server\110\DTS\Binn. Em um computador de 64 bits, o arquivo está localizado na pasta *\<unidade>* :\Arquivos de Programas(x86)\Microsoft SQL Server\110\DTS\Binn  
  
 Se o arquivo SamplesSites.xml se tornar corrompido, substitua o xml no arquivo pelo seguinte xml padrão.  
  
 `<?xml version="1.0" ?>`  
  
 `- <SamplesSites>`  
  
 `<GettingStartedSamples>https://go.microsoft.com/fwlink/?LinkID=203147</GettingStartedSamples>`  
  
 `- <ToolboxSamples>`  
  
 `<Site>https://go.microsoft.com/fwlink/?LinkID=203286&query=SSIS%20{0}</Site>`  
  
 `</ToolboxSamples>`  
  
 `</SamplesSites>`  
  
 Esta tabela relaciona as janelas disponíveis nos menus **SSIS** e **Exibir** e as superfícies de design do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
|Janela|Finalidade|Acesso|  
|------------|-------------|------------|  
|**Variáveis**|Adicionar e administrar variáveis personalizadas.|No menu **SSIS** , clique em **Variáveis**.<br /><br /> -ou-<br /><br /> Clique com o botão direito do mouse em qualquer lugar na superfície de design das guias **Fluxo de Controle** e **Fluxo de Dados** e clique em **Variáveis**.<br /><br /> -ou-<br /><br /> No menu **Exibir** , aponte para **Outras Janelas**e clique em **Variáveis**.|  
|**Eventos de Log**|Exibir entradas de log em tempo de execução.|No menu **SSIS** , clique em **Eventos de Log**.<br /><br /> -ou-<br /><br /> Clique com o botão direito do mouse em qualquer lugar na superfície de design das guias **Fluxo de Controle** e **Fluxo de Dados** e clique em **Eventos de Log**.<br /><br /> -ou-<br /><br /> No menu **Exibir** , aponte para **Outras Janelas**e clique em **Eventos de Log**.|  
  
## <a name="custom-editors"></a>Editores personalizados  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece uma caixa de diálogo personalizada para a maioria dos contêineres, tarefas, fontes, transformações e destinos.  
  
 A tabela a seguir descreve como acessar caixas de diálogo personalizadas.  
  
|Tipo de editor|Acesso|  
|-----------------|------------|  
|Contêiner. Para obter mais informações, consulte [Contêineres do Integration Services](../integration-services/control-flow/integration-services-containers.md).|Na superfície de design da guia **Fluxo de Controle** , clique duas vezes no contêiner.|  
|Tarefa. Para obter mais informações, consulte [Tarefas do Integration Services](../integration-services/control-flow/integration-services-tasks.md).|Na superfície de design da guia **Fluxo de Controle** , clique duas vezes na tarefa.|  
|Fonte.|Na superfície de design da guia **Fluxo de Controle** , clique duas vezes na fonte.|  
|Transformação. Para obter mais informações, consulte [Integration Services Transformations](../integration-services/data-flow/transformations/integration-services-transformations.md).|Na superfície de design da guia **Fluxo de Controle** , clique duas vezes na transformação.|  
|Destino.|Na superfície de design da guia **Fluxo de Dados** , clique duas vezes no destino.|  
  
## <a name="advanced-editor"></a>Editor Avançado  
 A caixa de diálogo **Editor Avançado** é uma interface do usuário para configurar componentes de fluxo de dados. Ela reflete as propriedades do componente usando um layout genérico. A caixa de diálogo **Editor Avançado** não está disponível para transformações do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com várias entradas.  
  
 Para abrir esse editor, clique em **Editor ShowAdvanced** na janela **Propriedades** ou clique com o botão direito do mouse em um componente do fluxo de dados e, em seguida, clique em **Editor ShowAdvanced**.  
  
 Se você criar uma fonte, transformação ou destino personalizados mas não quiser gravar uma interface do usuário personalizada, poderá usar então o **Editor Avançado** .  
  
## <a name="sql-server-data-tools-features"></a>Recursos das Ferramentas de Dados do SQL Server  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fornece janelas, caixas de diálogo e opções de menu para trabalhar com pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 A seguir há um resumo das janelas e menus disponíveis:  
  
-   A janela **Gerenciador de Soluções** relaciona projetos, inclusive o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no qual você desenvolve pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , e arquivos de projeto.  
  
     Para classificar por nome os pacotes contidos em um projeto, clique com o botão direito do mouse no nó **Pacotes SSIS** e clique em **Classificar por nome**.  
  
-   A janela **Caixa de Ferramentas** relaciona os itens de fluxo de controle e de fluxo de dados para criar fluxos de controle e de dados.  
  
-   A janela **Propriedades** relaciona propriedades de objeto.  
  
-   O menu **Formatar** fornece opções para dimensionar e alinhar controles em um pacote.  
  
-   O menu **Editar** fornece as funcionalidades de copiar e colar para copiar objetos nas superfícies de design.  
  
-   O menu **Exibir** fornece opções para modificar a representação gráfica de objetos no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)]  
  
 Para obter mais informações sobre janelas e menus adicionais, consulte a documentação do Visual Studio.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como criar pacotes no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], consulte [Copiar pacotes no SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Designer SSIS](../integration-services/ssis-designer.md)  
  
  
