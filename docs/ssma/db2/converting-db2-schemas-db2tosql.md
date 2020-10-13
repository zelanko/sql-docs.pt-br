---
description: Convertendo esquemas do DB2 (DB2ToSQL)
title: Convertendo esquemas do DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b506f7ae063964bc1667b4425028cd35fbc9c91e
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985082"
---
# <a name="converting-db2-schemas-db2tosql"></a>Convertendo esquemas do DB2 (DB2ToSQL)
Depois de ter se conectado ao DB2, conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e defina as opções de projeto e mapeamento de dados, você pode converter objetos de banco de dado DB2 em objetos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="the-conversion-process"></a>O processo de conversão  
A conversão de objetos de banco de dados usa as definições de objeto do DB2, converte-as em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos semelhantes e, em seguida, carrega essas informações nos metadados do SSMA. Ele não carrega as informações na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Em seguida, você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados.  
  
Durante a conversão, o SSMA imprime as mensagens de saída no painel de saída e as mensagens de erro no painel de Lista de Erros. Use as informações de saída e erro para determinar se você precisa modificar seus bancos de dados DB2 ou seu processo de conversão para obter os resultados de conversão desejados.  
  
## <a name="setting-conversion-options"></a>Configurando opções de conversão  
Antes de converter objetos, examine as opções de conversão do projeto na caixa de diálogo **configurações do projeto** . Usando essa caixa de diálogo, você pode definir como o SSMA converte funções e variáveis globais. Para obter mais informações, consulte [configurações do projeto &#40;conversão&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
## <a name="conversion-results"></a>Resultados da conversão  
A tabela a seguir mostra quais objetos DB2 são convertidos e os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos resultantes:  
  
|Objetos DB2|Objetos SQL Server resultantes|  
|-----------|----------------------------|  
|Tipos de dados|**O SSMA mapeia todos os tipos, exceto os seguintes listados abaixo:**<br /><br />CLOB: não há suporte para algumas funções nativas para trabalhar com este tipo (por exemplo, CLOB_EMPTY ())<br /><br />BLOB: não há suporte para algumas funções nativas para trabalhar com esse tipo (por exemplo, BLOB_EMPTY ())<br /><br />DBLOB: não há suporte para algumas funções nativas para trabalhar com esse tipo (por exemplo, DBLOB_EMPTY ())|  
|Tipos definidos pelo usuário|**O SSMA mapeia o seguinte definido pelo usuário:**<br /><br />Tipo distinto<br /><br />Tipo estruturado<br /><br />Tipos de dados do SQL PL-Observação: não há suporte para o tipo de cursor fraco.|  
|Registros especiais|**O SSMA mapeia apenas os registros listados abaixo:**<br /><br />CARIMBO DE DATA/HORA ATUAL<br /><br />DATA ATUAL<br /><br />HORA ATUAL<br /><br />FUSO HORÁRIO ATUAL<br /><br />USUÁRIO ATUAL<br /><br />SESSION_USER e usuário<br /><br />SYSTEM_USER<br /><br />CLIENT_APPLNAME ATUAL<br /><br />CLIENT_WRKSTNNAME ATUAL<br /><br />TEMPO LIMITE DE BLOQUEIO ATUAL<br /><br />ESQUEMA ATUAL<br /><br />SERVIDOR ATUAL<br /><br />ISOLAMENTO ATUAL<br /><br />Outros registros especiais não são mapeados para a semântica do SQL Server.|  
|CREATE TABLE|**O SSMA Maps CREATE TABLE com as seguintes exceções:**<br /><br />Tabelas do MDC (multidimensional clustering)<br /><br />Intervalo de tabelas clusterizadas (RCT)<br /><br />Tabelas particionadas<br /><br />Tabela desanexada<br /><br />Cláusula de captura de dados<br /><br />Opção IMPLICITamente oculta<br /><br />Opção volátil|  
|CREATE VIEW|O SSMA Maps cria VIEW com ' WITH LOCAL CHECK OPTION ', mas outras opções não são mapeadas para a semântica do SQL Server|  
|CREATE INDEX|**O SSMA Maps cria um índice com as seguintes exceções:**<br /><br />Índice XML<br /><br />Opção BUSINESS_TIME sem sobreposições<br /><br />Cláusula PARTICIONAda<br /><br />Opção somente especificação<br /><br />ESTENDER usando opção<br /><br />Opção MINPCTUSED<br /><br />Opção de divisão de página|  
|Gatilhos|**O SSMA mapeia a seguinte semântica de gatilho:**<br /><br />Gatilhos AFTER/para cada linha<br /><br />APÓS o disparo de cada instrução<br /><br />ANTES/para cada linha e em vez de/para cada gatilho de linha|  
|Sequências|São mapeados.|  
|Instrução SELECT|**O SSMA Maps seleciona com as seguintes exceções:**<br /><br />Cláusula data-Change-Table-Reference-parcialmente mapeada, mas não há suporte para tabelas finais<br /><br />Cláusula de referência de tabela-parcialmente mapeada, mas somente-Table-Reference, referência de tabela externa, analyze_table-Expression, Collection-Derived-Table e Xmltable-Expression não são mapeados para a semântica do SQL Server<br /><br />Cláusula period-Specification-não mapeada.<br /><br />Cláusula do manipulador de continuação-não mapeada.<br /><br />Cláusula de correlação digitada-não mapeada.<br /><br />Cláusula de resolução de acesso simultâneo-não mapeada.|  
|Instrução VALUEs|É mapeado.|  
|Instrução INSERT|É mapeado.|  
|Instrução UPDATE|**Os mapas do SMA S são atualizados com as seguintes exceções:**<br /><br />Cláusula de referência de tabela-somente-a referência de tabela não está mapeada para a semântica do SQL Server<br /><br />A cláusula period-não está mapeada.|  
|Instrução MERGE|**A MESCLAgem do SSMA Maps com as seguintes exceções:**<br /><br />Ocorrências únicas e múltiplas de cada cláusula – é mapeada para a semântica do SQL Server para ocorrências limitadas de cada cláusula<br /><br />Cláusula de sinal – não mapeia para SQL Server semântica<br /><br />Cláusulas de atualização e exclusão mistas-não mapeia para SQL Server semântica<br /><br />Cláusula de período-não mapeia para SQL Server semântica|  
|Instrução DELETE|**O SSMA Maps é excluído com as seguintes exceções:**<br /><br />Cláusula de referência de tabela-somente-a referência de tabela não está mapeada para a semântica do SQL Server<br /><br />Cláusula de período-não mapeia para SQL Server semântica|  
|Nível de isolamento e tipo de bloqueio|É mapeado.|  
|Procedimentos (SQL)|São mapeados.|  
|Procedimentos (externos)|Exigir atualização manual.|  
|Procedimentos (originados)|Não mapeie para SQL Server semântica.|  
|Instrução de atribuição|É mapeado.|  
|Instrução de chamada para um procedimento|É mapeado.|  
|Instrução CASE|É mapeado.|  
|Instrução FOR|É mapeado.|  
|instrução GOTO|É mapeado.|  
|Instrução IF|É mapeado.|  
|Instrução de ITERAção|É mapeado.|  
|Instrução LEAVE|É mapeado.|  
|Instrução LOOP|É mapeado.|  
|Instrução REPEAT|É mapeado.|  
|Instrução de assinatura|Não há suporte para condições. As mensagens podem ser opcionais.|  
|Instrução de retorno|É mapeado.|  
|Instrução SIGNAL|Não há suporte para condições. As mensagens podem ser opcionais.|  
|Instrução WHILE|É mapeado.|  
|OBTER instrução de diagnóstico|**O SSMA Maps Obtém DIAGNÓSTICOs com as seguintes exceções:**<br /><br />ROW_COUNT-está mapeado.<br /><br />DB2_RETURN_STATUS-está mapeado.<br /><br />MESSAGE_TEXT-está mapeado.<br /><br />DB2_SQL_NESTING_LEVEL-não mapeia para SQL Server semântica<br /><br />DB2_TOKEN_STRING-não mapeia para SQL Server semântica|  
|Cursores|**CURSOres do SSMA Maps com as seguintes exceções:**<br /><br />Instrução ALLOCATE CURSOR-não mapeia para SQL Server semântica<br /><br />Instrução associar LOCALIZADOres-não mapeia para SQL Server semântica<br /><br />Instrução DECLARE CURSOR-a cláusula de retorno não está mapeada para a semântica do SQL Server<br /><br />Instrução FETCH-mapeamento parcial. Variáveis como destino têm suporte apenas. O DESCRITOr SQLDA não está mapeado para a semântica do SQL Server|  
|Variáveis|São mapeados.|  
|Exceções, manipuladores e condições|**O SSMA mapeia "manipulação de exceções" com as seguintes exceções:**<br /><br />Manipuladores de saída-são mapeados.<br /><br />Manipuladores de desfazer-são mapeados.<br /><br />CONTINUAR manipuladores-não estão mapeados.<br /><br />Condições-ele não é mapeado para a semântica do SQL Server.|  
|SQL dinâmico|Não mapeado.|  
|Aliases|São mapeados.|  
|Apelidos|Mapeamento parcial. O processamento manual é necessário para o objeto subjacente|  
|Sinônimos|São mapeados.|  
|Funções padrão no DB2|O SSMA mapeia as funções padrão do DB2 quando uma função equivalente está disponível no SQL Server:|  
|Authorization|Não mapeado.|  
|Predicados|São mapeados.|  
|instrução SELECT INTO|Não mapeado.|  
|VALORES em instrução|Não mapeado.|  
|Controle de transação|Não mapeado.|  
  
## <a name="converting-db2-database-objects"></a>Convertendo objetos de banco de dados DB2  
Para converter objetos de banco de dados DB2, primeiro selecione os objetos que deseja converter e, em seguida, faça com que o SSMA execute a conversão. Para exibir mensagens de saída durante a conversão, no menu **Exibir** , selecione **saída**.  
  
**Para converter objetos DB2 em sintaxe de SQL Server**  
  
1.  No Gerenciador de metadados do DB2, expanda o servidor DB2 e expanda **esquemas**.  
  
2.  Selecione os objetos a serem convertidos:  
  
    -   Para converter todos os esquemas, marque a caixa de seleção ao lado de **esquemas**.  
  
    -   Para converter ou omitir um banco de dados, marque a caixa de seleção ao lado do nome do esquema.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda um esquema e marque ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir objetos individuais, expanda a pasta categoria e marque ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com o botão direito do mouse em **esquemas** e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou em sua pasta pai e, em seguida, selecionando **converter esquema**.  
  
## <a name="viewing-conversion-problems"></a>Exibindo problemas de conversão  
Alguns objetos DB2 podem não ser convertidos. Você pode determinar as taxas de êxito da conversão exibindo o relatório de conversão de resumo.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do DB2, selecione **esquemas**.  
  
2.  No painel direito, selecione a guia **relatório** .  
  
    Este relatório mostra o relatório de avaliação de resumo para todos os objetos de banco de dados que foram avaliados ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório de um esquema individual, selecione o esquema no Gerenciador de metadados do DB2.  
  
    -   Para exibir o relatório de um objeto individual, selecione o objeto no Gerenciador de metadados do DB2. Objetos que têm problemas de conversão têm um ícone de erro vermelho.  
  
Para objetos que falharam na conversão, você pode exibir a sintaxe que resultou na falha de conversão.  
  
**Para exibir problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do DB2, expanda **esquemas**.  
  
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
  
-   Você pode modificar o objeto no banco de dados DB2 para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você precisará atualizar os metadados. Para obter mais informações, consulte [conectando ao banco de dados DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
-   Você pode excluir o objeto da migração. No Gerenciador de metadados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no Gerenciador de metadados DB2, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrar dados do DB2.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [carregar os objetos convertidos em SQL Server](./loading-converted-database-objects-into-sql-server-db2tosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Migrar dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
