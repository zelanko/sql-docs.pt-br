---
title: Gerenciamento de conteúdo do servidor de relatório (modo nativo) | Microsoft Docs
ms.date: 06/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- administering Reporting Services
- published reports [Reporting Services], managing
- report servers [Reporting Services], content management
- content management [Reporting Services]
ms.assetid: 641961ac-53a5-4997-9d42-cf4ecce1f892
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 78fb75acfefce3a1f0c8cb28ea286a028463a56b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286380"
---
# <a name="report-server-content-management-ssrs-native-mode"></a>Gerenciamento do Conteúdo do Servidor de Relatório (Modo Nativo SSRS)
No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o gerenciamento de conteúdo se refere ao gerenciamento de itens de servidor de relatório. Todos os itens podem ser gerenciados independentemente um do outro por propriedades e configurações de segurança. Qualquer item pode ser movido para um local diferente no namespace de pasta de servidor de relatório. Para gerenciar os itens com eficiência, você precisa saber quais tarefas são executadas por um gerenciador de conteúdo. Do SQL Server 2016 Reporting Services ou posterior (SSRS) CTP 3.2 em diante, o portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está disponível. Este artigo analisa o portal da Web e a experiência do novo portal da Web.  
  
> [!NOTE]  
> O gerenciamento de conteúdo é diferente da administração de servidor de relatório. Para obter mais informações sobre como gerenciar o ambiente em que um servidor de relatório é executado, consulte [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
 O gerenciamento de conteúdo inclui as seguintes tarefas:  
  
-   Proteger o site e os itens do servidor de relatório aplicando a segurança com base em funções fornecidas com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Criar a hierarquia de pastas do servidor de relatório adicionando, modificando e excluindo pastas.  
  
-   Definir valores padrão e propriedades que se aplicam aos itens gerenciados pelo servidor de relatório. Por exemplo, você pode definir valores máximos de linha de base que determinam políticas de armazenamento do histórico de relatórios.  
  
-   Criar itens de fontes de dados compartilhadas que podem ser usados em vez de conexões de fonte de dados específicas do relatório. Um publicador ou gerenciador de conteúdo pode selecionar uma fonte de dados diferente da originalmente definida para um relatório; por exemplo, substituir uma referência de um banco de dados de teste por uma referência de um banco de dados de produção.  
  
-   Criar agendas compartilhadas que podem ser usadas em vez de agendas específicas do relatório e da assinatura, facilitando a manutenção das informações de agenda com o passar do tempo.  
  
-   Criar assinaturas controladas por dados que geram listas de destinatários recuperando dados de um armazenamento de dados.  
  
-   Equilibrar as demandas de processamento de relatórios feitas pelo servidor agendando o processamento do relatório e especificando quais podem ser executados sob demanda e quais serão carregados por meio do cache.  
  
-   Fornecer permissão para executar tarefas de gerenciamento usando funções predefinidas: **Administrador do Sistema** e **Gerenciador de Conteúdo**. O gerenciamento eficaz do conteúdo do servidor de relatório requer que você tenha as duas funções.  
  
Ferramentas para gerenciar o conteúdo do servidor de relatório incluem [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e o portal da Web. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] permite definir padrões e habilitar recursos. O portal da Web é usado para conceder acesso a itens e operações do servidor de relatório, exibir e usar relatórios e outros tipos de conteúdo e exibir e usar todos os itens compartilhados e recursos de distribuição de relatórios. O portal da Web é um site atualizado que contém grande parte da funcionalidade do Gerenciador de Relatórios preterido. Para obter mais informações, consulte [Ferramentas do Reporting Services](../../reporting-services/tools/reporting-services-tools.md).  
  
##  <a name="report-server-items"></a><a name="bkmk_ReportServerItems"></a> Itens do servidor de relatório  
 Os itens de servidor de relatório incluem relatórios, fontes de dados compartilhadas, conjuntos de dados compartilhados, partes de relatórios, recursos (itens armazenados, mas não processados por um servidor de relatório) e pastas. Os itens podem depender de outros itens, por exemplo, um relatório pode depender d fontes de dados compartilhadas que referencia. Se você mover um item dependente, o servidor de relatório atualizará as informações de referência automaticamente.  
  
 Você pode mover itens do servidor de relatório para locais de pasta diferentes na hierarquia de pastas do servidor de relatório. Quando você move um item, todas as propriedades (inclusive configurações de segurança) são movidas com o item para o novo local. Ao mover uma pasta, todos os itens na pasta são movidos juntos.  
  
> [!NOTE]  
>  Para o CTP 3.2, se quiser mover o local de um item, você precisará realizar essa ação no portal da Web.  
  
 No portal da Web, os itens que podem ser movidos estão indicados na hierarquia de pastas. A imagem a seguir mostra o ícone para cada item móvel.  
  
  ![Ícones do servidor de relatório para itens que podem ser movidos](media/report-server-content-management-ssrs-native-mode/report-server-content-icons.png)

 Nem todos os itens com os quais você trabalha podem ser movidos. Não é possível mover itens associados a um relatório, como assinaturas ou histórico de relatório. Esses itens são movidos com os seus relatórios associados. De maneira semelhante, não é possível mover itens, como agendas compartilhadas, que existem fora da hierarquia de pasta. Não é possível mover itens sem a devida permissão. A permissão para mover um item é concedida quando as seguintes tarefas são selecionadas na atribuição de função para o item em questão: "Gerenciar relatórios", "Gerenciar pastas" e "Gerenciar fontes de dados".  
  
##  <a name="folders"></a><a name="bkmk_Folders"></a> Pastas  
 Uma hierarquia de pastas é usada para tratar itens que são armazenados e gerenciados por um servidor de relatório.  Por padrão, a estrutura de pastas consiste em um nó raiz denominado Página Inicial e em pastas reservadas que dão suporte ao recurso opcional Meus Relatórios. Pastas adicionais são definidas pelo usuário. As pastas do servidor de relatórios serão úteis se você quiser conceder o mesmo nível de acesso a vários itens. As permissões que você define na pasta podem ser herdadas por itens na pasta e por pastas adicionais ramificadas dessa pasta. Por exemplo, você pode criar um conjunto de pastas na pasta Base, atribuir permissões de equipe a cada pasta e permitir que os membros da equipe personalizem pastas sob a pasta de equipe quando necessário.  
  
 Se estiver usando um navegador para conectar-se diretamente a um servidor de relatório da estrutura de pastas, o nó raiz terá o nome do diretório virtual do servidor de relatório. No nó raiz, você pode criar, modificar e excluir pastas conforme necessário para organizar o conteúdo do servidor de relatório. Você pode adicionar conteúdo a uma pasta, mover itens entre pastas, modificar nomes ou locais de pasta e excluir pastas que não são mais necessárias.  
  
 As pastas são contêineres virtuais para itens publicados que você acessa pelo portal da Web ou por uma conexão de navegador com o servidor de relatório. Nem as pastas nem seus conteúdos realmente existem em um sistema de arquivos. Na verdade, eles são armazenados no banco de dados do servidor de relatório e acessados pelo ponto de extremidade do serviço Web Servidor de Relatórios. O namespace da pasta do servidor de relatório é uma hierarquia que inclui um nó raiz, pastas predefinidas e pastas definidas pelo usuário. O namespace identifica exclusivamente os itens que são armazenados em um servidor de relatório. Ele fornece um esquema de endereçamento para especificar itens em uma URL. Quando você seleciona ou localiza um relatório, o caminho da pasta se torna parte da URL para esse relatório.  
  
 O modo de trabalho com pastas depende das tarefas que fazem parte de sua atribuição de função. Se você estiver usando a segurança padrão, gerenciadores e editores de conteúdo podem criar e gerenciar pastas. Se atribuições de função personalizadas forem utilizadas, a atribuição de função deve incluir tarefas que ofereçam suporte para o gerenciamento de pastas. Para obter mais informações sobre atribuições de funções e tarefas, consulte [Concedendo permissões em um Servidor de Relatório no modo Nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md) e [Tarefas e Permissões](../../reporting-services/security/tasks-and-permissions.md).  
  
 As pastas do servidor de relatório podem conter os seguintes itens:  
  
-   Relatórios  
  
-   Fontes de dados compartilhadas  
  
-   Conjuntos de dados compartilhados  
  
-   Partes de relatório  
  
-   KPIs  
  
-   Relatórios móveis  
  
-   Recursos (itens que são armazenados mas não são processados por um servidor de relatório)  
  
-   Outras pastas  
  
### <a name="reserved-folders"></a>Pastas reservadas  
 Pastas predefinidas são reservadas pelo Reporting Services; elas não podem ser movidas, renomeadas ou excluídas. As pastas definidas pelo usuário incluem qualquer pasta criada por um usuário ou administrador do servidor de relatórios com permissão para adicionar itens a uma pasta.  
  
 A tabela a seguir descreve as pastas predefinidas que ancoram a hierarquia de pastas e fornecem uma estrutura para vários recursos.  
  
|Pasta|Finalidade|  
|------------|-------------|  
|Home|O nó raiz da hierarquia de pastas.|  
|Usuários|Esta pasta aparece quando você habilita o recurso Meus Relatórios. Ela contém subpastas para todos os usuários que usam o recurso Meus Relatórios e está acessível somente para administradores do servidor de relatórios. Cada nome de subpasta corresponde ao nome do usuário.|  
|Meus Relatórios|Fornece um workspace pessoal para cada usuário.|  
  
### <a name="creating-folders"></a>Criar pastas  
 Você pode criar uma pasta em qualquer pasta disponível na hierarquia.  
  
 Se você estiver criando pastas com a finalidade de restringir o acesso a relatórios e modelos específicos, especifique atribuições de funções que permitam aos usuários procurar, mas não exibir o conteúdo de pastas pai que estão no caminho da pasta.  
  
### <a name="modifying-folder-properties"></a>Modificar propriedades de pasta  
 Após criar uma pasta, você pode modificar propriedades para renomear a pasta, adicionar ou modificar a descrição ou mover a pasta para outro local. Estas propriedades estão disponíveis na página Propriedades gerais da pasta. Para obter mais informações sobre como definir propriedades que concedem acesso a uma pasta, consulte [Proteger Pastas](../../reporting-services/security/secure-folders.md).  
  
### <a name="deleting-folders-and-folder-contents"></a>Excluir pastas e conteúdos de pasta  
 Ao excluir uma pasta, você exclui todos os itens contidos nela. Antes de excluir uma pasta, observe o conteúdo para determinar se a pasta contém itens que podem ser mencionados ou usados por outros itens em outra parte da hierarquia de pasta. Os itens mencionados incluem definições de relatório que oferecem suporte para relatórios vinculados, fontes de dados compartilhadas e recursos.  
  
 Se um relatório que tem um ou mais relatórios vinculados que fazem referência a ele for excluído, os relatórios vinculados ficarão inválidos após a exclusão. Não é possível determinar com antecedência quais relatórios vinculados serão afetados porque o relatório não retém informações sobre relatórios vinculados. No entanto, você pode revisar as propriedades de um relatório vinculado para descobrir em qual relatório ele é baseado. Por outro lado, os itens de fontes de dados compartilhadas listam todos os relatórios que usam o item atualmente, de modo que é possível determinar com facilidade se as informações de conexão estão em uso. Para obter mais informações, consulte [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md). Finalmente, os recursos que são usados por relatórios não identificam esses relatórios.  
  
 Antes de excluir uma pasta, verifique se é necessário manter o histórico de relatórios de algum relatório que está prestes a ser excluído ou uma construção específica do relatório (como uma assinatura controlada por dados). Se alguma dessas informações for necessária, retire o item da pasta antes de excluí-la.  
  
 A visibilidade de um item em uma pasta depende das atribuições de função (isto é, da permissão para exibir um item) e das opções de exibição habilitadas para uma pasta. No portal da Web, você pode definir a página Conteúdo para exibição de lista ou de detalhes. Em alguns casos, um relatório ou item pode estar oculto na exibição de lista. Não se esqueça de exibir uma pasta em detalhes antes de excluir seu conteúdo.  
  
##  <a name="resources"></a><a name="bkmk_Resources"></a> Recursos  
 Um recurso é um item gerenciado armazenado, mas não processado, em um servidor de relatório. Normalmente, um recurso fornece conteúdo externo para usuários de relatórios. Alguns exemplos incluem uma imagem em um arquivo .jpg, um arquivo de forma ESRI que contém dados espaciais ou um arquivo HTML que descreve as regras de negócio usadas em um relatório. O arquivo JPG, SHP ou HTML é armazenado no servidor de relatório, mas o servidor de relatório passa o arquivo diretamente ao navegador em vez de processá-lo antes. Para obter mais informações, confira [Imagens &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md) e a seção "Adicionando dados a um mapa" em [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
### <a name="adding-and-viewing-a-resource"></a>Adicionar e exibir um recurso  
 Para adicionar um recurso a um servidor de relatórios, você carrega ou publica um arquivo:  
  
|Operação|Tipo de arquivo|  
|---------------|---------------|  
|Carregar|Para carregar um recurso, será necessário usar o portal da Web se o servidor de relatório estiver sendo executado no modo nativo ou por uma página de aplicativo em um site do SharePoint, se o servidor for executado no modo integrado do SharePoint. Para saber mais, confira [Carregar um arquivo ou relatório no servidor de relatório](../../reporting-services/reports/upload-a-file-or-report-report-manager.md) ou [Carregar documentos em uma biblioteca do SharePoint &#40;Reporting Services no modo do SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md).|  
|Publicar|Todos os arquivos em um projeto que não são relatórios, partes de relatório, fontes de dados ou conjuntos de dados são carregados como recursos. Para publicar um recurso, adicione um item existente a um projeto no Designer de Relatórios e publique o projeto em um servidor de relatório.|  
  
 Todos os recursos são gerados como arquivos em um sistema de arquivos, que são carregados subsequentemente em um servidor de relatório. Exceto pelas limitações de tamanho de arquivo padrão de 4 megabytes impostas pelo ASP.NET, não há restrições quanto ao tipo de arquivo que pode ser carregado. Entretanto, quando publicados em um servidor de relatório como recursos, tipos de arquivo com tipos MIME equivalentes são melhores que outros. Por exemplo, recursos com base em arquivos HTML e JPG serão abertos em uma janela de navegador quando o usuário clicar no recurso, renderizando o HTML como uma página da Web e o JPG como uma imagem que pode ser visualizada pelo usuário. De outro modo, recursos que não possuem tipos MIME equivalentes, como arquivos de aplicativos de desktop, por exemplo, talvez não sejam renderizados em uma janela do navegador.  
  
 Um recurso poder ser visualizado por usuários de relatórios dependendo dos recursos de exibição do navegador. Como recursos não são processados pelo servidor de relatório, é necessário que o navegador forneça o recurso de exibição para renderizar o tipo MIME específico. Se o navegador não for capaz de renderizar o conteúdo, os usuários que visualizam o recurso conseguirão visualizar somente as propriedades gerais do recurso.  
  
### <a name="securing-and-managing-a-resource"></a>Proteger e gerenciar um recurso  
 Recursos existem em relatórios, fontes de dados compartilhadas, agendas compartilhadas e pastas como itens nomeados na hierarquia de pasta do servidor de relatório. É possível procurar, exibir, proteger e definir propriedades em recursos assim como acontece com qualquer outro item armazenado em um servidor de relatório. Para visualizar ou gerenciar um recurso, é necessário ter a tarefa Exibir recursos ou a tarefa Gerenciar recursos na sua atribuição de função.  
  
### <a name="referencing-an-image-resource-from-a-report"></a>Fazer referência a um recurso de imagem de um relatório  
 Recursos podem conter uma imagem à qual você faz referência em um relatório. Se as exigências de relatório incluírem o uso de imagens externas, considere as seguintes vantagens de armazenar a imagem como recurso:  
  
-   Armazenamento centralizado no banco de dados do servidor de relatório. Se você mover o banco de dados do servidor de relatório e seu conteúdo, a imagem externa permanecerá com o relatório. Não é necessário rastrear os arquivos de imagem armazenados em disco em computadores diferentes.  
  
-   Segurança através de atribuições de função, e não por segurança do sistema de arquivos. As mesmas permissões usadas para exibir um relatório podem ser aplicadas ao recurso. Em contrapartida, se a imagem for armazenada em disco, é necessário certificar-se de que a conta de usuário Anônimo ou a conta de execução autônoma tem permissão para acessar o arquivo.  
  
 Para usar um recurso de imagem em um relatório, adicione o arquivo de imagem ao projeto e publique-o juntamente com o relatório. Quando a imagem for publicada, será possível atualizar a referência da imagem no relatório de modo que aponte para o recurso no servidor de relatório. Sendo assim, somente publique novamente o relatório para salvar as alterações. Você poderá atualizar subsequentemente a imagem, independentemente do relatório, republicando o recurso. O relatório usa a versão mais atual da imagem disponível no servidor de relatórios.  
  
 Para obter mais informações, confira [Atualizar um Recurso (portal da Web)](../../reporting-services/report-server/update-a-resource-report-manager.md).  
  
##  <a name="my-reports"></a><a name="bkmk_MyReports"></a> Meus Relatórios  
 A pasta Meus Relatórios é um workspace pessoal para cada usuário que efetua logon em um servidor de relatório com uma conta de domínio válida. Essa pasta de finalidade especial armazena relatórios de trabalhos em andamento, relatórios que não serão distribuídos amplamente ou relatórios que foram modificados para atender a uma necessidade. Não é possível restringir o número ou o tamanho dos itens armazenados em uma pasta Meus Relatórios, nem configurá-la para ser compartilhada entre usuários.  
  
 Tecnicamente, a pasta Meus Relatórios mapeia o nome de uma pasta virtual que cada usuário vê (Meus Relatórios) para uma pasta Pastas dos Usuários mestre e uma subpasta exclusiva baseada no nome de usuário. Quando um usuário acessa sua pasta Meus Relatórios, na realidade, ele é redirecionado para sua subpasta em Pastas dos Usuários. Cada subpasta armazena os relatórios e itens que um usuário adiciona à sua pasta Meus Relatórios. No portal da Web, você não verá Meus Relatórios no nível raiz. Será necessário aprofundar na pasta Usuários.  
  
 A pasta Pastas dos Usuários é criada quando o servidor de relatório é instalado. As subpastas subsequentes baseadas no usuário são criadas quando um usuário abre Meus Relatórios pela primeira vez (por exemplo, ao clicar em Meus Relatórios no portal da Web). Cada nome de pasta está no seguinte formato:  
  
```  
/Users Folders/<username>/My Reports  
```  
  
 As pastas são alocadas somente para usuários com contas de sistema válidas. Se um nome de usuário contiver caracteres especiais, as pastas serão criadas com caracteres de escape equivalentes. Os caracteres de escape equivalentes são listados na tabela a seguir.  
  
|Caractere|Valor de escape|Exemplo|  
|---------------|------------------|-------------|  
|(espaço)|[ ]|*Nome Sobrenome* se transforma em *Nome[ ]Sobrenome*|  
|\ (barra invertida)|Substituída por um caractere de espaço único|*Nomededomínio\Nomedeusuário* se transforma em *Nomededomínio Nomedeusuário*|  
|@ (símbolo de arroba)|[arroba]|*nomedeusuário*@hotmail.com se transforma em *nomedeusuário*[arroba]hotmail.com|  
|& (e comercial)|[E comercial]|*nomedeusuário*@*empresa*&*empresa.com* se transforma em *nomedeusuário*[arroba]*empresa*[E comercial]*empresa.com*|  
|$ (cifrão)|[cifrão]|*Nome d* $*Usuário* se transforma em *Nome de*[ ][cifrão]*Usuário*|  
  
 O recurso Meus Relatórios é opcional. Ao instalar um servidor de relatório, Meus Relatórios é desabilitado por padrão. Para obter mais informações sobre como habilitar esse recurso, consulte [Habilitar e desabilitar Meus Relatórios](../../reporting-services/report-server/enable-and-disable-my-reports.md). Para obter mais informações, consulte [Proteger Meus Relatórios](../../reporting-services/security/secure-my-reports.md).  
  
## <a name="tasks"></a>Tarefas  
 [Carregar arquivos em uma pasta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
 [Criar, excluir ou modificar uma pasta (portal da Web)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)  
 [Atualizar um recurso (portal da Web)](../../reporting-services/report-server/update-a-resource-report-manager.md)  
 [Carregar arquivos em uma pasta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
## <a name="see-also"></a>Confira também  
 [Ferramentas do Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
 [Funções e permissões &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)   
 [Relatórios do Reporting Services &#40;SSRS&#41;](../../reporting-services/reports/reporting-services-reports-ssrs.md)  
  