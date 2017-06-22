---
title: Criar, modificar e excluir fontes de dados compartilhadas (SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
caps.latest.revision: 53
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3d4025539369dcc955e8675a92def39e356cb86d
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>Criar, modificar e excluir fontes de dados compartilhadas (SSRS)
  Uma fonte de dados compartilhada é um conjunto de propriedades de conexão de fonte de dados que pode ser referenciada por vários relatórios, modelos e assinaturas controladas por dados que são executados em um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  As fontes de dados compartilhadas fornecem um modo fácil de gerenciar as propriedades da fonte de dados que geralmente são alteradas com o passar do tempo. Se a conta de usuário ou senha for alterada ou se você mover o banco de dados para outro servidor, as informações de conexão poderão ser atualizadas em um único lugar.  
  
 O ícone seguinte indica uma fonte de dados compartilhada na hierarquia da pasta do Gerenciador de Relatórios:  
  
 ![Shared data source icon](../../reporting-services/report-data/media/hlp-16datasource.png "Shared data source icon")  
ícone de fonte de dados compartilhada  
  
 As fontes de dados compartilhadas são opcionais para relatórios e assinaturas controladas por dados, mas são obrigatórias para modelos de relatórios. Se você planeja usar os modelos de relatório para relatórios ad hoc, deve criar e manter um item fonte de dados compartilhada para fornecer informações de conexão ao modelo.  
  
 Uma fonte de dados compartilhada é composta pelas seguintes partes:  
  
|Parte|Description|  
|----------|-----------------|  
|Nome|Um nome que identifica o item dentro da hierarquia de pastas do servidor de relatórios.|  
|Description|Uma descrição que aparece com o item no Gerenciador de Relatórios quando você exibe os conteúdos da pasta.|  
|Tipo de conexão|A extensão de processamento de dados usada com a fonte de dados. Você só poderá usar extensões de processamento de dados que estiverem implantadas no servidor de relatórios. Para obter mais informações sobre as extensões de processamento de dados incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).|  
|Cadeia de conexão|A cadeia de conexão para o banco de dados. Para obter mais informações e exibir exemplos de cadeias de conexão para fontes de dados usadas com frequência, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).|  
|Tipo de credencial|Especifica como as credenciais são obtidas para a conexão e se elas serão usadas depois que a conexão for estabelecida. Para obter mais informações, consulte [Specify Credential and Connection Information for Report Data Sources](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).|  
  
 Uma fonte de dados compartilhada não contém informações de consulta usadas para a recuperação de dados. A consulta sempre é mantida dentro de uma definição do relatório.  
  
## <a name="creating-and-modifying-shared-data-sources"></a>Criando e modificando fontes de dados compartilhadas  
 Para criar uma fonte de dados compartilhada ou modificar suas propriedades, é preciso ter permissões para **Gerenciar fontes de dados** no servidor de relatório. Se o servidor de relatórios for executado em modo nativo, você poderá usar o Gerenciador de Relatórios para criar e configurar a fonte de dados compartilhada. Se o servidor de relatórios for executado no modo integrado do SharePoint, use as páginas de aplicativo em um site do SharePoint. Para qualquer servidor de relatórios independentemente de seu modo, você pode criar uma fonte de dados compartilhada no Designer de Relatórios e publicá-la em um servidor de destino.  
  
 Depois de criar uma fonte de dados compartilhada no servidor de relatórios, você poderá criar atribuições de função para controlar o acesso a ela, movê-la para outro local, renomeá-la ou torná-la offline para evitar o processamento de relatórios durante as operações de manutenção na fonte de dados externa. Se renomear ou mover um item fonte de dados compartilhada para outro local na hierarquia de pastas do servidor de relatórios, as informações de caminho em todos os relatórios ou assinaturas que fazem referência à fonte de dados compartilhada serão atualizadas. Ao colocar a fonte de dados no estado offline, todos os relatórios, modelos e assinaturas não serão executados enquanto a fonte de dados não for reativada.  
  
 Para obter mais informações sobre como controlar o acesso às fontes de dados compartilhadas na hierarquia de pastas do servidor de relatório, consulte [Proteger itens de fontes de dados compartilhadas](../../reporting-services/security/secure-shared-data-source-items.md).  
  
 **Para criar uma fonte de dados compartilhada no Designer de Relatórios**  
  
1.  Na barra de ferramentas do painel Dados do Relatório, clique em **Nova** e em **Fonte de Dados**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
    > [!NOTE]  
    >  Se o painel Dados do Relatório não estiver visível, clique em **Dados do Relatório** no menu **Exibir** .  
  
2.  Na caixa de texto **Nome** , digite um nome para a fonte de dados ou aceite o padrão. O nome da fonte de dados é usado internamente no relatório. Para fins de esclarecimento, recomendamos que o nome da fonte de dados contenha o nome do banco de dados especificado na cadeia de conexão.  
  
3.  Verifique se a opção **Usar referência da fonte de dados compartilhada** está selecionada e escolha uma das opções a seguir.  
  
    1.  Clique em **Nova**. Na caixa de diálogo de propriedades **Fonte de Dados Compartilhada** , siga as etapas 2 e 3 para criar uma nova fonte de dados.  
  
    2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
         A nova fonte de dados compartilhada é exibida na pasta Fontes de Dados Compartilhada no Gerenciador de Soluções.  
  
4.  Clique em Credenciais.  
  
     Especifique as credenciais que serão usadas para essa fonte de dados. O proprietário da fonte de dados escolhe o tipo de credenciais com suporte.  
  
 **Para criar uma fonte de dados compartilhada no Gerenciador de Relatórios**  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** .  
  
3.  Clique em **Nova Fonte de Dados**. A página **Nova Fonte de Dados** será aberta.  
  
4.  Digite um nome para o item. Um nome deve conter pelo menos um caractere e deve começar com uma letra. Ele também pode incluir certos símbolos, mas não espaços nem os caracteres ; ? : @ & = + , $ / * < > | " /.  
  
5.  Como opção, digite uma descrição para oferecer aos usuários informações sobre a conexão. Essa descrição será exibida na página **Conteúdo** no Gerenciador de Relatórios.  
  
6.  Na lista **Tipo de fonte de dados** , especifique a extensão de processamento de dados usada para processar dados da fonte de dados.  
  
7.  Em **Cadeia de conexão**, especifique a cadeia de conexão usada pelo servidor de relatório para se conectar à fonte de dados. Recomendamos que você não especifique credenciais na cadeia de conexão.  
  
     O exemplo a seguir ilustra uma cadeia de conexão usada para conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] local:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  Em **Conectar usando**, especifique como são obtidas as credenciais na execução do relatório:  
  
    -   Se desejar solicitar ao usuário o nome de logon e a senha, clique em **Credenciais fornecidas pelo usuário que está executando o relatório**. Para usar as credenciais inseridas pelo usuário como credenciais do Windows, clique em **Usar as credenciais do Windows ao conectar-se à fonte de dados**. Se o nome de usuário e a senha forem credenciais de banco de dados, não selecione esta opção.  
  
    -   Caso pretenda usar a fonte de dados como uma fonte de dados compartilhada com credenciais salvas que são gerenciadas pelo proprietário da fonte de dados, ou para relatórios que dão suporte a assinaturas ou outras operações agendadas (como a geração automatizada de histórico de relatório), clique em **Credenciais armazenadas com segurança no servidor de relatório**. Se o servidor do banco de dados oferecer suporte a representação ou delegação, é possível selecionar **Representar o usuário autenticado depois que uma conexão é estabelecida com a fonte de dados**.  
  
    -   Se desejar que o servidor de relatório passe as credenciais do usuário que está acessando o relatório para o servidor que está hospedando a fonte de dados externa, clique em **Segurança Integrada do Windows**. Nesse caso, não é solicitado que o usuário digite um nome de usuário ou senha.  
  
    -   Se a fonte de dados não usar credenciais (se a fonte de dados for um arquivo XML acessado pelo sistema de arquivos, por exemplo), clique em **Não são necessárias credenciais**. Você deve especificar esse tipo de credencial somente se ele for válido para a fonte de dados. Se você selecionar essa opção para uma fonte de dados que requer autenticação, a conexão falhará. Se essa opção for selecionada, certifique-se de configurar a conta de execução autônoma que permite que o servidor de relatório se conecte a outros computadores para recuperar dados ou arquivos quando as credenciais do usuário não estiverem disponíveis.  
  
         Para obter mais informações sobre como configurar as credenciais, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). Para obter mais informações sobre a conta de execução autônoma, consulte [Configurar a conta de execução autônoma &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
9. Clique no botão **Testar Conexão** para validar a configuração da fonte de dados.  
  
    > [!NOTE]  
    >  O botão Testar Conexão não tem suporte para o tipo de fonte de dados XML.  
  
10. Clique em **OK**.  
  
 **Para modificar uma fonte de dados compartilhada no Gerenciador de Relatórios**  
  
1.  No Gerenciador de Relatórios, navegue até a página Conteúdo.  
  
2.  Navegue até o item de fonte de dados compartilhada, focalize o item, clique na lista suspensa e, no menu de contexto, clique em **Gerenciar**. A página **Propriedades** é exibida.  
  
3.  Modifique a fonte de dados e clique em **Aplicar**.  
  
## <a name="deleting-shared-data-sources"></a>excluindo fontes de dados compartilhadas  
 Você pode excluir uma fonte de dados compartilhada da mesma forma que exclui qualquer item do servidor de relatórios.  
  
 **Para excluir uma fonte de dados compartilhada**  
  
1.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** e execute uma das seguintes opções:  
  
    -   Navegue até o item da fonte de dados compartilhada.  
  
         Clique no item para abri-lo. A página Propriedades Gerais será aberta.  
  
         Clique em **Excluir**e em **OK**.  
  
    -   Na página **Conteúdo** , navegue até a pasta que contém a fonte de dados que você quer excluir.  
  
         Focalize o item, clique na lista suspensa e, no menu de contexto, clique em **Excluir**.  
  
         [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 A exclusão de uma fonte de dados compartilhada desabilitará todos os relatórios, modelos ou assinaturas controladas por dados que a usam. Sem as informações de conexão da fonte de dados, os itens não poderão ser executados. Para habilitar esses itens, abra cada um deles e siga as etapas a seguir:  
  
-   Para os relatórios e as assinaturas controlados por dados que fazem referência à fonte de dados compartilhada, você pode especificar as informações de conexão da fonte de dados nas propriedades do relatório ou da assinatura, ou também pode selecionar uma nova fonte de dados compartilhada que contenha os valores desejados.  
  
-   Para modelos e relatórios do Construtor de Relatórios que usam esse modelo, é preciso especificar uma nova fonte de dados compartilhada. Os modelos podem obter as informações de conexão da fonte de dados somente pelas fontes de dados compartilhadas.  
  
 Não existe a operação Desfazer para a exclusão de uma fonte de dados compartilhada. Entretanto, em caso de exclusão acidental, você poderá criar uma nova fonte de dados compartilhada usando os mesmos valores de propriedades daquela que foi excluída. Também será preciso abrir cada relatório, modelo e assinatura controlada por dados para reassociar a fonte de dados compartilhada ao item que a usa, mas como as propriedades serão as mesmas, os relatórios, os modelos e as assinaturas continuarão funcionando normalmente.  
  
## <a name="importing-shared-data-sources"></a>Importando fontes de dados compartilhadas  
 **Para importar uma origem de dados existente no Designer de Relatórios**  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Fontes de Dados Compartilhadas** no projeto do servidor de relatório e clique em **Adicionar Item Existente**. A caixa de diálogo **Adicionar Item Existente** será aberta.  
  
2.  Navegue até um arquivo de fonte de dados Compartilhada de Definição de Relatório (rds) e clique em **Abrir**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="shared-data-sources-in-sharepoint"></a>Fontes de dados compartilhadas no SharePoint  
 Ao executar um relatório a partir de uma biblioteca do SharePoint, as informações de conexão podem ser definidas no relatório ou em um arquivo externo vinculado ao relatório. Se as informações de conexão estiverem inseridas no relatório, ele será denominado uma fonte de dados personalizada. Se as informações de conexão estiverem definidas em um arquivo externo, ele será denominado uma fonte de dados compartilhados. O arquivo externo pode ser um arquivo de fonte de dados do servidor de relatório (.rsds) ou um arquivo de conexão de dados do Office (.odc).  
  
 Um arquivo .rsds é semelhante a um arquivo .rds, mas tem um esquema diferente. Para criar um arquivo .rsds, você pode publicar um arquivo .rds do Designer de Relatórios ou do Designer de Modelo em uma biblioteca do SharePoint (um novo arquivo .rsds é criado a partir do arquivo .rds original). Se preferir, você pode criar um novo arquivo em uma biblioteca em um site do SharePoint.  
  
 Após criar ou publicar uma fonte de dados compartilhada, você pode editar propriedades de conexão ou excluir o arquivo caso não seja mais utilizado. Antes de excluir uma fonte de dados compartilhada, descubra se ela é usada por relatórios e modelos de relatório. Para tal exiba itens dependentes que fazem referência à fonte de dados compartilhada.  
  
 Embora a lista de itens dependentes informe se existe referência a uma fonte de dados compartilhada, ela não informa se o item está sendo usado ativamente. Para descobrir se uma fonte de dados compartilhados ou um modelo está sendo usado ativamente, você pode revisar os arquivos de log no servidor de relatórios. Se você não tiver acesso aos arquivos de log ou se os arquivos não contiverem as informações desejadas, você poderá mover o relatório para uma pasta inacessível enquanto descobre seu status real.  
  
 **Para criar um arquivo .rsds (SharePoint 2010)**  
  
1.  Clique na guia **Documentos** na faixa de opções da biblioteca.  
  
2.  No menu **Novo Documento** , clique em **Fonte de Dados de Relatório**  
  
    > [!NOTE]  
    >  Caso você não veja o item **Fonte de Dados de Relatório** no menu, isso significa que o tipo de conteúdo da fonte de dados de relatório não foi habilitado. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  Em **Nome**, insira um nome descritivo para o arquivo .rsds.  
  
4.  Em **Tipo de Fonte de Dados**, selecione o tipo de fonte de dados na lista. Para obter mais informações, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
5.  Em **Cadeia de Conexão**, especifique um ponteiro para a fonte de dados e outras configurações necessárias para estabelecer uma conexão com a fonte de dados externa. O tipo de fonte de dados usado determina a sintaxe da cadeia de caracteres de conexão. Para obter mais informações e exemplos, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
6.  Em **Credenciais**, especifique como o servidor de relatório obtém credenciais para acessar a fonte de dados externa. Credenciais podem ser armazenadas, solicitadas, integradas ou configuradas para processamento autônomo do relatório.  
  
    -   Selecione **Autenticação do Windows (integrada)** se desejar acessar os dados usando as credenciais do usuário que abriu o relatório. Não selecione essa opção se o site ou farm do SharePoint utilizar autenticação de formulários ou se conectar com o servidor de relatório usando uma conta confiável. Não selecione essa opção se desejar agendar a assinatura ou o processamento de dados para esse relatório. Essa opção funciona melhor quando a autenticação Kerberos está habilitada para seu domínio ou quando a fonte de dados está no mesmo computador que o servidor de relatórios. Se a autenticação Kerberos não estiver habilitada, as credenciais do Windows poderão ser passadas apenas para outro computador. Isso significa que, se a fonte de dados externa estiver em outro computador, exigindo uma conexão adicional, você receberá uma mensagem de erro em vez dos dados esperados.  
  
    -   Selecione **Prompt para credenciais** se quiser que o usuário insira suas credenciais sempre que executar o relatório. Não selecione essa opção se desejar agendar a assinatura ou o processamento de dados para esse relatório.  
  
    -   Selecione **Credenciais armazenadas** se quiser acessar os dados usando um único conjunto de credenciais. As credenciais são criptografadas antes de serem armazenadas. Você pode selecionar opções que determinam como as credenciais armazenadas são autenticadas. Selecione Usar como credenciais do Windows se as credenciais armazenadas pertencerem a uma conta de usuário do Windows. Selecione **Definir o contexto de execução para esta conta** se desejar definir o contexto de execução no servidor de banco de dados. No caso de bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essa opção define a função SETUSER. Para obter mais informações, consulte [SETUSER &#40;Transact-SQL&#41;](../../t-sql/statements/setuser-transact-sql.md).  
  
    -   Selecione **Não são necessárias credenciais** se quiser especificar credenciais na cadeia de conexão ou se quiser executar o relatório usando uma conta de privilégios mínimos configurada no servidor de relatório. Se essa conta não estiver configurada no servidor de relatório, os usuários serão solicitados a fornecer suas credenciais, e as operações agendadas que você definir para o relatório não serão executadas.  
  
7.  Selecione **Habilitar esta fonte de dados** se desejar que a fonte de dados esteja ativa. Se a fonte de dados estiver configurada mas não ativa, os usuários verão uma mensagem de erro quando tentarem usar um relatório com base na fonte de dados.  
  
8.  Clique no botão **Testar Conexão** para validar a configuração da fonte de dados.  
  
    > [!NOTE]  
    >  O botão Testar Conexão não tem suporte para o tipo de fonte de dados XML.  
  
9. Clique em **OK** para salvar e criar a fonte de dados compartilhada.  
  
 **Para excluir um arquivo da fonte de dados compartilhada (.rsds)**  
  
1.  Abra a biblioteca que contém o arquivo .rsds.  
  
2.  Aponte para a fonte de dados compartilhada.  
  
3.  Clique para exibir uma seta para baixo e clique em **Excluir**.  
  
 Se, por engano, você excluir uma fonte de dados compartilhada que pretendia manter, crie uma nova fonte de dados que contenha as mesmas informações de conexão. Depois de recriar a fonte de dados compartilhada, você deve abrir cada relatório e cada modelo que usava essa fonte de dados e selecionar a fonte de dados compartilhada. O novo item da fonte de dados compartilhada pode ter nome, credenciais ou sintaxe de cadeia de caracteres de conexão diferentes daquele que foi excluído. Desde que a conexão leve à mesma fonte de dados, as propriedades de conexão podem variar em relação aos valores originais.  
  
 Tenha cuidado ao excluir um modelo de relatório. Se você excluir um modelo, não será mais possível abrir e modificar relatórios baseados nesse modelo no Construtor de Relatórios. Se você excluir por engano um modelo usado por relatórios existentes, será preciso gerar novamente o modelo, recriar e salvar os relatórios que usam o modelo e especificar novamente a segurança de todos os itens do modelo que deseje usar. Você não pode simplesmente gerar o modelo de novo e, em seguida, anexá-lo a um relatório existente.  
  
## <a name="dependent-items"></a>Itens Dependentes  
 Para exibir a lista de relatórios e modelos que usam a fonte de dados, abra a página Itens Dependentes da fonte de dados compartilhada. Você pode acessar essa página quando abrir a fonte de dados no Gerenciador de Relatórios ou uma página de aplicativo do SharePoint. Observe que a página Itens Dependente não mostra as assinaturas controladas por dados. Se uma fonte de dados compartilhada for usada por uma assinatura, a assinatura não será exibida na lista de itens dependentes.  
  
 **Para exibir itens dependentes no SharePoint**  
  
1.  Abra a biblioteca que contém o arquivo .rsds.  
  
2.  Aponte para a fonte de dados compartilhada.  
  
3.  Clique para exibir uma seta para baixo e selecione **Exibir Itens Dependentes**.  
  
     No caso de modelos de relatórios, a lista de itens dependentes mostra os relatórios criados no Construtor de Relatórios. No caso de fontes de dados compartilhadas, a lista de itens dependentes pode incluir relatórios e modelos de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)   
 [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Gerenciar fontes de dados de relatório](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](http://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56)   
 [Página Propriedades de Fontes de Dados &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/f37edda0-19e6-489e-b544-8751fa6b6cfb)   
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Configurar propriedades de fonte de dados para um relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  

