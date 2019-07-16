---
title: Converter bancos de dados do MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1ad4cbbdf80422f87c850c44e47f82899de4c82a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103066"
---
# <a name="converting-mysql-databases-mysqltosql"></a>Converter bancos de dados MySQL (MySQLToSQL)
Depois de se conectar ao MySQL, conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure e defina o projeto e as opções de mapeamento de dados, você pode converter objetos de banco de dados MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos de banco de dados do SQL Azure.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto do MySQL, converte-os em semelhante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure objetos e, em seguida, carrega essas informações nos metadados SSMA. Não carrega as informações para a instância da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em seguida, você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Gerenciador de metadados do SQL Azure.  
  
Durante a conversão, o SSMA imprime mensagens de saída para o painel de saída e mensagens de erro para o painel de lista de erros. Use as informações de erro e de saída para determinar se é preciso modificar seus bancos de dados do MySQL ou o processo de conversão para obter os resultados da conversão desejada.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto na **configurações do projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte tabelas e índices. Para obter mais informações, consulte [configurações do projeto &#40;conversão&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>Resultados de conversão  
A tabela a seguir mostra quais objetos de MySQL são convertidos e resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos:  
  
|||  
|-|-|  
|**Objetos do MySQL**|**Objetos do SQL Server resultantes**|  
|Tabelas com objetos dependentes, como índices|O SSMA cria tabelas com objetos dependentes. Tabela for convertida com todos os índices e restrições. Os índices são convertidos em separado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos.<br /><br />**Mapeamento de tipo de dados espaciais** podem ser executadas somente no nível de nó de tabela.<br /><br />Para obter mais informações sobre as configurações de conversão de tabela, consulte [configurações de conversão](conversion-settings-mysqltosql.md)|  
|Funções|Se a função pode ser convertida diretamente para o Transact-SQL, o SSMA cria uma função. Em alguns casos, a função deve ser convertida em um procedimento armazenado. Isso pode ser feito por meio **conversão de função** nas configurações do projeto. Nesse caso, o SSMA cria um procedimento armazenado e uma função que chama o procedimento armazenado.<br /><br />**Opções de dado:**<br /><br />Converter de acordo com as configurações de projeto<br /><br />Converter em função<br /><br />Converter em procedimento armazenado<br /><br />Para obter mais informações sobre configurações de função de conversão, consulte [configurações de conversão](conversion-settings-mysqltosql.md)|  
|Procedimentos|Se o procedimento pode ser convertido diretamente para o Transact-SQL, o SSMA cria um procedimento armazenado. Em alguns casos, um procedimento armazenado deve ser chamado em uma transação autônoma. Nesse caso, o SSMA cria dois procedimentos armazenados: uma que implementa o procedimento e outro que é usada para chamar a implementação de procedimento armazenado.|  
|Conversão de banco de dados|Bancos de dados como objetos de MySQL não são convertidos diretamente pelo SSMA para MySQL. Bancos de dados MySQL são tratados mais como nomes de esquema e todos os parâmetros físicos serão perdidos durante a conversão. SSMA para MySQL usa [mapeamento de bancos de dados MySQL para esquemas SQL Server &#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) para mapear objetos de banco de dados MySQL para o par de banco de dados ou o esquema do SQL Server apropriado.|  
|Conversão de gatilho|**O SSMA cria gatilhos com base nas seguintes regras:**<br /><br />ANTES dos gatilhos são convertidos em gatilhos INSTEAD OF T-SQL<br /><br />Gatilhos AFTER são convertidos em gatilhos depois de T-SQL com ou sem iterações por linhas.|  
|Conversão de modo de exibição|O SSMA cria exibições com objetos dependentes|  
|Conversão de instrução|-Cada objeto de instrução SQL pode conter uma única instrução de MySQL (como DDL, DML e outros tipos de instruções) ou BEGIN... Bloco final.<br />-   **Conversão de várias instruções: BEGIN... Conversão de bloco final**instrução SQL também pode conter um BEGIN... Bloco END, como na definição de procedimento, função ou gatilho. Esses blocos devem ser convertidos da mesma forma que eles estão sendo convertidos para os objetos de instrução únicos do MySQL.|  
  
## <a name="converting-mysql-database-objects"></a>Converter objetos de banco de dados MySQL  
Para converter objetos de banco de dados MySQL, primeiro selecione os objetos que você deseja converter e, em seguida, ter o SSMA realizar a conversão. Para exibir mensagens de saída durante a conversão na **modo de exibição** menu, selecione **saída**.  
  
**Para converter objetos de MySQL à sintaxe do SQL Server ou SQL Azure**  
  
1.  No Gerenciador de metadados do MySQL, expanda o servidor MySQL e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione objetos a ser convertida:  
  
    -   Para converter todos os esquemas, selecione a caixa de seleção ao lado **bancos de dados**.  
  
    -   Para converter ou omitir um banco de dados, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda um esquema e, em seguida, selecione ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir os objetos individuais, expanda a pasta de categoria e, em seguida, selecione ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com botão direito **bancos de dados** e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou as categorias de objetos, clicando duas vezes o objeto ou a pasta pai e, em seguida, selecionando **converter esquema**.  
  
## <a name="viewing-conversion-problems"></a>Problemas de conversão de exibição  
Alguns objetos do MySQL podem não ser convertidos. Você pode determinar as taxas de sucesso de conversão, exibindo o relatório de resumo de conversão.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do MySQL, selecione **bancos de dados**.  
  
2.  No painel direito, selecione a **relatório** guia.  
  
    Este relatório mostra o relatório de resumo de avaliação para todos os objetos de banco de dados que foram avaliados ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório para um esquema individual, selecione o banco de dados no Gerenciador de metadados do MySQL.  
  
    -   Para exibir o relatório para um objeto individual, selecione o objeto no Gerenciador de metadados do MySQL. Objetos que têm problemas de conversão têm um ícone vermelho de erro.  
  
Para objetos que falha na conversão, você pode exibir a sintaxe que resultou em falha de conversão.  
  
**Para exibir os problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do MySQL, expanda **bancos de dados**.  
  
2.  Expanda o banco de dados que mostra um ícone vermelho de erro.  
  
3.  Em banco de dados, expanda uma pasta que tem um ícone vermelho de erro.  
  
4.  Selecione o objeto que tem um ícone vermelho de erro.  
  
5.  No painel direito, clique no **relatório** guia.  
  
6.  Na parte superior do **relatório** guia é uma lista suspensa. Se a lista mostra **estatísticas**, altere a seleção **origem**.  
  
    O SSMA exibirá o código-fonte e vários botões imediatamente acima do código.  
  
7.  Clique o **próximo problema** botão. Isso é um ícone vermelho de erro com uma seta que aponta para a direita.  
  
    O SSMA realçará o código-fonte problemático primeiro que ele localiza no objeto atual.  
  
Para cada item que não pôde ser convertido, você deve determinar o que você deseja fazer com esse objeto:  
  
-   Você pode modificar o objeto no banco de dados MySQL para remover ou revisar código problemático. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [conectando ao MySQL a &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Você pode excluir o objeto da migração. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure e o Gerenciador de metadados do MySQL, desmarque a caixa de seleção próxima ao item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure e a migração de dados do MySQL.  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no processo de migração [Carregando objetos de banco de dados convertidos no SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
