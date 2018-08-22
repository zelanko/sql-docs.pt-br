---
title: Converter esquemas Oracle (OracleToSQL) | Microsoft Docs
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
ms.openlocfilehash: 277ad816d887a7f5641d8d37e7bdc60dc7ddb28a
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393793"
---
# <a name="converting-oracle-schemas-oracletosql"></a>Converter esquemas Oracle (OracleToSQL)
Depois de se conectar ao Oracle, conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e defina o projeto e as opções de mapeamento de dados, você pode converter objetos de banco de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de banco de dados.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto do Oracle, converte-os em semelhante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos e, em seguida, carrega essas informações nos metadados SSMA. Não carrega as informações para a instância da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em seguida, você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados.  
  
Durante a conversão, o SSMA imprime mensagens de saída para o painel de saída e mensagens de erro para o painel de lista de erros. Use as informações de erro e de saída para determinar se é preciso modificar seus bancos de dados Oracle ou o processo de conversão para obter os resultados da conversão desejada.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto na **configurações do projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte funções e variáveis globais. Para obter mais informações, consulte [configurações do projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
## <a name="conversion-results"></a>Resultados de conversão  
A tabela a seguir mostra quais objetos do Oracle são convertidos e resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos:  
  
|||  
|-|-|  
|Objetos do Oracle|Objetos do SQL Server resultantes|  
|Funções|Se a função pode ser convertida diretamente em [!INCLUDE[tsql](../../includes/tsql-md.md)], SSMA cria uma função.<br /><br />Em alguns casos, a função deve ser convertida em um procedimento armazenado. Nesse caso, o SSMA cria um procedimento armazenado e uma função que chama o procedimento armazenado.|  
|Procedimentos|Se o procedimento pode ser convertido diretamente em [!INCLUDE[tsql](../../includes/tsql-md.md)], SSMA cria um procedimento armazenado.<br /><br />Em alguns casos, um procedimento armazenado deve ser chamado em uma transação autônoma. Nesse caso, o SSMA cria dois procedimentos armazenados: uma que implementa o procedimento e outro que é usada para chamar a implementação de procedimento armazenado.|  
|Packages|O SSMA cria um conjunto de procedimentos armazenados e funções que são unificadas por nomes de objeto semelhantes.|  
|Sequências|O SSMA cria objetos de sequência (SQL Server 2012 ou SQL Server 2014) ou emula sequências da Oracle.|  
|Tabelas com objetos dependentes, como índices e disparadores|O SSMA cria tabelas com objetos dependentes.|  
|Exibir com objetos dependentes, como gatilhos|O SSMA cria exibições com objetos dependentes.|  
|Exibições materializadas|**O SSMA cria exibições indexadas no SQL server com algumas exceções. Conversão falhará se a exibição materializada inclui um ou mais das construções a seguir:**<br /><br />Função definida pelo usuário<br /><br />Campo não determinístico de função / expressão no, selecione onde ou cláusulas GROUP BY<br /><br />Uso de coluna Float em SELECT *, onde ou cláusulas GROUP BY (caso especial de edição anterior)<br /><br />Tipo de dados personalizados (tabelas aninhadas de incl.)<br /><br />COUNT (distinct &lt;campo&gt;)<br /><br />FETCH<br /><br />junções OUTER (LEFT, RIGHT ou FULL)<br /><br />Subconsulta, outro modo de exibição<br /><br />ACIMA, CLASSIFICAR, CLIENTE POTENCIAL, FAÇA LOGON<br /><br />MIN, MAX<br /><br />UNION, SUBTRAÇÃO, SE CRUZAM<br /><br />HAVING|  
|Gatilho|**O SSMA cria gatilhos com base nas seguintes regras:**<br /><br />ANTES dos gatilhos são convertidos em gatilhos INSTEAD OF.<br /><br />Gatilhos AFTER são convertidos em gatilhos AFTER.<br /><br />Os gatilhos INSTEAD OF são convertidos em gatilhos INSTEAD OF. Vários gatilhos INSTEAD OF definidos na mesma operação são combinados em um gatilho.<br /><br />Gatilhos de nível de linha são emulados usando cursores.<br /><br />Gatilhos em cascata são convertidos em vários disparadores individuais.|  
|Sinônimos|**Sinônimos são criados para os seguintes tipos de objeto:**<br /><br />Tabelas e tabelas de objeto<br /><br />Modos de exibição e objeto<br /><br />Procedimentos armazenados<br /><br />Funções<br /><br />**Sinônimos para os seguintes objetos são resolvidos e substituídos por referências de objeto:**<br /><br />Sequências<br /><br />Packages<br /><br />Objetos de esquema de classe de Java<br /><br />Tipos de objeto definido pelo usuário<br /><br />Sinônimos de outro sinônimo não podem ser migrados e serão marcados como erros.<br /><br />Sinônimos não são criados para Materialized modos de exibição.|  
|Tipos definidos pelo usuário|**O SSMA fornece suporte para a conversão de tipos definidos pelo usuário. Tipos definidos pelo usuário, incluindo seu uso em programas de PL/SQL são marcados com erros de conversão especial guiados pelas seguintes regras:**<br /><br />Coluna da tabela de um tipo definido pelo usuário é convertida em VARCHAR(8000).<br /><br />Tipo definido pelo argumento do usuário para um procedimento armazenado ou função é convertida em VARCHAR(8000).<br /><br />Variável do tipo definido pelo usuário no bloco de PL/SQL é convertido em VARCHAR(8000).<br /><br />Tabela de objeto é convertida em uma tabela padrão.<br /><br />Exibição do objeto é convertida em uma exibição padrão.|  
  
## <a name="converting-oracle-database-objects"></a>Converter objetos de banco de dados Oracle  
Para converter objetos de banco de dados Oracle, primeiro selecione os objetos que você deseja converter e, em seguida, ter o SSMA realizar a conversão. Para exibir mensagens de saída durante a conversão na **modo de exibição** menu, selecione **saída**.  
  
**Para converter objetos Oracle em sintaxe do SQL Server**  
  
1.  No Gerenciador de metadados do Oracle, expanda o servidor Oracle e, em seguida, expanda **esquemas**.  
  
2.  Selecione objetos a ser convertida:  
  
    -   Para converter todos os esquemas, selecione a caixa de seleção ao lado **esquemas**.  
  
    -   Para converter ou omitir um banco de dados, marque a caixa de seleção ao lado do nome do esquema.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda um esquema e, em seguida, selecione ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir os objetos individuais, expanda a pasta de categoria e, em seguida, selecione ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com botão direito **esquemas** e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou as categorias de objetos, clicando duas vezes o objeto ou a pasta pai e, em seguida, selecionando **converter esquema**.  
  
## <a name="viewing-conversion-problems"></a>Problemas de conversão de exibição  
Alguns objetos do Oracle não podem ser convertidos. Você pode determinar as taxas de sucesso de conversão, exibindo o relatório de resumo de conversão.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do Oracle, selecione **esquemas**.  
  
2.  No painel direito, selecione a **relatório** guia.  
  
    Este relatório mostra o relatório de resumo de avaliação para todos os objetos de banco de dados que foram avaliados ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório para um esquema individual, selecione o esquema no Gerenciador de metadados do Oracle.  
  
    -   Para exibir o relatório para um objeto individual, selecione o objeto no Gerenciador de metadados do Oracle. Objetos que têm problemas de conversão têm um ícone vermelho de erro.  
  
Para objetos que falha na conversão, você pode exibir a sintaxe que resultou em falha de conversão.  
  
**Para exibir os problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do Oracle, expanda **esquemas**.  
  
2.  Expanda o esquema que mostra um ícone vermelho de erro.  
  
3.  Sob o esquema, expanda uma pasta que tem um ícone vermelho de erro.  
  
4.  Selecione o objeto que tem um ícone vermelho de erro.  
  
5.  No painel direito, clique no **relatório** guia.  
  
6.  Na parte superior do **relatório** guia é uma lista suspensa. Se a lista mostra **estatísticas**, altere a seleção **origem**.  
  
    O SSMA exibirá o código-fonte e vários botões imediatamente acima do código.  
  
7.  Clique o **próximo problema** botão. Isso é um ícone vermelho de erro com uma seta que aponta para a direita.  
  
    O SSMA realçará o código-fonte problemático primeiro que ele localiza no objeto atual.  
  
Para cada item que não pôde ser convertido, você deve determinar o que você deseja fazer com esse objeto:  
  
-   Você pode modificar o código-fonte para obter procedimentos sobre o **SQL** guia.  
  
-   Você pode modificar o objeto no banco de dados Oracle para remover ou revisar código problemático. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [conectar-se ao banco de dados Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Você pode excluir o objeto da migração. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e o Gerenciador de metadados do Oracle, desmarque a caixa de seleção próxima ao item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migração de dados do Oracle.  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no processo de migração [carregar objetos convertidos no SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando do Oracle bancos de dados para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
