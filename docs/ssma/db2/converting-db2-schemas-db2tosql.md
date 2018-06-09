---
title: Convertendo esquemas de DB2 (DB2ToSQL) | Microsoft Docs
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
ms.openlocfilehash: b7d16e10ec2dfb3474679f63aff9941bd2ef84a8
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774492"
---
# <a name="converting-db2-schemas-db2tosql"></a>Convertendo esquemas de DB2 (DB2ToSQL)
Depois de se conectar ao DB2, conectado à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], e o conjunto de projeto e as opções de mapeamento de dados, você pode converter objetos de banco de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos de banco de dados.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto do DB2, converte-os em semelhante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos e, em seguida, carrega essas informações para os metadados do SSMA. Não carrega as informações para a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados.  
  
Durante a conversão, o SSMA imprime mensagens de saída para o painel de saída e mensagens de erro para o painel de lista de erros. Use as informações de saída e de erro para determinar se você precisa modificar seus bancos de dados do DB2 ou o processo de conversão para obter os resultados da conversão desejada.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto no **configurações de projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte funções e variáveis globais. Para obter mais informações, consulte [configurações de projeto &#40;conversão&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
## <a name="conversion-results"></a>Resultados de conversão  
A tabela a seguir mostra quais objetos do DB2 são convertidos e resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos:  
  
|Objetos do DB2|Objetos resultantes do SQL Server|  
|-----------|----------------------------|  
|Tipos de dados|**O SSMA mapeia cada tipo, exceto o seguinte listado abaixo:**<br /><br />CLOB: Algumas funções nativas para trabalhar com esse tipo não são suportados (por exemplo, CLOB_EMPTY())<br /><br />BLOB: Algumas funções nativas para trabalhar com esse tipo não são suportados (por exemplo, BLOB_EMPTY())<br /><br />DBLOB: Algumas funções nativas para trabalhar com esse tipo não são suportados (por exemplo, DBLOB_EMPTY())|  
|Tipos definidos pelo usuário|**O SSMA mapeia a seguir definida pelo usuário:**<br /><br />Tipo distinto<br /><br />Tipo estruturado<br /><br />Tipos de dados SQL PL – Observação: não há suporte para o tipo de cursor fraca.|  
|Registra especiais|**O SSMA mapeia apenas registros listados abaixo:**<br /><br />CARIMBO DE HORA ATUAL<br /><br />DATA ATUAL<br /><br />HORA ATUAL<br /><br />FUSO HORÁRIO ATUAL<br /><br />USUÁRIO ATUAL<br /><br />SESSION_USER e do usuário<br /><br />SYSTEM_USER<br /><br />CLIENT_APPLNAME ATUAL<br /><br />CLIENT_WRKSTNNAME ATUAL<br /><br />TEMPO LIMITE DE BLOQUEIO ATUAL<br /><br />ESQUEMA ATUAL<br /><br />SERVIDOR ATUAL<br /><br />ISOLAMENTO ATUAL<br /><br />Outros registra especiais não é mapeada para a semântica do SQL server.|  
|CREATE TABLE|**O SSMA mapeia CREATE TABLE com as seguintes exceções:**<br /><br />Tabelas de clustering (MDC) multidimensionais<br /><br />Tabelas de intervalo clusterizados (RCT)<br /><br />Tabelas particionadas<br /><br />Tabela desanexada<br /><br />Cláusula de captura de dados<br /><br />Opção IMPLICITLY oculto<br /><br />Opção /VOLATILE|  
|CREATE VIEW|O SSMA mapeia CREATE VIEW com 'WITH LOCAL CHECK OPTION', mas outras opções não estão mapeadas para a semântica do SQL server|  
|CREATE INDEX|**O SSMA mapeia CREATE INDEX com as seguintes exceções:**<br /><br />Índice XML<br /><br />Opção BUSINESS_TIME sem SOBREPOSIÇÕES<br /><br />Cláusula PARTICIONADA<br /><br />Opção de especificação somente<br /><br />Opção usando EXTEND<br /><br />Opção MINPCTUSED<br /><br />Opção de divisão de página|  
|Gatilhos|**O SSMA mapeia a semântica de gatilho a seguir:**<br /><br />Depois / linha EACH GATILHOS<br /><br />Depois de /FOR cada instrução gatilhos<br /><br />ANTES de / para EACH linha e, em vez de / para gatilhos EACH linhas|  
|Sequências|São mapeados.|  
|Instrução SELECT|**Selecione o SSMA mapas com as seguintes exceções:**<br /><br />Cláusula de dados-alteração de tabela de referência – parcialmente mapeado, mas as tabelas FINAL não tem suporte<br /><br />Cláusula de referência de tabela – parcialmente mapeada, mas somente--referência de tabela, a referência de tabela externa, analyze_table-expression, tabela derivada coleção, expressão xmltable não são mapeadas para a semântica do SQL server<br /><br />Cláusula de especificação de período – não mapeada.<br /><br />Cláusula de manipulador continuar – não mapeada.<br /><br />Cláusula de correlação digitado – não mapeada.<br /><br />Resolução de acesso simultâneo a cláusula – não mapeada.|  
|Instrução de valores|Está mapeada.|  
|Instrução INSERT|Está mapeada.|  
|Instrução UPDATE|S**SMA mapeia atualização com as seguintes exceções:**<br /><br />Cláusula de referência de tabela – somente--referência de tabela não está mapeada para a semântica do SQL server<br /><br />Cláusula Períoda – não está mapeado.|  
|Instrução MERGE|**O SSMA mapeia a mesclagem com as seguintes exceções:**<br /><br />Único versus várias ocorrências de cada cláusula - é mapeado para a semântica do SQL server para ocorrências limitadas de cada cláusula<br /><br />Cláusula de sinal – não é mapeado para a semântica do SQL Server<br /><br />Misto atualizar e excluir cláusulas – não é mapeado para a semântica do SQL Server<br /><br />Cláusula de período – não é mapeado para a semântica do SQL Server|  
|Instrução DELETE|**Excluir SSMA mapas com as seguintes exceções:**<br /><br />Cláusula de referência de tabela – somente--referência de tabela não está mapeada para a semântica do SQL server<br /><br />Cláusula Períoda – não é mapeado para a semântica do SQL Server|  
|Nível de isolamento e tipo de bloqueio|Está mapeada.|  
|Procedimentos (SQL)|São mapeados.|  
|Procedimentos (externo)|Exigem a atualização manual.|  
|Procedimentos (originados)|Não mapeie a semântica do SQL Server.|  
|Instrução de atribuição|Está mapeada.|  
|Instrução de chamada para um procedimento|Está mapeada.|  
|Instrução CASE|Está mapeada.|  
|Instrução FOR|Está mapeada.|  
|instrução GOTO|Está mapeada.|  
|Instrução IF|Está mapeada.|  
|Instrução de ITERAÇÃO|Está mapeada.|  
|Deixe a instrução|Está mapeada.|  
|Instrução de LOOP|Está mapeada.|  
|REPITA a instrução|Está mapeada.|  
|RESIGNAL instrução|Não há suporte para condições. Mensagens podem ser opcionais.|  
|Instrução RETURN|Está mapeada.|  
|Instrução de sinal|Não há suporte para condições. Mensagens podem ser opcionais.|  
|Instrução WHILE|Está mapeada.|  
|DIAGNÓSTICO instrução GET|**O SSMA mapeia obter diagnósticos com as seguintes exceções:**<br /><br />ROW_COUNT – é mapeado.<br /><br />DB2_RETURN_STATUS – é mapeado.<br /><br />MESSAGE_TEXT – é mapeado.<br /><br />DB2_SQL_NESTING_LEVEL - não é mapeado para a semântica do SQL Server<br /><br />DB2_TOKEN_STRING - não é mapeado para a semântica do SQL Server|  
|Cursores|**O SSMA mapeia CURSORES com as seguintes exceções:**<br /><br />Instrução de CURSOR ALLOCATE - não é mapeado para a semântica do SQL Server<br /><br />Instrução de LOCALIZADORES ASSOCIAR - não é mapeado para a semântica do SQL Server<br /><br />Instrução DECLARE CURSOR - cláusula Returnability não está mapeada para a semântica do SQL server<br /><br />Instrução FETCH – um mapeamento parcial. Variáveis como destino têm suporte apenas. DESCRITOR de sqlda não não está mapeada para a semântica do SQL server|  
|Variáveis|São mapeados.|  
|Exceções, manipuladores e condições|**O SSMA mapeia "tratamento de exceção" com as seguintes exceções:**<br /><br />Manipuladores de saída – são mapeados.<br /><br />Desfazer manipuladores – são mapeados.<br /><br />CONTINUAR manipuladores – não estão mapeados.<br /><br />Condições - ele não mapeia a semântica do SQL server.|  
|SQL dinâmico|Não mapeado.|  
|Aliases|São mapeados.|  
|Apelidos|Mapeamento parcial. Processamento manual é necessário para o objeto subjacente|  
|Sinônimos|São mapeados.|  
|Funções padrão no DB2|O SSMA mapeia as funções padrão do DB2 quando uma função equivalente está disponível no SQL Server:|  
|Autorização|Não mapeado.|  
|Predicados|São mapeados.|  
|instrução SELECT INTO|Não mapeado.|  
|Os valores na instrução|Não mapeado.|  
|Controle de transação|Não mapeado.|  
  
## <a name="converting-db2-database-objects"></a>Converter objetos de banco de dados DB2  
Para converter objetos de banco de dados do DB2, você primeiro selecionar os objetos que você deseja converter e, em seguida, SSMA executar a conversão. Para exibir mensagens de saída durante a conversão no **exibição** menu, selecione **saída**.  
  
**Para converter objetos DB2 em sintaxe de SQL Server**  
  
1.  No Gerenciador de metadados do DB2, expanda o servidor do DB2 e, em seguida, expanda **esquemas**.  
  
2.  Selecione objetos para converter:  
  
    -   Para converter todos os esquemas, selecione a caixa de seleção ao lado de **esquemas**.  
  
    -   Para converter ou omitir um banco de dados, marque a caixa de seleção ao lado do nome do esquema.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda um esquema e, em seguida, marque ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir os objetos individuais, expanda a pasta de categoria e, em seguida, marque ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com botão direito **esquemas** e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou as categorias de objetos, clicando duas vezes o objeto ou a pasta pai e, em seguida, selecionando **converter esquema**.  
  
## <a name="viewing-conversion-problems"></a>Problemas de conversão de exibição  
Alguns objetos do DB2 podem não ser convertidos. Você pode determinar as taxas de sucesso de conversão exibindo o relatório de resumo de conversão.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do DB2, selecione **esquemas**.  
  
2.  No painel direito, selecione o **relatório** guia.  
  
    Este relatório mostra o relatório de resumo de avaliação para todos os objetos de banco de dados que tenham sido avaliada ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório para um esquema individual, selecione o esquema no Gerenciador de metadados do DB2.  
  
    -   Para exibir o relatório para um objeto individual, selecione o objeto no Gerenciador de metadados do DB2. Objetos que têm problemas de conversão têm um ícone de erro vermelho.  
  
Para objetos que falha na conversão, você pode exibir a sintaxe que resultaram em falha de conversão.  
  
**Para exibir os problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do DB2, expanda **esquemas**.  
  
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
  
-   Você pode modificar o objeto no banco de dados DB2 para remover ou revisar código problemática. Para carregar o código atualizado no SSMA, você terá que atualizar os metadados. Para obter mais informações, consulte [se conectar ao banco de dados DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
-   Você pode excluir o objeto de migração. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados e o Gerenciador de metadados do DB2, desmarque a caixa de seleção ao lado do item antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e migração de dados do DB2.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [carregar objetos convertidos no SQL Server](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
## <a name="see-also"></a>Consulte também  
[Migrando dados do DB2 no SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
