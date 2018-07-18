---
title: Converter esquemas do DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d6c63b66a52f0fbc6a676a2143299b7ee5b13208
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980698"
---
# <a name="converting-db2-schemas-db2tosql"></a>Converter esquemas do DB2 (DB2ToSQL)
Depois de se conectar ao DB2, conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], e defina o projeto e as opções de mapeamento de dados, você pode converter objetos de banco de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos de banco de dados.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto do DB2, converte-os em semelhante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos e, em seguida, carrega essas informações nos metadados SSMA. Não carrega as informações para a instância da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Em seguida, você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados.  
  
Durante a conversão, o SSMA imprime mensagens de saída para o painel de saída e mensagens de erro para o painel de lista de erros. Use as informações de erro e de saída para determinar se é preciso modificar seus bancos de dados do DB2 ou o processo de conversão para obter os resultados da conversão desejada.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto na **configurações do projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte funções e variáveis globais. Para obter mais informações, consulte [configurações do projeto &#40;conversão&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
## <a name="conversion-results"></a>Resultados de conversão  
A tabela a seguir mostra quais objetos do DB2 são convertidos e resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos:  
  
|Objetos do DB2|Objetos do SQL Server resultantes|  
|-----------|----------------------------|  
|Tipos de dados|**O SSMA mapeia cada tipo, exceto o seguinte listado abaixo:**<br /><br />CLOB: Algumas funções nativas para o trabalho com esse tipo não são suportados (por exemplo, CLOB_EMPTY())<br /><br />BLOB: Algumas funções nativas para o trabalho com esse tipo não são suportados (por exemplo, BLOB_EMPTY())<br /><br />DBLOB: Algumas funções nativas para o trabalho com esse tipo não são suportados (por exemplo, DBLOB_EMPTY())|  
|Tipos definidos pelo usuário|**O SSMA mapeia a seguir definida pelo usuário:**<br /><br />Tipo distinto<br /><br />Tipo estruturado<br /><br />Tipos de dados SQL PL – Observação: não há suporte para o tipo de cursor fraco.|  
|Registradores especiais|**O SSMA mapeia apenas registros listados abaixo:**<br /><br />CARIMBO DE HORA ATUAL<br /><br />DATA ATUAL<br /><br />HORA ATUAL<br /><br />FUSO HORÁRIO ATUAL<br /><br />USUÁRIO ATUAL<br /><br />SESSION_USER e usuário<br /><br />SYSTEM_USER<br /><br />CLIENT_APPLNAME ATUAL<br /><br />CLIENT_WRKSTNNAME ATUAL<br /><br />TEMPO LIMITE DE BLOQUEIO ATUAL<br /><br />ESQUEMA ATUAL<br /><br />SERVIDOR ATUAL<br /><br />ISOLAMENTO ATUAL<br /><br />Outros registra especiais não é mapeado para a semântica do SQL server.|  
|CREATE TABLE|**O SSMA mapeia CREATE TABLE com as seguintes exceções:**<br /><br />Tabelas de clustering (MDC) multidimensional<br /><br />Tabelas de intervalo clusterizado (RCT)<br /><br />Tabelas particionadas<br /><br />Tabela desanexada<br /><br />Cláusula de captura de dados<br /><br />Opção IMPLICITLY oculto<br /><br />Opção VOLATILE|  
|CREATE VIEW|O SSMA mapeia CREATE VIEW com 'Com LOCAL CHECK OPTION', mas outras opções não são mapeadas para a semântica do SQL server|  
|CREATE INDEX|**O SSMA mapeia CREATE INDEX com as seguintes exceções:**<br /><br />Índice XML<br /><br />Opção BUSINESS_TIME sem SOBREPOSIÇÕES<br /><br />Cláusula PARTICIONADA<br /><br />ESPECIFICAÇÃO apenas de opção<br /><br />Opção usando EXTEND<br /><br />Opção MINPCTUSED<br /><br />Opção de divisão de página|  
|Gatilhos|**O SSMA mapeia a semântica de gatilho a seguir:**<br /><br />APÓS / linha EACH GATILHOS<br /><br />Depois de /FOR dispara a cada instrução<br /><br />ANTES de / para EACH linha e, em vez de / para a linha EACH gatilhos|  
|Sequências|São mapeados.|  
|Instrução SELECT|**Selecione o SSMA mapas com as seguintes exceções:**<br /><br />Cláusula de dados-alteração de tabela de referência – parcialmente mapeado, mas tabelas FINAL faz sem suporte<br /><br />Cláusula de referência de tabela – parcialmente mapeados, mas somente--referência de tabela, a referência de tabela externa, analyze_table-expression, tabela derivada coleção, expressão xmltable não são mapeados para a semântica do SQL server<br /><br />Cláusula de especificação de período – não mapeada.<br /><br />Cláusula de manipulador continuar – não mapeada.<br /><br />Cláusula de correlação digitado – não mapeada.<br /><br />Cláusula de resolução simultânea da acesso – não mapeada.|  
|Instrução de valores|É mapeado.|  
|Instrução INSERT|É mapeado.|  
|Instrução UPDATE|S**SMA mapas de atualização com as seguintes exceções:**<br /><br />Cláusula de referência de tabela – somente--referência de tabela não está mapeada para a semântica do SQL server<br /><br />Cláusula Períoda – não está mapeado.|  
|Instrução MERGE|**O SSMA mapeia direta com as seguintes exceções:**<br /><br />Único versus várias ocorrências de cada cláusula – é mapeado para a semântica do SQL server para as ocorrências de cada cláusula limitadas<br /><br />Cláusula de sinal – não é mapeado para a semântica do SQL Server<br /><br />Misto atualizar e excluir cláusulas – não é mapeado para a semântica do SQL Server<br /><br />Cláusula de período – não é mapeado para a semântica do SQL Server|  
|Instrução DELETE|**Excluir SSMA mapas com as seguintes exceções:**<br /><br />Cláusula de referência de tabela – somente--referência de tabela não está mapeada para a semântica do SQL server<br /><br />Cláusula Períoda – não é mapeado para a semântica do SQL Server|  
|Nível de isolamento e o tipo de bloqueio|É mapeado.|  
|Procedimentos (SQL)|São mapeados.|  
|Procedimentos (externo)|Exigir atualização manual.|  
|Procedimentos (originados)|Não mapeie a semântica do SQL Server.|  
|Instrução de atribuição|É mapeado.|  
|Instrução de chamada para um procedimento|É mapeado.|  
|Instrução CASE|É mapeado.|  
|Instrução FOR|É mapeado.|  
|instrução GOTO|É mapeado.|  
|Instrução IF|É mapeado.|  
|Instrução de ITERAÇÃO|É mapeado.|  
|Deixe a instrução|É mapeado.|  
|Instrução de LOOP|É mapeado.|  
|REPITA a instrução|É mapeado.|  
|RESIGNAL instrução|Não há suporte para condições. As mensagens podem ser opcionais.|  
|Instrução RETURN|É mapeado.|  
|Instrução de sinal|Não há suporte para condições. As mensagens podem ser opcionais.|  
|Instrução WHILE|É mapeado.|  
|OBTER o demonstrativo de diagnóstico|**O SSMA mapeia obter diagnóstico com as seguintes exceções:**<br /><br />ROW_COUNT – é mapeado.<br /><br />DB2_RETURN_STATUS – é mapeado.<br /><br />MESSAGE_TEXT – é mapeado.<br /><br />DB2_SQL_NESTING_LEVEL - não é mapeado para a semântica do SQL Server<br /><br />DB2_TOKEN_STRING - não é mapeado para a semântica do SQL Server|  
|Cursores|**O SSMA mapeia CURSORES com as seguintes exceções:**<br /><br />Instrução de CURSOR ALLOCATE - não é mapeado para a semântica do SQL Server<br /><br />Instrução de LOCALIZADORES ASSOCIAR - não é mapeado para a semântica do SQL Server<br /><br />Instrução DECLARE CURSOR - cláusula Returnability não está mapeada para a semântica do SQL server<br /><br />Instrução FETCH – mapeamento parcial. Variáveis como destino têm suporte apenas. DESCRITOR de SQLDA não está mapeado para a semântica do SQL server|  
|Variáveis|São mapeados.|  
|Exceções, manipuladores e condições|**O SSMA mapeia "tratamento de exceção" com as seguintes exceções:**<br /><br />Manipuladores de saída – são mapeados.<br /><br />Desfazer manipuladores – são mapeados.<br /><br />CONTINUAR manipuladores – não são mapeados.<br /><br />Condições - ele não é mapeado para a semântica do SQL server.|  
|SQL dinâmico|Não mapeado.|  
|Aliases|São mapeados.|  
|Apelidos|Mapeamento parcial. Processamento manual é necessário para o objeto subjacente|  
|Sinônimos|São mapeados.|  
|Funções padrão no DB2|O SSMA mapeia as funções padrão de DB2 quando uma função equivalente está disponível no SQL Server:|  
|Autorização|Não mapeado.|  
|Predicados|São mapeados.|  
|instrução SELECT INTO|Não mapeado.|  
|Instrução de valores em|Não mapeado.|  
|Controle de transações|Não mapeado.|  
  
## <a name="converting-db2-database-objects"></a>Converter objetos de banco de dados do DB2  
Para converter objetos de banco de dados do DB2, primeiro selecione os objetos que você deseja converter e, em seguida, ter o SSMA realizar a conversão. Para exibir mensagens de saída durante a conversão na **modo de exibição** menu, selecione **saída**.  
  
**Para converter objetos de DB2 em sintaxe do SQL Server**  
  
1.  No Gerenciador de metadados do DB2, expanda o servidor do DB2 e, em seguida, expanda **esquemas**.  
  
2.  Selecione objetos a ser convertida:  
  
    -   Para converter todos os esquemas, selecione a caixa de seleção ao lado **esquemas**.  
  
    -   Para converter ou omitir um banco de dados, marque a caixa de seleção ao lado do nome do esquema.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda um esquema e, em seguida, selecione ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir os objetos individuais, expanda a pasta de categoria e, em seguida, selecione ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com botão direito **esquemas** e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou as categorias de objetos, clicando duas vezes o objeto ou a pasta pai e, em seguida, selecionando **converter esquema**.  
  
## <a name="viewing-conversion-problems"></a>Problemas de conversão de exibição  
Alguns objetos do DB2 podem não ser convertidos. Você pode determinar as taxas de sucesso de conversão, exibindo o relatório de resumo de conversão.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do DB2, selecione **esquemas**.  
  
2.  No painel direito, selecione a **relatório** guia.  
  
    Este relatório mostra o relatório de resumo de avaliação para todos os objetos de banco de dados que foram avaliados ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório para um esquema individual, selecione o esquema no Gerenciador de metadados do DB2.  
  
    -   Para exibir o relatório para um objeto individual, selecione o objeto no Gerenciador de metadados do DB2. Objetos que têm problemas de conversão têm um ícone vermelho de erro.  
  
Para objetos que falha na conversão, você pode exibir a sintaxe que resultou em falha de conversão.  
  
**Para exibir os problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do DB2, expanda **esquemas**.  
  
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
  
-   Você pode modificar o objeto no banco de dados DB2 para remover ou revisar código problemático. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [conectar-se ao banco de dados DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
-   Você pode excluir o objeto da migração. Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados e o Gerenciador de metadados do DB2, desmarque a caixa de seleção próxima ao item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e migração de dados do DB2.  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no processo de migração [carregar objetos convertidos no SQL Server](http://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
## <a name="see-also"></a>Consulte também  
[Migrando dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
