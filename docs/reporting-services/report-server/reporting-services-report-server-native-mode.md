---
title: "Servidor de relatório do Reporting Services (modo nativo) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administering Reporting Services
- administering [Reporting Services]
- Reporting Services, administration
ms.assetid: fa0d84e2-4c21-432c-aa7c-23517da75253
caps.latest.revision: "24"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 65acea8f2887a2c45553c69d8d53ecfeb65e96a5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="reporting-services-report-server-native-mode"></a>Reporting Services Report Server (Native Mode)
  Um servidor de relatório configurado para o modo nativo como um servidor de aplicativo que fornece todos os recursos de processamento e gerenciamento exclusivamente através de componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 É possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou o Gerenciador de Relatórios para administrar relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Use o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para gerenciar um servidor de relatório em Modo Nativo.  
  
 Se o servidor de relatório estiver configurado no modo do SharePoint, será necessário usar as páginas de gerenciamento de conteúdo no site do SharePoint para gerenciar relatórios, fontes de dados compartilhadas e outros itens do servidor de relatório.  
  
 Este tópico inclui as informações a seguir:  
  
-   [Resumo do modo nativo](#bkmk_sum)  
  
-   [Gerenciando conteúdo](#bkmk_managecontent)  
  
-   [Gerenciamento e segurança de um recurso](#bkmk_manageresources)  
  
-   [Fazendo referência a um recurso de imagem de um relatório](#bkmk_referenceimage)  
  
##  <a name="bkmk_sum"></a> Resumo do modo nativo  
 Uma instalação em modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consiste em vários recursos do servidor que são necessários administrar e manter. Os recursos de servidor são os seguintes:  
  
-   O serviço Web Servidor de Relatórios, executado dentro do serviço Servidor de Relatório.  
  
-   Os aplicativos de processamento em segundo plano, que controlam operações agendadas e entrega de relatórios.  
  
-   O banco de dados do servidor de relatório.  
  
 Para administrar totalmente uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , é necessário ter as seguintes permissões:  
  
-   Inscrição no grupo Administrador local no computador do servidor de relatório. Se a instalação incluir recursos do servidor que são executados em computadores remotos, será necessário ter permissões de administrador nesses computadores para gerenciar os servidores através de uma conexão remota.  
  
-   Permissões de administrador de banco de dados para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados.  
  
-   Se você estiver instalando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um controlador de domínio, será necessário ser um administrador de domínio.  
  
##  <a name="bkmk_managecontent"></a> Gerenciando conteúdo  
 No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o gerenciamento de conteúdo refere-se ao gerenciamento de relatórios, modelos, pastas, recursos e fontes de dados compartilhadas. Todos esses itens podem ser gerenciados independentemente um do outro por propriedades e configurações de segurança. Qualquer item pode ser movido para um local diferente no namespace de pasta de servidor de relatório. Para gerenciar os itens com eficiência, você precisa saber quais tarefas são executadas por um gerenciador de conteúdo.  
  
> [!NOTE]  
>  O gerenciamento de conteúdo é diferente da administração de servidor de relatório. Para obter mais informações sobre como gerenciar o ambiente no qual um servidor de relatório é executado, consulte [Configuração e administração de um servidor de relatório &#40;modo do SharePoint do Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).  
  
 O gerenciamento de conteúdo inclui as seguintes tarefas:  
  
-   Proteger o site e os itens do servidor de relatório aplicando a segurança com base em funções fornecida com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Estruturar a hierarquia de pasta do servidor de relatório adicionando, modificando e excluindo pastas.  
  
-   Definir padrões e propriedades que se aplicam aos itens gerenciados pelo servidor de relatório. Por exemplo, você pode definir valores máximos de linha de base que determinam políticas de armazenamento do histórico de relatórios.  
  
-   Criar itens de fontes de dados compartilhadas que podem ser usados em vez de conexões de fonte de dados específicas do relatório. Um publicador ou gerenciador de conteúdo pode selecionar uma fonte de dados diferente da originalmente definida para um relatório; por exemplo, substituir uma referência de um banco de dados de teste por uma referência de um banco de dados de produção.  
  
-   Criar agendas compartilhadas que podem ser usadas em vez de agendas específicas do relatório e da assinatura, facilitando a manutenção das informações de agenda com o passar do tempo.  
  
-   Criar assinaturas controladas por dados que geram listas de destinatários recuperando dados de um repositório de dados.  
  
-   Equilibrar as demandas de processamento de relatórios feitas pelo servidor agendando o processamento do relatório e especificando quais podem ser executados sob demanda e quais serão carregados a partir do cache.  
  
 A permissão para executar tarefas de gerenciamento é fornecida por duas funções predefinidas: **Administrador do Sistema** e **Gerenciador de Conteúdo**. O gerenciamento eficaz do conteúdo do servidor de relatório requer que você tenha as duas funções. Para obter mais informações sobre essas funções predefinidas, consulte [Funções e permissões &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md).  
  
 Ferramentas para gerenciar o conteúdo do servidor de relatórios incluem [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou Gerenciador de Relatórios. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] permite definir padrões e habilitar recursos. O Gerenciador de Relatórios é usado para conceder acesso a itens e operações do servidor de relatório, exibir e usar relatórios e outros tipos de conteúdo e exibir e usar todos os itens compartilhados e recursos de distribuição de relatórios.  
  
##  <a name="bkmk_manageresources"></a> Gerenciamento e segurança de um recurso  
 Um recurso é um item gerenciado armazenado, mas não processado, em um servidor de relatório. Normalmente, um recurso fornece conteúdo externo para usuários de relatórios. Alguns exemplos incluem uma imagem em um arquivo .jpg ou um arquivo HTML que descreve as regras de negócio usadas em um relatório. O arquivo JPG ou HTML é armazenado no servidor de relatórios, mas este passa o arquivo diretamente para o navegador, em vez de processá-lo antes.  
  
 Para adicionar um recurso a um servidor de relatórios, você carrega ou publica um arquivo:  
  
|Operação|Tipo de arquivo|  
|---------------|---------------|  
|Carregar|Todos os arquivos são carregados como recursos, exceto arquivos de definição de relatório (.rdl) e modelo de relatório (.smdl).<br /><br /> Para carregar um recurso, é necessário usar o Gerenciador de Relatórios se o servidor de relatório estiver sendo executado no modo nativo ou por uma página de aplicativo em um site do SharePoint, se servidor for executado no modo integrado do SharePoint. Para obter mais informações, consulte [Carregar um arquivo ou relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md) ou [Carregar documentos em uma biblioteca do SharePoint &#40;Reporting Services no modo do SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md).|  
|Publicar|Todos os arquivos em um projeto são carregados como recursos, exceto pelos arquivos .rdl, .smdl e .rds da fonte de dados. Para publicar um recurso, adicione um item existente a um projeto no Designer de Relatórios e publique o projeto em um servidor de relatório.|  
  
 Todos os recursos são gerados como arquivos em um sistema de arquivos, que são carregados subsequentemente em um servidor de relatório. Exceto pelas limitações de tamanho de arquivo padrão de 4 megabytes impostas pelo ASP.NET, não há restrições quanto ao tipo de arquivo que pode ser carregado. Entretanto, quando publicados em um servidor de relatório como recursos, tipos de arquivo com tipos MIME equivalentes são melhores que outros. Por exemplo, recursos com base em arquivos HTML e JPG serão abertos em uma janela de navegador quando o usuário clicar no recurso, renderizando o HTML como uma página da Web e o JPG como uma imagem que pode ser visualizada pelo usuário. De outro modo, recursos que não possuem tipos MIME equivalentes, como arquivos de aplicativos de desktop, por exemplo, talvez não sejam renderizados em uma janela do navegador.  
  
 Um recurso poder ser visualizado por usuários de relatórios dependendo dos recursos de exibição do navegador. Como recursos não são processados pelo servidor de relatório, é necessário que o navegador forneça o recurso de exibição para renderizar o tipo MIME específico. Se o navegador não for capaz de renderizar o conteúdo, os usuários que visualizam o recurso conseguirão visualizar somente as propriedades gerais do recurso.  
  
 Recursos existem em relatórios, fontes de dados compartilhadas, agendas compartilhadas e pastas como itens nomeados na hierarquia de pasta do servidor de relatório. É possível procurar, exibir, proteger e definir propriedades em recursos assim como acontece com qualquer outro item armazenado em um servidor de relatório. Para visualizar ou gerenciar um recurso, é necessário ter a tarefa Exibir recursos ou a tarefa Gerenciar recursos na sua atribuição de função.  
  
##  <a name="bkmk_referenceimage"></a> Fazendo referência a um recurso de imagem de um relatório  
 Recursos podem conter uma imagem à qual você faz referência em um relatório. Se as exigências de relatório incluírem o uso de imagens externas, considere as seguintes vantagens de armazenar a imagem como recurso:  
  
-   Armazenamento centralizado no banco de dados do servidor de relatório. Se você mover o banco de dados do servidor de relatório e seu conteúdo, a imagem externa permanecerá com o relatório. Não é necessário rastrear os arquivos de imagem armazenados em disco em computadores diferentes.  
  
-   Segurança através de atribuições de função, e não por segurança do sistema de arquivos. As mesmas permissões usadas para exibir um relatório podem ser aplicadas ao recurso. Em contrapartida, se a imagem for armazenada em disco, é necessário certificar-se de que a conta de usuário Anônimo ou a conta de execução autônoma tem permissão para acessar o arquivo.  
  
 Para usar um recurso de imagem em um relatório, adicione o arquivo de imagem ao projeto e publique-o juntamente com o relatório. Quando a imagem for publicada, será possível atualizar a referência da imagem no relatório de modo que aponte para o recurso no servidor de relatório. Sendo assim, somente publique novamente o relatório para salvar as alterações. Você poderá atualizar subsequentemente a imagem, independentemente do relatório, republicando o recurso. O relatório usa a versão mais atual da imagem disponível no servidor de relatórios.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Solucionar um problema da instalação do Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
  
  
