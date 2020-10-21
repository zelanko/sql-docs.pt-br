---
title: Assistente para Gerar e Publicar Scripts
description: Saiba como usar o Assistente para Gerar e Publicar Scripts para criar scripts a fim de transferir um banco de dados entre instâncias de banco de dados. As instâncias podem ser instâncias do Mecanismo de Banco de Dados do SQL Server ou do Banco de Dados SQL do Azure.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql9.swb.generatescriptswizard.chooseviews.f1
- sql13.swb.generatescriptswizard.manageproviders.f1
- sql9.swb.generatescriptswizard.scriptwizarddescription.f1
- sql9.swb.generatescriptswizard.choosedefaults.f1
- sql13.swb.generatescriptswizard.summarypage.f1
- sql13.swb.generatescriptswizard.providerconfiguration.f1
- sql9.swb.generatescriptswizard.chooseuddt.f1
- sql9.swb.generatescriptswizard.chooserules.f1
- sql13.swb.generatescriptswizard.introduction.f1
- sql13.swb.generatescriptswizard.setscriptingoptions.f1
- sql13.swb.generatescriptswizard.saveorpublishscripts.f1
- sql9.swb.generatescriptswizard.progress.f1
- sql9.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.welcome.f1
- sql9.swb.generatescriptswizard.scriptfileoption.f1
- sql13.swb.generatescriptswizard.chooseobjects.f1
- sql13.swb.generatescriptswizard.advancedpublishingoptions.f1
- sql9.swb.generatescriptswizard.selectdatabase.f1
- sql9.swb.generatescriptswizard.choosetables.f1
- sql9.swb.generatescriptswizard.choosestoredprocedures.f1
- sql9.swb.generatescriptswizard.chooseobjecttypes.f1
- sql13.swb.generatescriptswizard.advancedscriptingoptions.f1
- sql9.swb.generatescriptswizard.choosescriptoptions.f1
- sql9.swb.generatescriptswizard.chooseudf.f1
helpviewer_keywords:
- databases [SQL Server], publishing
- publishing databases
- scripts [SQL Server], generating
- scripts [SQL Server], publishing
- databases [SQL Server], generating scripts
- Publish Database Wizard
ms.assetid: 5ee520ba-ec7e-4199-a441-189e9e264b37
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 04/07/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: edbce6b52c224bc95aad1b3a6088696dba4c4f6a
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039012"
---
# <a name="generate-and-publish-scripts-wizard"></a>Assistente para Gerar e Publicar Scripts

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Você pode usar **Assistente para Gerar e Publicar Scripts** para criar scripts para transferir um banco de dados entre instâncias do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ou do [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. É possível gerar scripts para um banco de dados em uma instância do Mecanismo de Banco de Dados em sua rede local ou no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Os scripts gerados podem ser executados em outra instância do Mecanismo de Banco de Dados ou no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. É possível usar o assistente para publicar o conteúdo de um banco de dados diretamente em um serviço Web criado usando os Serviços de Publicação de Banco de dados. É possível criar scripts para um banco de dados inteiro ou limitá-lo a objetos específicos.

Confira mais detalhes sobre como usar o assistente para Gerar e Publicar Scripts no [Tutorial: Assistente para Gerar Scripts](../tutorials/scripting-ssms.md#script-databases).

## <a name="before-you-begin"></a>Antes de começar

Os bancos de dados de origem e destino podem estar no [!INCLUDE[ssSDS](../../includes/sssds-md.md)], ou em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que esteja executando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior.

### <a name="publishing-to-a-hosted-service"></a><a name="PubHostSvc"></a> Publicando em um serviço hospedado

Além de criar scripts, você pode usar o **Assistente para Gerar e Publicar Scripts** para criar scripts para publicar um banco de dados em um tipo específico de serviço Web hospedado do SQL Server. O Conjunto de Ferramentas de Hospedagem do SQL Server fornece Serviços de Publicação de Banco de dados como um projeto de origem compartilhado no CodePlex. O projeto dos Serviços de Publicação de Banco de dados pode ser usado por provedores de hospedagem na Web para criar um conjunto de serviços Web que facilitam a implantação de banco de dados no serviço Web para clientes. Para obter mais informações sobre como baixar o Conjunto de Ferramentas de Hospedagem do SQL Server, consulte [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025)(em inglês).

Para publicar um banco de dados em um serviço de hospedagem Web, selecione a opção **Publicar no Serviço Web** na página **Definir Opções de Script** do assistente.

### <a name="permissions"></a><a name="Permissions"></a> Permissões

A permissão mínima para publicar um banco de dados é a associação à função de banco de dados fixa db_ddladmin no banco de dados de origem. A permissão mínima para publicar um script de banco de dados para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no provedor de hospedagem é a participação na função de banco de dados fixa db_ddladmin no banco de dados de destino.

O usuário também tem que fornecer um nome e uma senha do usuário para acessar a conta do provedor de hospedagem para publicação com o assistente. O banco de dados de destino deve ser criado no provedor de hospedagem antes da publicação do banco de dados de origem. A publicação substitui objetos naquele banco de dados existente.

## <a name="using-the-generate-and-publish-scripts-wizard"></a><a name="GenPubScriptWiz"></a> Usando o Assistente para Gerar e Publicar Scripts

**Para gerar e publicar um script**

1. No **Pesquisador de Objetos**, expanda o nó da instância que contém o banco de dados a ser incluído no script.

2. Aponte para **Tarefas** e selecione **Gerar Scripts**.

    ![Assistente para Gerar Scripts](media/generate-and-publish-scripts-wizard/generate-scripts.png)

3. Conclua as etapas das caixas de diálogo do assistente:

    - [Página de Introdução](#Introduction)
    - [Página Escolher Objetos](#ChooseObjects)
    - [Página Definir Opções de Script](#SetScriptOpt)
    - [Página Opções de Script Avançadas](#AdvScriptOpt)
    - [Página de Resumo](#Summary)
    - [Página Salvar ou Publicar Scripts](#SavePubScripts)

###  <a name="introduction-page"></a><a name="Introduction"></a> Página de Introdução

Esta página descreve as etapas para gerar ou publicar um script.

**Não mostrar esta página novamente** – Ignore esta página na próxima vez que iniciar o **Assistente para Gerar e Publicar Scripts**.

  ![Página de Introdução](media/generate-and-publish-scripts-wizard/intro.png)

### <a name="choose-objects-page"></a><a name="ChooseObjects"></a> Página Escolher Objetos

Use esta página para escolher quais objetos você deseja incluir nos scripts gerados por este assistente. Na página do assistente a seguir, você tem a opção de salvar esses scripts no local de sua escolha ou usá-los para publicar objetos de banco de dados em um provedor remoto de hospedagem Web que tenha os [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025) instalados.

**Opção Gerar Script de Todo o Banco de Dados** – Selecione a fim de gerar scripts para todos os objetos do banco de dados e incluir um script para o próprio banco de dados.

   ![Gerar script de todo o BD](media/generate-and-publish-scripts-wizard/script-all.png)

**Selecionar objetos de banco de dados específicos** – Selecione a fim de limitar o assistente para gerar scripts somente para os objetos específicos no banco de dados escolhido:

- **Objetos de banco de dados** – Selecione, pelo menos, um objeto para incluir no script.

- **Selecionar Tudo** – Marca todas as caixas de seleção disponíveis.

- **Desmarcar Tudo** – Limpa todas as caixas de seleção. Para continuar, você deve selecionar pelo menos um objeto de banco de dados.

   ![Gerar um script específico](media/generate-and-publish-scripts-wizard/script-specific-objects.png)

### <a name="set-scripting-options-page"></a><a name="SetScriptOpt"></a> Página Definir Opções de Script

Use esta página para especificar se você deseja que o assistente salve scripts no local de sua escolha ou use os scripts para publicar objetos de banco de dados em um provedor remoto de hospedagem Web. Para publicar, você precisa ter acesso a um serviço Web instalado usando os Database Publishing Services.

**Opções** – Se desejar que o assistente salve scripts em um local de sua preferência, selecione **Salvar scripts em um local específico**. Você pode executar os scripts posteriormente em relação a uma instância do Mecanismo de Banco de Dados ou em relação ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Se você desejar que o assistente publique seus objetos de banco de dados em um provedor remoto de hospedagem Web, selecione **Publicar no serviço Web**.

**Salvar Scripts em uma Localização Específica** – salve um ou mais arquivos de script Transact-SQL em uma localização especificada.

![Salvar como notebook](media/generate-and-publish-scripts-wizard/save.png)

- **[Salvar como bloco de anotações](../../azure-data-studio/notebooks/notebooks-guidance.md)** – Salve o script em um ou mais arquivos .sql. Selecione o botão Procurar ( **…** ) para especificar um nome e uma localização para o arquivo.

- **Salvar como arquivo de script** – Salve o script em um ou mais arquivos .sql. Selecione o botão Procurar ( **…** ) para especificar um nome e uma localização para o arquivo. Marque a caixa de seleção **Substituir o arquivo existente** para substituir o arquivo se já existir outro com o mesmo nome. Selecione **Arquivo de script único** ou **Arquivo de script único por objeto** para especificar como os scripts devem ser gerados. Selecione **Texto Unicode** ou **Texto ANSI** para especificar o tipo de texto que deve ser usado no script.

- **Salvar na Área de Transferência** – Salve o script Transact-SQL na área de transferência.

- **Abrir em nova janela de consulta** – Gere o script em uma janela do Editor de Consultas do Mecanismo de Banco de Dados. Se nenhuma janela de editor for aberta, uma nova janela de editor será aberta como o destino do script.

- **Avançado** – Exiba a caixa de diálogo **Opções de Publicação Avançadas** em que você pode selecionar opções avançadas para publicar scripts.

- **Provedor** – Selecione o provedor que especifica as informações de conexão para o serviço de host Web que hospeda o banco de dados em que você deseja publicar os objetos selecionados. Você deve ter pelo menos um provedor na caixa de diálogo **Gerenciar Provedores** para selecionar um provedor.

- **Banco de dados de destino** – Selecione o banco de dados de destino em que você deseja publicar os objetos selecionados. Você deve selecionar um provedor antes de selecionar um banco de dados de destino.

### <a name="advanced-scripting-options-page"></a><a name="AdvScriptOpt"></a> Página Opções de Script Avançadas

Use essa página para especificar como você deseja que esse assistente gere scripts. Muitas opções diferentes estão disponíveis. As opções ficarão acinzentadas se não tiverem suporte da versão do SQL Server ou do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] especificado no **Tipo de mecanismo de banco de dados**.

![Opções avançadas](media/generate-and-publish-scripts-wizard/advanced.png)

**Opções** – Especifique opções avançadas selecionando um valor da lista de configurações disponíveis à direita de cada opção.

**Geral** – as opções a seguir se aplicam ao script inteiro.

- **Preenchimento ANSI** – Inclui **ANSI PADDING ON** no script. O padrão é **True**.

- **Acrescentar ao arquivo** – Se for **True**, este script será adicionado à parte inferior de um script existente, especificado na página **Definir Opções de Script** . Se for **False**, o novo script substituirá um script anterior. O padrão é **False**.

- **Verifique a existência do objeto** – quando **True**, o adiciona a verificação de existência antes de gerar a instrução CREATE para seus Objetos SQL. Por exemplo: tabelas, exibições, funções ou procedimentos armazenados. A instrução CREATE é encapsulada em uma instrução IF. Se você souber que seu destino está limpo, o script será muito mais limpo. Se você NÃO esperar que os objetos existam no destino, receberá um erro. O padrão é **False**.

- **Continuar o script se houver erro** – Quando for **False**, o script será interrompido quando ocorrer um erro. Se for **True**, o script continuará. O padrão é **False**.

- **Converter UDDTs em tipos de base** – Se for **True**, os UDDT (tipos de dados definidos pelo usuário) serão convertidos nos tipos de dados base subjacentes que foram usados para criá-los. Use **True** quando o UDDT não existir no banco de dados em que o script é executado. Se for **False**, serão usados UDDTs. O padrão é **False**.

- **Gerar script para objetos dependentes** – Gera um script para qualquer objeto que precise estar presente quando o script do objeto selecionado for executado. O padrão é **True**.

- **Incluir cabeçalhos descritivos** – Se for **True**, comentários descritivos serão adicionados ao script, separando-o em seções para cada objeto. O padrão é **False**.

- **Incluir se NOT EXISTS** – Se for **True**, o script incluirá uma instrução para verificar se o objeto já existe no banco de dados e não tentará criar um novo objeto se já existir um. O padrão é **False**.

- **Incluir nomes de restrição do sistema** – quando essa opção é definida como **False**, o valor padrão de restrições que foram nomeadas automaticamente no banco de dados de origem é renomeado automaticamente no banco de dados de destino. Se for **True**, as restrições terão o mesmo nome nos bancos de dados de origem e de destino.

- **Incluir instruções sem suporte** – Se for **False**, o script não conterá instruções para objetos sem suporte na versão de servidor selecionada ou no tipo de mecanismo. Se for **True**, o script conterá os objetos sem suporte. Cada instrução para um objeto sem suporte tem um comentário de que a instrução deve ser editada antes que o script seja executado conforme a versão do SQL Server ou o tipo de mecanismo selecionado. O padrão é **False**.

- **Qualificar nomes de objetos do esquema** – Inclui o nome do esquema no nome de objetos que são criados. O padrão é **True**.

- **Associação de script** – Gera um script para associação padrão e objetos de regra. O padrão é **False**. Para obter mais informações, veja [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md) e [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md).

- **Ordenação de scripts** – Inclui informações de ordenação no script. O padrão é **False**. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).

- **Padrões de script** – Inclui objetos padrão usados para definir valores padrão em colunas de tabela. O padrão é **True**. Para obter mais informações, veja [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md).

- **Script drop e create** – Se for **Script CREATE**, serão incluídas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar objetos. Se for o **Script DROP**, serão incluídas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para descartar objetos. Se for **Script DROP e CREATE**, a instrução drop [!INCLUDE[tsql](../../includes/tsql-md.md)] será incluída no script, seguida da instrução create, para cada objeto de script. O padrão é **Script CREATE**.

- **Propriedades estendidas do script** – Inclui propriedades estendidas no script se o objeto tem propriedades estendidas. O padrão é **True**.

- **Script para tipo de mecanismo** – Cria um script que pode ser executado no tipo selecionado do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ou em uma instância do Mecanismo de Banco de Dados do SQL Server. Objetos sem suporte no tipo especificado não são incluídos no script. O padrão é o tipo do servidor de origem.

- **Script para a versão do servidor** – Cria um script que pode ser executado na versão selecionada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Recursos que são novos em uma versão não podem ser incluídos em scripts executado por versões anteriores. O padrão é a versão do servidor de origem.

- **Logons de script** – Quando o objeto a ser gerado com scrip é um usuário de banco de dados, esta opção cria os logons dos quais o usuário depende. O padrão é **False**.

- **Gerar script de permissões em nível de objeto** – Inclui scripts para definir a permissão nos objetos no banco de dados. O padrão é **False**.

- **Estatísticas de script** – Quando definido como **Estatísticas do Script**, esta opção inclui a instrução **CREATE STATISTICS** para recriar estatísticas no objeto. A opção **Gerar script de estatísticas e histogramas** também cria informações de histograma. O padrão é **Não gerar script de estatísticas**. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).

- **Gerar script de USE DATABASE** – Adiciona a instrução **USE DATABASE** ao script. Para ter certeza de que os objetos de banco de dados serão criados no banco de dados correto, inclua a instrução **USE DATABASE** . Quando se espera que o script seja usado em um outro banco de dados, selecione **False** para omitir a instrução **USE DATABASE** . O padrão é **True**. Para obter mais informações, veja [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md).

- **Tipos de dados para o script** – Seleciona o que deve ser inserido no script: **Somente dados**, **Somente esquema** ou ambos. O padrão é **Esquema somente**.

**Opções de tabela/exibição** – As opções a seguir são válidas somente para scripts de tabelas ou exibições.

- **Controle de alterações de script** – Controle de alterações de scripts se for habilitado no banco de dados de origem ou nas tabelas no banco de dados de origem. O padrão é **False**. Para obter mais informações, veja [Sobre o controle de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md).

- **Restrições de Verificação do Script** – adiciona restrições **CHECK** ao script. O padrão é **True**. Restrições**CHECK** exigem que os dados inseridos em uma tabela atendam algumas condições especificadas. Para obter mais informações, consulte [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).

- **Opções de compactação de dados de script** – Gera scripts de opções de compactação de dados quando elas são configuradas no banco de dados de origem ou em tabelas no banco de dados de origem. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md). O padrão é **False**.

- **Chaves estrangeiras do script** – Adiciona chaves estrangeiras ao script. O padrão é **True**. Chaves estrangeiras indicam e impõem relações entre tabelas.

- **Índices de texto completo do script** – Gera script para a criação de índices de texto completo. O padrão é **False**.

- **Índices de script** – Gera script para a criação de índices nas tabelas. O padrão é **True**. Os índices ajudam você a localizar dados rapidamente.

- **Chaves primárias de script** – Gera script para a criação de chaves primárias em tabelas. O padrão é **True**. Chaves primárias identificam com exclusividade cada linha de uma tabela.

- **Gatilhos de script** – Gera script para a criação de gatilhos DML em tabelas. O padrão é **False**. Um gatilho DML é uma ação programada para executar quando um evento de linguagem de manipulação de dados (DML) ocorre no servidor de banco de dados. Para obter mais informações, consulte [DML Triggers](../../relational-databases/triggers/dml-triggers.md).

- **Chaves exclusivas do script** – Gera script para a criação de chaves exclusivas em tabelas. Chaves exclusivas evitam a inserção de dados duplicados. O padrão é **True**. Para obter mais informações, consulte [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).

### <a name="summary-page"></a><a name="Summary"></a> Página de Resumo

![Resumo do GS](media/generate-and-publish-scripts-wizard/summary.png)

Essa página resume as opções selecionadas nesse assistente. Para alterar uma opção, selecione **Anterior**. Para começar a gerar scripts que serão salvos ou publicados, selecione **Avançar**.

**Examinar as seleções** – Exibe as seleções feitas em cada página do assistente. Expanda um nó para ver as opções selecionadas para a página correspondente.

### <a name="save-or-publish-scripts-page"></a><a name="SavePubScripts"></a> Página Salvar ou Publicar Scripts  

Use esta página para monitorar o andamento do assistente enquanto ele ocorre.

**Detalhes** – Exiba a coluna **Ação** para consultar o andamento do assistente. Depois de gerar os scripts, o assistente salva os scripts em um arquivo ou os usa para publicar em um serviço Web, dependendo de suas seleções. Quando cada uma dessas etapas estiver concluída, selecione o valor na coluna **Resultado** para ver o resultado da etapa correspondente.

**Salvar Relatório** – Selecione para salvar os resultados do progresso do assistente em um arquivo.

**Cancelar** – Selecione para fechar o assistente antes da conclusão do processamento ou se ocorrer um erro.

**Concluir** – Selecione para fechar o assistente depois da conclusão do processamento ou se ocorrer um erro.

### <a name="save-scripts"></a>Salvar scripts

![Concluir](media/generate-and-publish-scripts-wizard/save-scripts-finish.png)

Se todas as configurações estiverem corretas, sua configuração será concluída com êxito.

## <a name="generating-scripts-on-azure-synapse-analytics"></a>Gerando scripts no Azure Synapse Analytics

Se a sintaxe gerada ao usar "Script como…" não parecer uma sintaxe [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] ou se você receber uma mensagem de erro, talvez seja necessário definir as opções de script no SQL Server Management Studio para o [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].

### <a name="how-to-set-default-scripting-options-to-sql-data-warehouse"></a>Como definir opções de script padrão para o SQL Data Warehouse

Para gerar script para objetos com a sintaxe [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] , defina a opção de script padrão como [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] da seguinte maneira:

1. Selecione **Ferramentas** e **Opções**.
2. Em **Opções Gerais de Script** , defina:
    1. Script para o tipo de mecanismo de banco de dados: **Banco de Dados SQL do Microsoft Azure**.
    2. Script da edição do mecanismo de banco de dados: **Edição do SQL Data Warehouse do Microsoft Azure**.
3. Selecione **OK**.

### <a name="how-to-generate-scripts-for-sql-data-warehouse-when-it-is-not-the-default-scripting-option"></a>Como gerar scripts para o SQL Data Warehouse quando esta não for a opção de script padrão

Se você definir [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] como a opção de script padrão, como mostrado acima, essas instruções poderão ser ignoradas. No entanto, se você optar por usar opções de script padrão diferentes, poderá receber um erro. Para evitar erros, siga estas etapas para Gerar e Publicar Scripts para [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]:

1. Clique com o botão direito do mouse no banco de dados SQL Data Warehouse.
2. Selecione **Gerar Scripts**.
3. Escolha os Objetos dos quais deseja gerar script.
4. Em **Opções de Script**, selecione **Avançado**. Em **Geral** , defina:
    1. Script para o tipo de mecanismo de banco de dados: **Banco de Dados SQL do Microsoft Azure**.
    2. Script da edição do mecanismo de banco de dados: **Edição do SQL Data Warehouse do Microsoft Azure**.
5. Selecione **Salvar ou Publicar Scripts** e **Concluir**.

As opções definidas na Etapa 4 não são lembradas. Se você preferir que essas opções sejam lembradas, siga as instruções em **Como definir opções de script padrão para o SQL Data Warehouse**.

## <a name="see-also"></a>Confira também

- [Instalando o SMO](../../relational-databases/server-management-objects-smo/installing-smo.md)

- [Copiar bancos de dados para outros servidores](../../relational-databases/databases/copy-databases-to-other-servers.md)