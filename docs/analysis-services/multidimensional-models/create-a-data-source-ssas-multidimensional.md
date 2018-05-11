---
title: Criar uma fonte de dados (SSAS Multidimensional) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d381bfd9c2421664a4910c56f45d9c73c0c9687c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="create-a-data-source-ssas-multidimensional"></a>Criar uma fonte de dados (SSAS multidimensional)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Em um modelo multidimensional do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , um objeto de fonte de dados representa uma conexão para a fonte de dados com base na qual você está processando (ou importando) os dados. Um modelo multidimensional deve conter pelo menos um objeto de fonte de dados, mas você pode adicionar mais para combinar dados de vários data warehouses. Use as instruções neste tópico para criar um objeto de fonte de dados para seu modelo. Para obter mais informações sobre como definir propriedades nesse objeto, consulte [Definir propriedades da fonte de dados &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md).  
  
 Este tópico inclui as seguintes seções:  
  
 [Escolher um provedor de dados](#bkmk_provider)  
  
 [Definir opções de credenciais e representação](#bkmk_impersonation)  
  
 [Exibir ou editar propriedades de conexão](#bkmk_ConnectionString)  
  
 [Criar uma fonte de dados usando o Assistente para Fontes de Dados](#bkmk_steps)  
  
 [Criar uma fonte de dados usando uma conexão existente](#bkmk_connection)  
  
 [Adicionar várias fontes de dados a um modelo](#bkmk_multipleDS)  
  
##  <a name="bkmk_provider"></a> Escolher um provedor de dados  
 Você pode conectar usando um [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework gerenciado ou provedor do OLE DB nativo. O provedor de dados indicado para fontes de dados do SQL Server é o SQL Server Native Client porque normalmente oferece desempenho melhor.  
  
 Para a Oracle e outras fontes de dados de terceiros, verifique se as de terceiros fornecem um provedor do OLE DB nativo e tente isso primeiro. Se você encontrar erros, tente um dos outros provedores de .NET ou provedores do OLE DB nativos listados no Gerenciador de Conexões. Verifique se todos os provedores de dados que você usa estão instalados em todos os computadores usados para desenvolver e executar a solução do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
##  <a name="bkmk_impersonation"></a> Definir opções de credenciais e representação  
 Uma conexão da fonte de dados pode muitas vezes usar a autenticação do Windows ou serviço de autenticação fornecido pelo sistema de gerenciamento de banco de dados, como a autenticação do SQL Server ao conectar-se a bancos de dados do SQL Azure. A conta que você especificar deve ter um logon no servidor de banco de dados remoto e permissões de leitura no banco de dados externo.  
  
### <a name="windows-authentication"></a>Autenticação do Windows  
 As conexões que usam autenticação do Windows são especificadas na guia **Informações sobre Representação** do Designer de Fonte de Dados. Use esta guia para escolher a opção de representação que especifica a conta sob a qual o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é executado ao conectar-se à fonte de dados externa. Nem todas as opções podem ser usadas em todos os cenários. Para obter mais informações sobre essas opções e quando usá-las, consulte [Definir opções de representação &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
### <a name="database-authentication"></a>Autenticação de banco de dados  
 Como uma alternativa para autenticação do Windows, você pode especificar uma conexão que usa um serviço de autenticação fornecido pelo sistema de gerenciamento de banco de dados. Em alguns casos, usar a autenticação de banco de dados é obrigatório. Cenários que pedem o uso da autenticação de banco de dados incluem o uso da autenticação do SQL Server para conectar-se a um Banco de dados SQL do Windows Azure ou o acesso a uma fonte de dados relacional que é executada em um sistema operacional diferente ou em um domínio não confiável.  
  
 Para uma fonte de dados que usa autenticação de banco de dados, o nome de usuário e a senha de um logon de banco de dados são especificados na cadeia de conexão. As credenciais são adicionadas à cadeia de conexão quando você insere um nome de usuário e senha no Gerenciador de Conexões ao configurar a conexão da fonte de dados em seu modelo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Lembre-se de especificar uma identidade de usuário que tenha permissões de leitura aos dados.  
  
 Ao recuperar dados, a biblioteca de cliente que faz a conexão formula uma solicitação de conexão que inclui as credenciais na cadeia de conexão. As opções de credencial de autenticação do Windows na guia de Informações sobre Representação não são usadas na conexão, mas podem ser usadas para outras operações, como acessar recursos no computador local. Para obter mais informações, consulte [Definir opções de representação &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
 Depois que você salva o objeto da fonte de dados em seu modelo, a cadeia de conexão e a senha são criptografadas.  Para fins de segurança, são removidos todos os rastreamentos visíveis da senha da cadeia de conexão quando você subsequentemente os exibe em ferramentas, script ou código.  
  
> [!NOTE]  
>  Por padrão, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] não salva senhas com a cadeia de conexão. Se a senha não for salva, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pedirá que você a digite sempre que necessário. Se você escolheu salvar a senha, a senha será armazenada em formato criptografado na cadeia de conexão de dados. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] criptografa informações de senha para fontes de dados usando a chave de criptografia do banco de dados que contém a fonte de dados. Com as informações da conexão criptografadas, use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para alterar a conta de serviço ou a senha do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou não será possível recuperar as informações criptografadas. Para obter mais informações, consulte [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).  
  
### <a name="defining-impersonation-information-for-data-mining-objects"></a>Definindo informações de representação para objetos de mineração de dados  
 As consultas de mineração de dados podem ser executadas no contexto da conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , mas também podem ser executadas no contexto do usuário que está enviando a consulta ou no contexto de um usuário especificado. O contexto no qual uma consulta é executada pode afetar seus resultados. Para operações do tipo **OPENQUERY** de mineração de dados, convém executar a consulta de mineração de dados no contexto do usuário atual ou no contexto de um usuário especificado (independentemente do usuário que está executando a consulta) e não no contexto da conta de serviço. Isso possibilita a execução da consulta com credenciais de segurança limitadas. Para que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] represente o usuário atual ou um usuário especificado, selecione a opção **Usar um nome de usuário e uma senha específicos** ou **Usar as credenciais do usuário atual** .  
  
##  <a name="bkmk_steps"></a> Criar uma fonte de dados usando o Assistente para Fontes de Dados  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou conecte-se ao banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no qual você deseja definir a fonte de dados.  
  
2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Fontes de Dados** e, em seguida, clique em **Nova Fonte de Dados** para iniciar o **Assistente da Fonte de Dados**.  
  
3.  Na página **Selecione como definir a conexão** , escolha **Criar uma fonte de dados com base em uma conexão já existente ou em uma nova conexão** e clique em **Novo** para abrir o **Gerenciador de Conexões**.  
  
     Novas conexões são criadas no Gerenciador de Conexões. No Gerenciador de Conexões, você seleciona um provedor e especifica as propriedades da cadeia de conexão usada pelo provedor para se conectar com os dados subjacentes. As informações necessárias variam de acordo com o provedor selecionado, mas, geralmente, incluem uma instância de servidor ou serviço, informações de logon na instância de servidor ou serviço, um banco de dados ou nome de arquivo e outras configurações específicas do provedor. Para o restante deste procedimento, presumiremos uma conexão de banco de dados do SQL Server.  
  
4.  Selecione o provedor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework ou de OLE DB nativo a ser usado para a conexão.  
  
     O provedor padrão de uma nova conexão é o provedor OLE DB nativo\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Ele é usado para estabelecer a conexão com uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando OLE DB. Para conexões com um banco de dados relacional do SQL Server, com frequência, é mais rápido usar o Native OLE DB\SQL Server Native Client 11.0 do que usar provedores alternativos.  
  
     Você pode escolher um provedor diferente para acessar outras fontes de dados. Para obter uma lista dos provedores e bancos de dados relacionais com suporte pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Fontes de dados com suporte &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
5.  Insira as informações solicitadas pelo provedor selecionado para se conectar à fonte de dados subjacente. Se o provedor **OLE DB Nativo\SQL Server Native Client** estiver selecionado, insira as seguintes informações:  
  
    1.  **Nome do Servidor** é o nome de rede da instância do Mecanismo de Banco de Dados. É possível especificá-lo como o endereço IP, o nome NETBIOS do computador ou um nome de domínio totalmente qualificado. Se o servidor estiver instalado como uma instância nomeada, você deve incluir o nome da instância (por exemplo, \<computername >\\< instancename\>).  
  
    2.  **Fazer logon no servidor** especifica como a conexão será autenticada. **Usar Autenticação do Windows** usa a autenticação do Windows. **Usar Autenticação do SQL Server** especifica um logon de usuário de banco de dados para um banco de dados SQL do Microsoft Azure ou uma instância do SQL Server que dá suporte à autenticação no modo misto.  
  
        > [!IMPORTANT]  
        >  O Gerenciador de Conexões inclui uma caixa de seleção **Salvar minha senha** para conexões que usam a autenticação do SQL Server. Embora a caixa de seleção sempre esteja visível, nem sempre ela é usada.  
        >   
        >  As condições sob as quais o Analysis Services não usa essa caixa de seleção incluem atualização ou processamento de dados relacionais do SQL Server que são utilizados no banco de dados ativo do Analysis Services. Quer você marque ou desmarque a opção **Salvar minha senha**, o Analysis Services sempre criptografará e salvará a senha. A senha é criptografada e armazena em arquivos .abf e de dados. Esse comportamento existe porque o Analysis Services não oferece suporte ao armazenamento de senha com base na sessão no servidor.  
        >   
        >  Esse comportamento se aplica apenas aos bancos de dados que a) são persistentes em uma instância do servidor Analysis Services e b) usam a autenticação do SQL Server para atualizar ou processar dados relacionais. Isso não se aplica às conexões de fontes de dados que você configura no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , que são utilizadas apenas durante a sessão. Embora não haja nenhuma forma de remover uma senha que já esteja armazenada, você pode usar credenciais diferentes ou a autenticação do Windows para substituir as informações de usuário atualmente armazenadas com o banco de dados.  
  
    3.  **Selecionar ou digitar um nome de banco de dados** ou **Anexar um arquivo de banco de dados** são usados para especificar o banco de dados.  
  
    4.  À esquerda da caixa de diálogo, clique em **Todos** para exibir as configurações adicionais dessa conexão, incluindo todas as configurações padrão desse provedor.  
  
    5.  Altere as configurações conforme apropriado para seu ambiente e, em seguida, clique em **OK**.  
  
         A nova conexão aparece no painel **Conexões de Dados** da página **Selecione como definir a conexão** do Assistente para Fontes de Dados.  
  
6.  Clique em **Avançar**.  
  
7.  Em **Informações sobre Representação**, especifique as credenciais do Windows ou a identidade de usuário que o Analysis Services usará para se conectar à fonte de dados externa. Se você estiver usando autenticação de banco de dados, estas configurações serão ignoradas para fins de conexão.  
  
     As diretrizes para escolher uma opção de representação variam, dependendo de como você está usando a fonte de dados. Para tarefas de processamento, o serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve ser executado no contexto de segurança de sua conta de serviço ou da conta de usuário especificada ao se conectar com a fonte de dados.  
  
    -   **Usar nome de usuário e senha específicos do Windows** para especificar um conjunto exclusivo de credenciais de privilégios mínimos.  
  
    -   **Usar a conta de serviço** para processar os dados usando a identidade de serviço.  
  
     A conta que você especificar deve ter permissões de Leitura na fonte de dados.  
  
8.  Clique em **Avançar**.  Em **Concluindo o Assistente**, insira um nome da fonte de dados ou use o nome padrão. O nome padrão é o nome do banco de dados especificado na conexão. O painel **Visualizar** exibe a cadeia de conexão dessa nova fonte de dados.  
  
9. Clique em **Concluir**.  A nova fonte de dados aparece na pasta **Fontes de Dados** do Gerenciador de Soluções.  
  
##  <a name="bkmk_connection"></a> Criar uma fonte de dados usando uma conexão existente  
 Quando você trabalha em um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , a fonte de dados pode se basear em uma fonte de dados existente na solução ou em um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O Assistente de Fonte de Dados fornece várias opções para criar o objeto de fonte de dados, inclusive usar uma conexão existente no mesmo projeto.  
  
-   Ao criar uma fonte de dados com base em uma fonte de dados existente, você poderá definir uma fonte de dados sincronizada com a fonte de dados existente. Quando o projeto que contém essa nova fonte de dados for criado, serão utilizadas as configurações da fonte de dados subjacente.  
  
-   Ao criar uma fonte de dados com base em projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você poderá fazer referência a outro projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da solução no projeto atual. A nova fonte de dados utiliza o provedor MSOLAP com as propriedades **Data Source** e **Initial Catalog** obtidas das propriedades **TargetServer** e **TargetDatabase** do projeto selecionado. Esse recurso será útil para soluções quando você estiver usando vários projetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para gerenciar partições remotas, pois os bancos de dados de origem e destino do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] requerem fontes de dados recíprocas para suportar armazenamento e processamento em partições remotas.  
  
 Ao fazer referência a um objeto de fonte de dados, você pode editar esse objeto apenas no objeto ou projeto de referência. Não é possível editar a informações de conexão no objeto de fonte de dados que contém a referência. As alterações feitas nas informações de conexão no objeto de referência ou projeto aparecerão na nova fonte de dados quando ela for criada. As informações da cadeia de conexão que aparecem no arquivo da fonte de dados (.ds) do projeto serão sincronizadas quando você criar o projeto ou eliminar a referência no Design de Fonte de Dados.  
  
##  <a name="bkmk_ConnectionString"></a> Exibir ou editar propriedades de conexão  
 A cadeia de conexão é formulada com base nas propriedades selecionadas no Designer da Fonte de Dados ou no Novo Assistente para Fonte de dados. Você pode exibir a cadeia de conexão e outras propriedades no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 **Para editar a cadeia de conexão.**  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique duas vezes no objeto da fonte de dados no Gerenciador de Soluções.  
  
2.  Clique em **Editar**e em **Todos** no painel de navegação esquerdo.  
  
3.  A grade de propriedade aparece, mostrando as propriedades disponíveis do provedor de dados que você está usando. Para obter mais informações sobre essas propriedades, consulte a documentação de produto do provedor.  Para o SQL Server Native Client, consulte [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Se você tiver vários objetos de fonte de dados na solução e preferir manter a cadeia de conexão em um local, poderá configurar a fonte de dados atual para referenciar o outro objeto de fonte de dados.  
  
 Uma *referência de fonte de dados* é uma associação a outro projeto ou fonte de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na mesma solução. Referências são um meio de sincronizar fontes de dados entre objetos de uma solução. As informações da cadeia de conexão são sincronizadas sempre que você criar o projeto. Para alterar a cadeia de conexão para uma fonte de dados que faz referência a outro objeto, altere a cadeia de conexão do objeto de referência.  
  
 Você pode remover a referência desmarcando a caixa de seleção. Isso encerra a sincronização entre os objetos e permite a alteração da cadeia de conexão da fonte de dados.  
  
##  <a name="bkmk_multipleDS"></a> Adicionar várias fontes de dados a um modelo  
 Você pode criar mais de um objeto de fonte de dados para dar suporte a conexões com fontes de dados adicionais. Cada fonte de dados deve ter colunas que podem ser usadas para criar relações.  
  
> [!NOTE]  
>  Se houver várias fontes de dados definidas e se os dados forem consultados por meio de várias fontes em uma mesma consulta, como no caso de uma dimensão em floco de neve, defina uma fonte de dados que dê suporte a consultas remotas usando **OpenRowset**. Normalmente, será uma fonte de dados do Microsoft SQL Server.  
  
 Os requisitos para usar várias fontes de dados incluem o seguinte:  
  
-   Designar uma fonte de dados como a fonte de dados primária. A fonte de dados primária é a usada para criar uma exibição da fonte de dados.  
  
-   Uma fonte de dados primária deve dar suporte à função **OpenRowset** .  Para obter mais informações sobre esta função no SQL Server, consulte <xref:Microsoft.SqlServer.TransactSql.ScriptDom.TSqlTokenType.OpenRowSet>.  
  
 Use a abordagem a seguir para combinar dados de várias fontes de dados:  
  
1.  Crie as fontes de dados em seu modelo.  
  
2.  Crie uma exibição da fonte de dados, usando um banco de dados relacional do SQL Server como a fonte de dados. Esta é sua fonte de dados primária.  
  
3.  No Designer de Exibição da Fonte de Dados, usando a exibição da fonte de dados que você acabou de criar, clique com o botão direito do mouse em qualquer lugar na área de trabalho e selecione **Adicionar/Remover Tabelas**.  
  
4.  Escolha a segunda fonte de dados e selecione as tabelas que você deseja adicionar.  
  
5.  Localize e selecione a tabela que você adicionou. Clique com o botão direito do mouse na tabela e selecione **Nova Relação**. Escolha as colunas de origem e destino que contêm dados de correspondência.  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados com suporte &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [Exibições da fonte de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
