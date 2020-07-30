---
title: Convertendo esquemas Oracle (OracleToSQL) | Microsoft Docs
description: Saiba como converter objetos de banco de dados Oracle em SQL Server objetos de banco de dados com o SSMA para Oracle, depois de definir opções e conectar-se ao Oracle e SQL Server.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 844d602168c063c90034469466ade816431481d4
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395161"
---
# <a name="converting-oracle-schemas-oracletosql"></a>Converter esquemas Oracle (OracleToSQL)
Depois de se conectar ao Oracle, conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e definir opções de mapeamento de projeto e de dados, você poderá converter objetos de banco de dado Oracle em objetos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="the-conversion-process"></a>O processo de conversão  
A conversão de objetos de banco de dados usa as definições de objeto do Oracle, converte-as em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos semelhantes e, em seguida, carrega essas informações nos metadados do SSMA. Ele não carrega as informações na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Em seguida, você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados.  
  
Durante a conversão, o SSMA imprime as mensagens de saída no painel de saída e as mensagens de erro no painel de Lista de Erros. Use as informações de saída e erro para determinar se você precisa modificar seus bancos de dados Oracle ou seu processo de conversão para obter os resultados de conversão desejados.  
  
## <a name="setting-conversion-options"></a>Configurando opções de conversão  
Antes de converter objetos, examine as opções de conversão do projeto na caixa de diálogo **configurações do projeto** . Usando essa caixa de diálogo, você pode definir como o SSMA converte funções e variáveis globais. Para obter mais informações, consulte [configurações do projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
## <a name="conversion-results"></a>Resultados da conversão  
A tabela a seguir mostra quais objetos Oracle são convertidos e os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos resultantes:  
  
|Objetos Oracle|Objetos SQL Server resultantes|  
|-|-|  
|Funções|Se a função puder ser convertida diretamente no [!INCLUDE[tsql](../../includes/tsql-md.md)] , o SSMA criará uma função.<br /><br />Em alguns casos, a função deve ser convertida em um procedimento armazenado. Nesse caso, o SSMA cria um procedimento armazenado e uma função que chama o procedimento armazenado.|  
|Procedimentos|Se o procedimento puder ser convertido diretamente no [!INCLUDE[tsql](../../includes/tsql-md.md)] , o SSMA criará um procedimento armazenado.<br /><br />Em alguns casos, um procedimento armazenado deve ser chamado em uma transação autônoma. Nesse caso, o SSMA cria dois procedimentos armazenados: um que implementa o procedimento e outro usado para chamar o procedimento armazenado de implementação.|  
|Pacotes|O SSMA cria um conjunto de procedimentos armazenados e funções que são unificados por nomes de objeto semelhantes.|  
|Sequências|O SSMA cria objetos de sequência (SQL Server 2012 ou SQL Server 2014) ou emula sequências Oracle.|  
|Tabelas com objetos dependentes, como índices e gatilhos|O SSMA cria tabelas com objetos dependentes.|  
|Exibir com objetos dependentes, como gatilhos|O SSMA cria exibições com objetos dependentes.|  
|Exibições materializadas|**O SSMA cria exibições indexadas no SQL Server com algumas exceções. A conversão falhará se a exibição materializada incluir uma ou mais das seguintes construções:**<br /><br />Função definida pelo usuário<br /><br />Campo/função/expressão não determinística em cláusulas SELECT, WHERE ou GROUP BY<br /><br />Uso de coluna float em SELECT *, WHERE ou GROUP BY cláusulas (caso especial de problema anterior)<br /><br />Tipo de dados personalizado (incluindo tabelas aninhadas)<br /><br />CONTAGEM ( &lt; campo distinto &gt; )<br /><br />FETCH<br /><br />junções OUTER (LEFT, RIGHT ou FULL)<br /><br />Subconsulta, outra exibição<br /><br />ACIMA, CLASSIFICAÇÃO, LEAD, LOG<br /><br />MIN, MAX<br /><br />UNIÃO, MENOS, INTERSEÇÃO<br /><br />HAVING|  
|Gatilho|**O SSMA cria gatilhos com base nas seguintes regras:**<br /><br />Os gatilhos BEFORE são convertidos em vez de gatilhos.<br /><br />Os gatilhos AFTER são convertidos em gatilhos AFTER.<br /><br />Gatilhos INSTEAD OF são convertidos em gatilhos INSTEAD OF. Vários gatilhos INSTEAD OF definidos na mesma operação são combinados em um gatilho.<br /><br />Os gatilhos em nível de linha são emulados usando cursores.<br /><br />Os gatilhos em cascata são convertidos em vários gatilhos individuais.|  
|Sinônimos|**Os sinônimos são criados para os seguintes tipos de objeto:**<br /><br />Tabelas e tabelas de objeto<br /><br />Exibições e exibições de objeto<br /><br />Procedimentos armazenados<br /><br />Funções<br /><br />**Os sinônimos para os seguintes objetos são resolvidos e substituídos por referências diretas de objeto:**<br /><br />Sequências<br /><br />Pacotes<br /><br />Objetos de esquema de classe Java<br /><br />Tipos de objeto definidos pelo usuário<br /><br />Os sinônimos de outro sinônimo não podem ser migrados e serão marcados como erros.<br /><br />Os sinônimos não são criados para exibições materializadas.|  
|Tipos definidos pelo usuário|**O SSMA não oferece suporte para conversão de tipos definidos pelo usuário. Os tipos definidos pelo usuário, incluindo seu uso em programas PL/SQL, são marcados com erros de conversão especiais orientados pelas seguintes regras:**<br /><br />A coluna de tabela de um tipo definido pelo usuário é convertida em VARCHAR (8000).<br /><br />O argumento do tipo definido pelo usuário para um procedimento armazenado ou função é convertido em VARCHAR (8000).<br /><br />A variável do tipo definido pelo usuário no bloco PL/SQL é convertida em VARCHAR (8000).<br /><br />A tabela de objetos é convertida em uma tabela padrão.<br /><br />A exibição de objeto é convertida em uma exibição padrão.|  
  
## <a name="converting-oracle-database-objects"></a>Convertendo objetos Oracle Database  
Para converter objetos do banco de dados Oracle, primeiro selecione os objetos que deseja converter e, em seguida, faça com que o SSMA execute a conversão. Para exibir mensagens de saída durante a conversão, no menu **Exibir** , selecione **saída**.  
  
**Para converter objetos Oracle em sintaxe de SQL Server**  
  
1.  No Gerenciador de metadados Oracle, expanda o servidor Oracle e, em seguida, expanda **esquemas**.  
  
2.  Selecione os objetos a serem convertidos:  
  
    -   Para converter todos os esquemas, marque a caixa de seleção ao lado de **esquemas**.  
  
    -   Para converter ou omitir um banco de dados, marque a caixa de seleção ao lado do nome do esquema.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda um esquema e marque ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir objetos individuais, expanda a pasta categoria e marque ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com o botão direito do mouse em **esquemas** e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou em sua pasta pai e, em seguida, selecionando **converter esquema**.  
  
## <a name="viewing-conversion-problems"></a>Exibindo problemas de conversão  
Alguns objetos Oracle podem não ser convertidos. Você pode determinar as taxas de êxito da conversão exibindo o relatório de conversão de resumo.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados Oracle, selecione **esquemas**.  
  
2.  No painel direito, selecione a guia **relatório** .  
  
    Este relatório mostra o relatório de avaliação de resumo para todos os objetos de banco de dados que foram avaliados ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório de um esquema individual, selecione o esquema no Gerenciador de metadados Oracle.  
  
    -   Para exibir o relatório de um objeto individual, selecione o objeto no Gerenciador de metadados Oracle. Objetos que têm problemas de conversão têm um ícone de erro vermelho.  
  
Para objetos que falharam na conversão, você pode exibir a sintaxe que resultou na falha de conversão.  
  
**Para exibir problemas de conversão individuais**  
  
1.  No Gerenciador de metadados Oracle, expanda **esquemas**.  
  
2.  Expanda o esquema que mostra um ícone de erro vermelho.  
  
3.  No esquema, expanda uma pasta que tem um ícone de erro vermelho.  
  
4.  Selecione o objeto que tem um ícone de erro vermelho.  
  
5.  No painel direito, clique na guia **relatório** .  
  
6.  Na parte superior da guia **relatório** está uma lista suspensa. Se a lista Mostrar **estatísticas**, altere a seleção para **origem**.  
  
    O SSMA exibirá o código-fonte e vários botões imediatamente acima do código.  
  
7.  Clique no botão **próximo problema** . Este é um ícone de erro vermelho com uma seta que aponta para a direita.  
  
    O SSMA irá destacar o primeiro código-fonte problemático encontrado no objeto atual.  
  
Para cada item que não pôde ser convertido, você precisa determinar o que deseja fazer com esse objeto:  
  
-   Você pode modificar o código-fonte para procedimentos na guia **SQL** .  
  
-   Você pode modificar o objeto no banco de dados Oracle para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você precisará atualizar os metadados. Para obter mais informações, consulte [conectando-se a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Você pode excluir o objeto da migração. No Gerenciador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados e no Gerenciador de metadados Oracle, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrar dados do Oracle.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [carregar os objetos convertidos em SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
