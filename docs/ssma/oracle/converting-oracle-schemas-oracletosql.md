---
title: Convertendo esquemas Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: bf41da767d5e11b439a919668fb6d16d8cb6aec7
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777202"
---
# <a name="converting-oracle-schemas-oracletosql"></a>Convertendo esquemas Oracle (OracleToSQL)
Depois de se conectar ao Oracle, conectado à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], e o conjunto de projeto e as opções de mapeamento de dados, você pode converter objetos de banco de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos de banco de dados.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto do Oracle, converte-os em semelhante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos e, em seguida, carrega essas informações para os metadados do SSMA. Não carrega as informações para a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados.  
  
Durante a conversão, o SSMA imprime mensagens de saída para o painel de saída e mensagens de erro para o painel de lista de erros. Use as informações de saída e de erro para determinar se você precisa modificar seus bancos de dados Oracle ou o processo de conversão para obter os resultados da conversão desejada.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto no **configurações de projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte funções e variáveis globais. Para obter mais informações, consulte [configurações de projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
## <a name="conversion-results"></a>Resultados de conversão  
A tabela a seguir mostra quais objetos do Oracle são convertidos e resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos:  
  
|||  
|-|-|  
|Objetos de Oracle|Objetos resultantes do SQL Server|  
|Funções|Se a função pode ser convertida diretamente em [!INCLUDE[tsql](../../includes/tsql_md.md)], SSMA cria uma função.<br /><br />Em alguns casos, a função deve ser convertida em um procedimento armazenado. Nesse caso, o SSMA cria um procedimento armazenado e uma função que chama o procedimento armazenado.|  
|Procedimentos|Se o procedimento pode ser convertido diretamente em [!INCLUDE[tsql](../../includes/tsql_md.md)], SSMA cria um procedimento armazenado.<br /><br />Em alguns casos, um procedimento armazenado deve ser chamado em uma transação autônoma. Nesse caso, o SSMA cria dois procedimentos armazenados: um que implementa o procedimento e outro que é usado para chamar a implementação do procedimento armazenado.|  
|Packages|O SSMA cria um conjunto de procedimentos armazenados e funções que são unificadas de nomes de objeto semelhantes.|  
|Sequências|O SSMA cria objetos de sequência (SQL Server 2012 ou SQL Server 2014) ou emula sequências da Oracle.|  
|Tabelas com objetos dependentes, como índices e gatilhos|O SSMA cria tabelas com objetos dependentes.|  
|Exibir com objetos dependentes, como gatilhos|O SSMA cria exibições com os objetos dependentes.|  
|Exibições materializadas|**O SSMA cria exibições indexadas no SQL server com algumas exceções. Conversão falhará se a exibição materializada inclui um ou mais das seguintes construções:**<br /><br />Função definida pelo usuário<br /><br />Campo não determinístico / função / expressão no, selecione onde ou cláusulas GROUP BY<br /><br />Uso da coluna de Float em SELECT *, onde ou cláusulas GROUP BY (caso especial de edição anterior)<br /><br />Tipo de dados personalizados (incluindo aninhados tabelas)<br /><br />CONTAGEM (distinta &lt;campo&gt;)<br /><br />FETCH<br /><br />junções OUTER (LEFT, RIGHT ou FULL)<br /><br />Subconsulta, outro modo de exibição<br /><br />EM, CLASSIFICAÇÃO, CLIENTE POTENCIAL, DE LOG<br /><br />MIN, MAX<br /><br />UNION, SUBTRAÇÃO, INTERSEÇÃO<br /><br />HAVING|  
|Gatilho|**O SSMA cria gatilhos com base nas seguintes regras:**<br /><br />ANTES dos gatilhos são convertidos em gatilhos INSTEAD OF.<br /><br />Depois que os gatilhos são convertidos em gatilhos AFTER.<br /><br />Os gatilhos INSTEAD OF são convertidos em gatilhos INSTEAD OF. Vários gatilhos INSTEAD OF definidos na mesma operação são combinados em um disparador.<br /><br />Gatilhos de nível de linha são emulados usar cursores.<br /><br />Os gatilhos em cascata são convertidos em vários disparadores individuais.|  
|Sinônimos|**Sinônimos são criados para os seguintes tipos de objeto:**<br /><br />Tabelas e tabelas de objeto<br /><br />Modos de exibição e objeto<br /><br />Procedimentos armazenados<br /><br />Funções<br /><br />**Sinônimos para os seguintes objetos são resolvidos e substituídos por referências diretas de objeto:**<br /><br />Sequências<br /><br />Packages<br /><br />Objetos de esquema de classe Java<br /><br />Tipos de objeto definido pelo usuário<br /><br />Sinônimos de outro sinônimo não podem ser migrados e serão marcados como erros.<br /><br />Sinônimos não são criados para Materialized exibições.|  
|Tipos definidos pelo usuário|**O SSMA não dá suporte para conversão de tipos definidos pelo usuário. Tipos definidos pelo usuário, incluindo seu uso em programas de PL/SQL são marcados com erros de conversão especial interativa pelas seguintes regras:**<br /><br />Coluna da tabela de um tipo definido pelo usuário é convertida em VARCHAR(8000).<br /><br />Tipo definido pelo argumento de usuário para um procedimento armazenado ou função é convertida em VARCHAR(8000).<br /><br />Variável de tipo definido pelo usuário no bloco de PL/SQL é convertido em VARCHAR(8000).<br /><br />Tabela de objeto é convertida em uma tabela padrão.<br /><br />Exibição do objeto é convertida em um modo de exibição padrão.|  
  
## <a name="converting-oracle-database-objects"></a>Converter objetos de banco de dados Oracle  
Para converter objetos de banco de dados Oracle, você primeiro selecionar os objetos que você deseja converter e, em seguida, SSMA executar a conversão. Para exibir mensagens de saída durante a conversão no **exibição** menu, selecione **saída**.  
  
**Para converter objetos Oracle em sintaxe de SQL Server**  
  
1.  No Gerenciador de metadados do Oracle, expanda o servidor Oracle e, em seguida, expanda **esquemas**.  
  
2.  Selecione objetos para converter:  
  
    -   Para converter todos os esquemas, selecione a caixa de seleção ao lado de **esquemas**.  
  
    -   Para converter ou omitir um banco de dados, marque a caixa de seleção ao lado do nome do esquema.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda um esquema e, em seguida, marque ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir os objetos individuais, expanda a pasta de categoria e, em seguida, marque ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com botão direito **esquemas** e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou as categorias de objetos, clicando duas vezes o objeto ou a pasta pai e, em seguida, selecionando **converter esquema**.  
  
## <a name="viewing-conversion-problems"></a>Problemas de conversão de exibição  
Alguns objetos do Oracle não podem ser convertidos. Você pode determinar as taxas de sucesso de conversão exibindo o relatório de resumo de conversão.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do Oracle, selecione **esquemas**.  
  
2.  No painel direito, selecione o **relatório** guia.  
  
    Este relatório mostra o relatório de resumo de avaliação para todos os objetos de banco de dados que tenham sido avaliada ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório para um esquema individual, selecione o esquema no Gerenciador de metadados do Oracle.  
  
    -   Para exibir o relatório para um objeto individual, selecione o objeto no Gerenciador de metadados do Oracle. Objetos que têm problemas de conversão têm um ícone de erro vermelho.  
  
Para objetos que falha na conversão, você pode exibir a sintaxe que resultaram em falha de conversão.  
  
**Para exibir os problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do Oracle, expanda **esquemas**.  
  
2.  Expanda o esquema que mostra um ícone de erro vermelho.  
  
3.  No esquema, expanda uma pasta que tem um ícone de erro vermelho.  
  
4.  Selecione o objeto que tem um ícone de erro vermelho.  
  
5.  No painel direito, clique no **relatório** guia.  
  
6.  Na parte superior do **relatório** guia é uma lista suspensa. Se a lista mostra **estatísticas**, altere a seleção do **fonte**.  
  
    O SSMA exibirá o código-fonte e vários botões imediatamente acima do código.  
  
7.  Clique o **próximo problema** botão. Este é um ícone de erro vermelho com uma seta que aponta para a direita.  
  
    O SSMA realçará o código-fonte problemático primeiro localiza no objeto atual.  
  
Para cada item que não puderam ser convertido, você deve determinar o que você deseja fazer com esse objeto:  
  
-   Você pode modificar o código-fonte para obter os procedimentos sobre o **SQL** guia.  
  
-   Você pode modificar o objeto no banco de dados Oracle para remover ou revisar código problemática. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [se conectar ao banco de dados Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Você pode excluir o objeto de migração. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados e o Gerenciador de metadados do Oracle, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e migração de dados do Oracle.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [carregar objetos convertidos no SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a).  
  
## <a name="see-also"></a>Consulte também  
[Bancos de dados Oracle migrando para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
