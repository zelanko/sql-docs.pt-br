---
title: Configurações de projeto de banco de dados | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.data.tools.DebugProperties
- sql.data.tools.dacsettings.dialog
- sql.data.tools.dbsqlclrlanguagevb
- SQL.DATA.TOOLS.DBADVANCEDBUILDSETTINGSCS
- sql.data.tools.dbadvancedbuildsettingscs
- ql.data.tools.criticalerror.dialog
- sql.data.tools.dbassemblysigningchangekeypassword
- sql.data.tools.advanceddeploymentsystemdefined.dialog
- sql.data.tools.advanceddatabasesettings.dialog
- sql.data.tools.extendedpropertiesvalueeditor.dialog
- sql.data.tools.dbsqlclrlanguagecs
- ql.data.tools.dbassemblysigningpasswordneeded
- sql.data.tools.vbadvancedsettings.dialog
- sql.data.tools.dbsqlclr
- sql.data.tools.SqlCmdVariablesProperties
- sql.data.tools.dbassemblysigning
- sql.data.tools.advanceddeploymentsettings.dialog
- sql.data.tools.advancedpublishsettings.dialog
- sql.data.tools.BuildActionProperties
- sql.data.tools.serverselectionpolicy.dialog
- sql.data.tools.dbadvancedbuildsettingsvb
- sql.data.tools.dbprojectwizard.buildeventcommandline
- sql.data.tools.dbreferencepaths
- sql.data.tools.GeneralProperties
- sql.data.tools.BuildProperties
- sql.data.tools.DeployProperties
- sql.data.tools.csadvancedsettings.dialog
- sql.data.tools.dbassemblyinfo
- sql.data.tools.extendedpropertieseditor.dialog
ms.assetid: 34418730-1aaa-4948-aee2-8f1e62cda85c
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cdf95f469cd5a94514d0e91d13ef7b9125c1531f
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093663"
---
# <a name="database-project-settings"></a>Configurações de projeto de banco de dados
Você usa as configurações de projeto de banco de dados para controlar aspectos do seu banco de dados, depuração e configurações de compilação. Essas configurações caem nas seguintes categorias.  
  
-   [Configurações do Projeto](#bkmk_proj_settings)  
  
-   [Verificação Estendida Transact-SQL](#bkmk_evf)  
  
-   [SQLCLR](#bkmk_sqlclr)  
  
-   [Build SQLCLR e SQLCLR](#bkmk_sqlclr_sqlclrbuild)  
  
-   [Compilação](#bkmk_build)  
  
-   [Variáveis SQLCMD](#bkmk_sqlcmd_variables)  
  
-   [Eventos de Compilação](#bkmk_build_events)  
  
-   [Depurador](#bkmk_debug)  
  
-   [Caminhos de Referência](#bkmk_ref_paths)  
  
-   [Análise de Código](#bkmk_code_analysis)  
  
### <a name="to-configure-properties-for-your-database-project"></a>Para configurar propriedades de seu projeto de banco de dados  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de banco de dados do qual você deseja configurar as propriedades e selecione **Propriedades**.  
  
    Como alternativa, clique duas vezes no nó **Propriedades** do projeto no **Gerenciador de Soluções**.  
  
2.  A folha de propriedades de seu projeto de banco de dados é exibida.  
  
3.  Clique na guia **Configurações do Projeto** . Agora é possível configurar as propriedades gerais de seu projeto de banco de dados. Observe a disponibilidade de várias guias (que representam categorias diferentes) no painel esquerdo.  
  
## <a name="bkmk_proj_settings"></a>Configurações do Projeto  
As configurações da tabela a seguir aplicam-se a todas as configurações deste projeto de banco de dados:  
  
|Campo|Valor padrão|Descrição|  
|---------|-----------------|---------------|  
|Plataforma de Destino|Microsoft SQL Server 2012|Especifica a versão do SQL Server de destino deste projeto de banco de dados.|  
|Habilitar a verificação estendida do Transact\-SQL para objetos comuns.|Não habilitado quando você cria um novo projeto.<br /><br />Habilitado quando você cria um projeto no Pesquisador de Objetos do SQL Server conectado ao SQL Azure, importa um banco de dados do SQL Azure para o projeto ou altera a plataforma de destino do projeto para o SQL Azure.|Quando essa opção está habilitada, são relatados os erros encontrados no projeto que não passaram na verificação do Compilador do SQL Server. Se você alterar a plataforma de destino para o SQL Azure, a verificação estendida será habilitada. A opção não será desmarcada se você alterar a plataforma de destino.<br /><br />Você pode habilitar essa opção para outras versões do SQL Server, mas a validação é limitada aos bancos de dados parcialmente independentes do Microsoft SQL Server 2012 e SQL Azure. Não há suporte para toda a sintaxe Transact\-SQL em todas as versões do SQL Server.<br /><br />Para saber mais, confira [Verificação Estendida Transact-SQL](#bkmk_evf) mais adiante neste tópico|  
|Tipos de saída|||  
|Aplicativo da camada de dados (arquivo .dacpac)|Habilitado e bloqueado. A saída da compilação de um projeto de banco de dados sempre produz um pacote .dacpac quando o projeto é compilado.|Se você estiver usando a versão do SQL Server Data Tools (SSDT) que tem a opção "Criar arquivo .dacpac de nível baixo adicional (v2.0)", marque-a se quiser que o pacote seja compatível com o SQL Server Management Studio ou o Portal de Gerenciamento do SQL Azure. Você pode implantar um pacote .dacpac diretamente do SSDT, mas somente poderá implantar uma versão 2.0 do arquivo .dacpac por meio do SQL Server Management Studio quando o SQL Server Data Tools for lançado.|  
|Criar Script (Arquivo .sql)||Especifica se um script CREATE .sql completo é gerado para todos os objetos do projeto e colocado na pasta bin\debug quando o projeto é compilado. É possível criar um script de atualização incremental usando o comando **Publicação de Projeto** ou o utilitário de Comparação do SQL.|  
|Genérico|||  
|Esquema padrão|dbo|Especifica o esquema padrão no qual os objetos SQLCLR e Transact\-SQL são criados. É possível substituir essa configuração especificando o esquema diretamente em objetos.|  
|Incluir nome de esquema no nome de arquivo.|não|Especifica se os nomes de arquivos incluem o esquema como um prefixo (por exemplo, dbo.Products.table.sql). Se essa caixa de seleção for limpa, os nomes de arquivos de objetos terão o formato ObjectName.ObjectType.sql (por exemplo, Products.table.sql).|  
|Validar Uso de Maiúsculas em Identificadores|sim|Especifica se maiúsculas e minúsculas em identificadores de objetos SQL do projeto são validadas quando o projeto é compilado. Essa opção se aplica a projetos de banco de dados que especificam agrupamento com diferenciação de maiúsculas e minúsculas para o banco de dados.|  
|Configurações de Banco de Dados|Configurações padrão baseadas nos parâmetros padrão para um banco de dados|Exemplos de configurações que podem ser especificadas incluem o método de agrupamento e o nível do banco de dados para um banco de dados do SQL Server.|  
  
## <a name="bkmk_evf"></a>Verificação Estendida Transact-SQL  
  
> [!IMPORTANT]  
> O recurso de verificação de Transact-SQL estendida será removido da próxima versão do recurso de SQL Server Data Tools e da próxima versão principal do Visual Studio.  
  
A Verificação Estendida Transact-SQL é um recurso do sistema de projetos de banco de dados que permite aos desenvolvedores enviar o projeto de banco de dados ao Serviço do Compilador Transact-SQL durante a compilação a fim de validar o código em relação ao analisador e interpretador do Mecanismo do SQL Server.  
  
### <a name="transact-sql-compiler-service"></a>Serviço do Compilador Transact-SQL  
O Serviço do Compilador Transact-SQL é um componente baseado no Mecanismo de Banco de Dados do Microsoft SQL Server 2012. Esse serviço pode validar a sintaxe e a semântica das instruções DDL com a mesma fidelidade que um Mecanismo de Banco de Dados do Microsoft SQL Server 2012. E significa que o Serviço do Compilador não tem suporte para a sintaxe ou recursos que foram substituídos no Microsoft SQL Server 2012. Para obter mais informações sobre recursos substituídos, consulte [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2012](http://msdn.microsoft.com/en-us/library/ms144262%28v=sql.110%29.aspx).  
  
Para validar o projeto de banco de dados, o Serviço do Compilador cria um banco de dados parcialmente independente e simula a execução das instruções DDL em relação àquele banco de dados. Para obter mais informações, consulte [Bancos de dados parcialmente independentes](http://msdn.microsoft.com/en-us/library/ff929071%28v=SQL.110%29.aspx).  
  
O Serviço do Compilador tem duas categorias de limitações.  
  
Recursos que dependem da configuração do banco de dados ou da instância incluindo:  
  
-   Referências de objeto de e ou 4 partes  
  
-   Tabelas de arquivos  
  
-   Controle de alterações  
  
-   Funções dos conjuntos de linhas - OPENROWSET, OPENQUERY, OPENDATASOURCE  
  
-   Pesquisa semântica de texto completo  
  
Recursos que não têm suporte para validação no momento incluindo:  
  
-   Service Broker  
  
-   Esquemas particionados com grupos de arquivos definidos pelo usuário  
  
-   Agrupamento de metadados do SQL Azure (o Serviço do compilador usa o agrupamento de metadados do banco de dados parcialmente independente do SQL Server 2012 - Latin1_General_100_CI_AS_KS_WS_SC.  
  
### <a name="enablingdisabling-extended-verification"></a>Habilitar/Desabilitar a Verificação Estendida Transact-SQL  
A Verificação Estendida Transact-SQL é habilitada por padrão em um projeto de banco de dados que é criado diretamente de um banco de dados do SQL Azure ou em um projeto cuja plataforma de destino é configurada para o SQL Azure. Recomenda-se que a Verificação Estendida seja usada durante o desenvolvimento para SQL Azure ou em um banco de dados com escopo de aplicativo direcionado para SQL Server 2012. Para obter mais informações sobre bancos de dados com escopo de aplicativo, consulte [Bancos de dados parcialmente independentes](http://msdn.microsoft.com/en-us/library/ff929071%28v=SQL.110%29.aspx).  
  
O recurso de Verificação Estendida também pode ser usado durante o desenvolvimento de um banco de dados para SQL Server 2008/R2 a fim de ter compatibilidade com o Microsoft SQL Server 2012 e o SQL Azure.  
  
##### <a name="to-enable-or-disable-extended-verification-at-the-project-level"></a>Para habilitar ou desabilitar a Verificação Estendida Transact-SQL nos projetos  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no arquivo de projeto e depois clique em **Propriedades**.  
  
2.  Em **Configurações do Projeto**, em **Plataforma de Destino**, marque ou desmarque **Habilitar a verificação estendida do Transact-SQL para objetos comuns**.  
  
##### <a name="to-disable-extended-verification-at-the-file-level"></a>Para desabilitar a Verificação Estendida no arquivos  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em um arquivo .sql.  
  
    > [!NOTE]  
    > Para desabilitar o recurso Verificação Transact\-SQL Estendida no nível do arquivo, a propriedade **Ação de Compilação** do arquivo deve ser definida como **Compilar**.  
  
2.  Em **Propriedades**, altere a propriedade **Verificação Estendida T-SQL** para **False**.  
  
![Propriedades do arquivo](../ssdt/media/ssdt-evf.gif "Propriedades do arquivo")  
  
### <a name="special-considerations-for-collations"></a>Considerações especiais para agrupamentos  
Para obter mais informações sobre agrupamentos em bancos de dados parcialmente independentes, consulte [Agrupamentos de bancos de dados independentes](http://msdn.microsoft.com/en-us/library/ff929080%28v=sql.110%29.aspx).  
  
## <a name="bkmk_sqlclr"></a>SQLCLR  
Para obter informações sobre as opções de Assembly, consulte [Caixa de diálogo Informações do Assembly](http://msdn.microsoft.com/en-us/library/1h52t681.aspx?queryresult=true).  
  
Para obter informações sobre como assinar, consulte a seção **Assinatura do Assembly** do tópico [Página de assinatura, Project Designer](http://msdn.microsoft.com/en-us/library/0k50fs3b.aspx?queryresult=true) .  
  
## <a name="bkmk_sqlclr_sqlclrbuild"></a>Build SQLCLR e SQLCLR  
As páginas de propriedades de **SQLCLR** e **Compilação SQLCLR** contêm muitas configurações para usar objetos SQL CLR em seu projeto. Especificamente, a página de propriedades de **SQLCLR** tem uma configuração de nível de permissão para definir permissões no assembly do SQLCLR. Também tem um parâmetro "Gerar DDL" para controlar se o DDL (Dynamic Data Language) é gerado para os objetos SQLCLR adicionados ao projeto. A página de propriedades de **Compilação** contém todas as opções de compilador que podem ser definidas para configurar a compilação de código SQLCLR no projeto.  
  
A página de propriedades **Compilação SQLCLR** contém configurações avançadas de compilação para compilar seus objetos SQL CLR. São fornecidas diferentes opções com base na linguagem (VB ou C#) usada para codificar os objetos SQL CLR.  
  
1.  Se o objeto for escrito em C#, você poderá acessar as opções com um clique no botão **Avançado** na página de propriedades de **Compilação SQLCLR**. As descrições das opções da linguagem C# podem ser localizadas em [Caixa de diálogo Configurações de Compilação Avançadas (C#)](http://msdn.microsoft.com/en-us/library/s4wcexbc.aspx).  
  
2.  Se o objeto for escrito em VB, você poderá primeiro escolher VB na lista suspensa **Linguagem** e clicar no botão **Avançado** . As descrições para as opções do VB podem ser localizadas em [Caixa de diálogo Configurações de Compilador Avançadas (Visual Basic)](http://msdn.microsoft.com/en-us/library/07bysfz2.aspx)  
  
Para saber mais, confira [Compilar propriedades de configuração](http://msdn.microsoft.com/query/dev10.query?appId=Dev10IDEF1&l=EN-US&k=k(CS.PROJECTPROPERTIESBUILD))  
  
## <a name="bkmk_build"></a>Compilação  
É possível escolher uma configuração de compilação para cada projeto de banco de dados de sua solução. Por padrão, há uma única configuração, mas você pode adicionar configurações personalizadas. Você pode optar por fazer isso, por exemplo, se desejar uma configuração personalizada na qual você sempre exclui e recria o banco de dados. Em soluções que contém diferentes tipos de projeto, você pode criar uma configuração de solução personalizada que contenha uma configuração de compilação específica para cada projeto.  
  
#### <a name="to-specify-a-build-configuration-for-a-solution"></a>Para especificar uma configuração de compilação para uma solução.  
  
1.  No **Gerenciador de Soluções**, clique no nó da solução para a qual você deseja especificar uma configuração da compilação.  
  
2.  No menu **Compilar** , clique em **Gerenciador de Configurações**. A caixa de diálogo **Gerenciador de Configurações** é exibida.  
  
    Especifique os parâmetros de configuração que você deseja usar para cada projeto de sua solução.  
  
#### <a name="to-specify-a-build-configuration-for-a-database-project"></a>Para especificar uma configuração de compilação para um projeto de banco de dados.  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de banco de dados para o qual você deseja especificar uma configuração da compilação e selecione **Propriedades**.  
  
2.  Na guia **Compilar** , use a lista suspensa **Configuração** para especificar os parâmetros de configuração que você deseja usar para este projeto.  
  
As configurações da tabela a seguir aplicam-se às configurações de compilação deste projeto de banco de dados.  
  
|Campo|Valor padrão|Descrição|  
|---------|-----------------|---------------|  
|Caminho de saída da compilação|bin\Debug\|Especifica onde a saída da compilação será gerada quando você compilar ou implantar o projeto de banco de dados. Se especificar um caminho relativo, você deverá especificá-lo como relativo ao caminho do projeto do banco de dados. Se o caminho não existir, ele será criado.|  
|Nome do arquivo de saída da compilação|*DatabaseProjectName*|Especifica o nome que você deseja dar à saída gerada ao compilar o projeto do banco de dados.|  
|Tratar avisos Transact\-SQL como erros|não|Especifica se um aviso Transact\-SQL deve fazer com que o processo de compilação e implantação seja cancelado. Se essa caixa de seleção estiver desmarcada, os avisos serão exibidos, mas o processo de compilação e implantação continuará. Essa configuração é específica ao projeto, não ao usuário, e é armazenada no arquivo .sqlproj.|  
|Suprimir avisos Transact\-SQL|Em branco|Especifica uma lista de números de avisos, delimitados por vírgula ou ponto e vírgula, que identificam os avisos suprimidos.<br /><br />Os avisos suprimidos não são exibidos na janela **Lista de Erros** e não afetam o êxito da compilação, mesmo se você marcar a caixa de seleção **Tratar avisos Transact\-SQL como erros**.|  
  
## <a name="bkmk_sqlcmd_variables"></a>Variáveis SQLCMD  
Em Projetos de Banco de Dados do SQL Server é possível utilizar variáveis SQLCMD para fornecer substituição dinâmica a ser usada para depuração ou publicação. Você insere o nome e os valores da variável e, durante a compilação, os valores são substituídos. Se não houver valores locais, o valor padrão será usado. Com a inserção dessas variáveis em propriedades de projetos, elas serão oferecidas automaticamente na publicação e serão armazenadas em perfis de publicação. É possível efetuar pull nos valores do projeto das variáveis na publicação por meio do botão Carregar Valores.  
  
Verifique se as variáveis corretas são inseridas nas propriedades do projeto, porque essas variáveis não são validadas em relação a um script no projeto, nem são usadas em script populado automaticamente.  
  
Além disso, a publicação de linha de comando permite que você substitua esses valores na linha de comando ou usando um perfil.  
  
## <a name="bkmk_build_events"></a>Eventos de Compilação  
É possível usar essas configurações para especificar que uma linha de comando seja executada antes do início da operação de compilação e que uma linha de comando seja executada após a operação de compilação ser concluída.  
  
|Campo|Valor padrão|Descrição|  
|---------|-----------------|---------------|  
|Linha de comando de evento de pré-compilação|Nenhum|Especifica que a linha de comando deve ser executada antes do projeto ser compilado. Clique em **Editar Pré-compilação** para modificar a linha de comando.|  
|Linha de comando de eventos pós-compilação|Nenhum|Especifica que a linha de comando deve ser executada depois do projeto ser compilado. Clique em **Editar Pós-compilação** para modificar a linha de comando.|  
|Executar o evento pós-compilação|Na compilação bem-sucedida|Especifica se a linha de comando pós-compilação deve ser executada sempre, apenas se a compilação for bem-sucedida ou apenas quando a compilação atualizar a saída do projeto (o script de compilação).|  
  
## <a name="bkmk_debug"></a>Depurador  
É possível usar essas configurações para controlar a depuração de seu projeto de banco de dados.  
  
|Campo|Valor padrão|Descrição|  
|---------|-----------------|---------------|  
|Iniciar Ação|Nenhum|Especifica um script ou um programa externo para execução quando você depura seu projeto.|  
|Cadeia de Conexão de Destino|Fonte de Dados=(localdb)\\*SolutionName*;Catálogo Inicial=*DatabaseProjectName*;Segurança Integrada=True;Pooling=False;Tempo Limite de Conexão=30|Especifica as informações de conexão do servidor de banco de dados de destino para a configuração da compilação especificada. A cadeia de conexão padrão é em relação a uma instância e banco de dados LocalDB do SQL Server criados localmente.|  
|Implantar propriedades do banco de dados|Sim|Especifica se as configurações de DatabaseProperties.DatabaseProperties são implantadas ou atualizadas quando você compila ou implanta o projeto de banco de dados.|  
|Sempre recriar banco de dados|não|Especifica se o banco de dados será cancelado e recriado em vez da execução de uma atualização incremental. Você pode selecionar essa caixa de seleção se desejar executar testes de unidade de banco de dados em uma implantação limpa do banco de dados, por exemplo. Se a caixa de seleção for limpa, o banco de dados existente será atualizado, em vez de ser removido e recriado.|  
|Bloquear implantação incremental se puder ocorrer perda de dados|sim|Especifica se a implantação será interrompida se uma atualização provocar perda de dados. Se essa caixa de seleção for selecionada, as alterações que criariam a perda de dados farão com que a implantação seja interrompida com um erro, o que impede que os dados sejam perdidos. Por exemplo, a implantação seria interrompida se uma coluna `varchar(50)` fosse alterada para `varchar(30)`.<br /><br />**OBSERVAÇÃO:** A implantação será bloqueada apenas se as tabelas onde a perda de dados pode ocorrer contiverem dados. A implantação continuará se nenhum dado for perdido.|  
|REMOVER objetos no destino, mas não no projeto|não|Especifica se os objetos que estão no banco de dados de destino, mas não no projeto do banco de dados devem ser removidos como parte do script de implantação. É possível excluir alguns arquivos de seu projeto para removê-los temporariamente de seu script de compilação. No entanto, você pode deixar as versões existentes desses objetos no banco de dados de destino. Essa caixa de seleção não terá nenhum efeito se a caixa de seleção **Sempre recriar banco de dados** estiver selecionada, pois o banco de dados será removido.|  
|No usar instruções ALTER ASSEMBLY para atualizar tipos CLR|não|Especifica se as instruções ALTER ASSEMBLY são usadas para atualizar tipos CLR (Common Language Runtime) ou se o objeto que instancia o tipo CLR será removido e recriado quando você implantar alterações.|  
|Avançado...|não|Botão de comando que permite especificar opções que controlam os eventos e o comportamento da implantação.|  
  
## <a name="bkmk_ref_paths"></a>Caminhos de Referência  
É possível usar esta página para definir as variáveis do servidor e do banco de dados que estão associadas a uma referência entre bancos de dados. Além disso, você pode especificar os valores dessas variáveis. Para obter mais informações, consulte [Usando referências em projetos de banco de dados](http://msdn.microsoft.com/en-us/library/bb386242.aspx).  
  
## <a name="bkmk_code_analysis"></a>Análise de Código  
Você pode usar Análise de Código para descobrir problemas potenciais em seus scripts, como design, nomeação e problemas de desempenho. As regras para projetos de bancos de dados são organizadas em conjuntos de regras predefinidas que se destinam a áreas específicas, e você pode habilitar ou desabilitar qualquer regra na guia **Análise de Código** na página de propriedades **Propriedades de Projeto** . Na mesma guia, você pode especificar a análise de código para ser executada automaticamente toda vez que um projeto é compilado, ou se os avisos são tratados como erros.  
  
Para usar a Análise de Código manualmente, clique com o botão direito do mouse no seu projeto no **Gerenciador de Soluções** e selecione **Executar Análise de Código**. Os avisos da análise de código são listados na janela **Lista de Erros** . Você pode clicar duas vezes em um aviso para navegar para o código-fonte que contém o problema e você pode exibir informações adicionais e possíveis correções para um aviso usando o menu contextual **Mostrar Ajuda para erros**. Para obter mais informações sobre Análise de Código, consulte [Analisando o código do banco de dados para melhorar a qualidade do código](http://msdn.microsoft.com/en-us/library/dd172133.aspx)(a página pode estar em inglês).  
  
