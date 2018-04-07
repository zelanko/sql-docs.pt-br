---
title: Conversão de bancos de dados MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1b1bbf54f4b8ddfa33b10d0aa1f5cb7cdbc139a6
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="converting-mysql-databases-mysqltosql"></a>Conversão de bancos de dados MySQL (MySQLToSQL)
Depois de se conectar ao MySQL, conectado à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure e conjunto de projeto e as opções de mapeamento de dados, você pode converter objetos de banco de dados MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos de banco de dados do SQL Azure.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto do MySQL, converte-os em semelhante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure objetos e, em seguida, carrega essas informações para os metadados do SSMA. Não carrega as informações para a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou o Gerenciador de metadados do SQL Azure.  
  
Durante a conversão, o SSMA imprime mensagens de saída para o painel de saída e mensagens de erro para o painel de lista de erros. Use as informações de saída e de erro para determinar se você precisa modificar seus bancos de dados MySQL ou o processo de conversão para obter os resultados da conversão desejada.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto no **configurações de projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte tabelas e índices. Para obter mais informações, consulte [configurações de projeto &#40;conversão&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>Resultados de conversão  
A tabela a seguir mostra quais objetos de MySQL são convertidos e resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos:  
  
|||  
|-|-|  
|**Objetos do MySQL**|**Objetos resultantes do SQL Server**|  
|Tabelas com objetos dependentes, como índices|O SSMA cria tabelas com objetos dependentes. Tabela é convertida com todos os índices e restrições. Os índices são convertidos em separado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos.<br /><br />**Mapeamento de tipo de dados espaciais** podem ser executadas somente no nível de nó de tabela.<br /><br />Para obter mais informações sobre as configurações de conversão de tabela, consulte [as configurações de conversão](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|Funções|Se a função pode ser convertida diretamente para o Transact-SQL, o SSMA cria uma função. Em alguns casos, a função deve ser convertida em um procedimento armazenado. Isso pode ser feito usando **conversão de função** nas configurações do projeto. Nesse caso, o SSMA cria um procedimento armazenado e uma função que chama o procedimento armazenado.<br /><br />**Opções fornecidas:**<br /><br />Converter de acordo com as configurações de projeto<br /><br />Converter em função<br /><br />Converter em procedimento armazenado<br /><br />Para obter mais informações sobre as configurações de conversão de função, consulte [as configurações de conversão](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|Procedimentos|Se o procedimento pode ser convertido diretamente para o Transact-SQL, o SSMA cria um procedimento armazenado. Em alguns casos, um procedimento armazenado deve ser chamado em uma transação autônoma. Nesse caso, o SSMA cria dois procedimentos armazenados: um que implementa o procedimento e outro que é usado para chamar a implementação do procedimento armazenado.|  
|Conversão de banco de dados|Bancos de dados como objetos de MySQL não são convertidos diretamente pelo SSMA para MySQL. Bancos de dados MySQL são tratados mais como um esquema de nomes e todos os parâmetros físicos serão perdidos durante a conversão. SSMA para MySQL usa [mapeamento de bancos de dados MySQL para esquemas SQL Server &#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) para mapear objetos de banco de dados MySQL para o par de banco de dados ou o esquema apropriado do SQL Server.|  
|Conversão de gatilho|**O SSMA cria gatilhos com base nas seguintes regras:**<br /><br />ANTES dos gatilhos são convertidos em gatilhos INSTEAD OF T-SQL<br /><br />Gatilhos AFTER são convertidos em gatilhos depois de T-SQL com ou sem iterações por linhas.|  
|Conversão de modo de exibição|O SSMA cria exibições com os objetos dependentes|  
|Conversão de instrução|-Cada objeto de instrução SQL pode conter uma única instrução MySQL (como DDL, DML e outros tipos de instruções) ou BEGIN... Bloco final.<br />-   **Conversão de várias instruções: BEGIN... Conversão de bloco final**instrução SQL também pode conter um BEGIN... Bloco END como na definição de procedimento, função ou gatilho. Os blocos devem ser convertidos da mesma forma que eles estão sendo convertidos para os objetos de instrução únicos do MySQL.|  
  
## <a name="converting-mysql-database-objects"></a>Converter objetos de banco de dados MySQL  
Para converter objetos de banco de dados MySQL, você primeiro selecionar os objetos que você deseja converter e, em seguida, SSMA executar a conversão. Para exibir mensagens de saída durante a conversão no **exibição** menu, selecione **saída**.  
  
**Para converter objetos de MySQL a sintaxe de SQL Server ou SQL Azure**  
  
1.  No Gerenciador de metadados do MySQL, expanda o servidor MySQL e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione objetos para converter:  
  
    -   Para converter todos os esquemas, selecione a caixa de seleção ao lado de **bancos de dados**.  
  
    -   Para converter ou omitir um banco de dados, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda um esquema e, em seguida, marque ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir os objetos individuais, expanda a pasta de categoria e, em seguida, marque ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com botão direito **bancos de dados** e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou as categorias de objetos, clicando duas vezes o objeto ou a pasta pai e, em seguida, selecionando **converter esquema**.  
  
## <a name="viewing-conversion-problems"></a>Problemas de conversão de exibição  
Alguns objetos do MySQL não podem ser convertidos. Você pode determinar as taxas de sucesso de conversão exibindo o relatório de resumo de conversão.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do MySQL, selecione **bancos de dados**.  
  
2.  No painel direito, selecione o **relatório** guia.  
  
    Este relatório mostra o relatório de resumo de avaliação para todos os objetos de banco de dados que tenham sido avaliada ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório para um esquema individual, selecione o banco de dados no Gerenciador de metadados do MySQL.  
  
    -   Para exibir o relatório para um objeto individual, selecione o objeto no Gerenciador de metadados do MySQL. Objetos que têm problemas de conversão têm um ícone de erro vermelho.  
  
Para objetos que falha na conversão, você pode exibir a sintaxe que resultaram em falha de conversão.  
  
**Para exibir os problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do MySQL, expanda **bancos de dados**.  
  
2.  Expanda o banco de dados que mostra um ícone de erro vermelho.  
  
3.  No banco de dados, expanda uma pasta que tem um ícone de erro vermelho.  
  
4.  Selecione o objeto que tem um ícone de erro vermelho.  
  
5.  No painel direito, clique no **relatório** guia.  
  
6.  Na parte superior do **relatório** guia é uma lista suspensa. Se a lista mostra **estatísticas**, altere a seleção do **fonte**.  
  
    O SSMA exibirá o código-fonte e vários botões imediatamente acima do código.  
  
7.  Clique o **próximo problema** botão. Este é um ícone de erro vermelho com uma seta que aponta para a direita.  
  
    O SSMA realçará o código-fonte problemático primeiro localiza no objeto atual.  
  
Para cada item que não puderam ser convertido, você deve determinar o que você deseja fazer com esse objeto:  
  
-   Você pode modificar o objeto no banco de dados MySQL para remover ou revisar código problemática. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [conectando ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Você pode excluir o objeto de migração. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure e o Gerenciador de metadados do MySQL, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure e migrando dados do MySQL.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [carregar objetos de banco de dados convertidos para o SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Bancos de dados MySQL migrando para o SQL Server - banco de dados SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
