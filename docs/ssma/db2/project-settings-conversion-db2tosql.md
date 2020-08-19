---
description: Configurações do projeto (conversão) (DB2ToSQL)
title: Configurações do projeto (conversão) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 165287fd2d699c56dc635d85fd58a1b081a497a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427028"
---
# <a name="project-settings-conversion-db2tosql"></a>Configurações do projeto (conversão) (DB2ToSQL)
A página conversão da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA converte a sintaxe do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe.  
  
O painel de conversão está disponível nas caixas de diálogo **configurações do projeto** e **configurações padrão do projeto** :  
  
-   Para especificar as configurações para todos os projetos do SSMA, no menu **ferramentas** , clique em **configurações de projeto padrão**, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas ou alteradas no menu suspenso **versão de destino de migração** , clique em **geral** na parte inferior do painel esquerdo e clique em **conversão**.  
  
-   Para especificar as configurações para o projeto atual, no menu **ferramentas** , clique em **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **conversão**.  
  
## <a name="conversion-messages"></a>Mensagens de conversão  
  
### <a name="generate-messages-about-issues-applied"></a>Gerar mensagens sobre os problemas aplicados  
Especifica se o SSMA gera mensagens informativas durante a conversão, exibe-as no painel de saída e as adiciona ao código convertido.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Não  
  
## <a name="miscellaneous-options"></a>Opções diversas  
  
### <a name="cast-rownum-expressions-as-integers"></a>Converter expressões ROWNUM como números inteiros  
Quando o SSMA converte as expressões ROWNUM, ele converte a expressão em uma cláusula TOP, seguida pela expressão. O exemplo a seguir mostra ROWNUM em uma instrução de exclusão do DB2:  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
O exemplo a seguir mostra o resultado [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
A parte superior exige que a expressão TOP cláusulas seja avaliada como um inteiro. Se o inteiro for negativo, a instrução produzirá um erro.  
  
-   Se você selecionar **Sim**, o SSMA converterá a expressão como um inteiro.  
  
-   Se você selecionar **não**, o SSMA marcará todas as expressões não-inteiras como um erro no código convertido.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/completo:** Não  
  
**Modo otimista:** Ok  
  
### <a name="default-schema-mapping"></a>Mapeamento de esquema padrão  
Essa configuração especifica como os esquemas DB2 são mapeados para esquemas de SQL Server. Duas opções estão disponíveis nesta configuração:  
  
1.  **Esquema para o banco de dados:** Neste modo, o esquema DB2 ' SCH1 ' será mapeado por padrão para ' dbo ' SQL Server esquema no banco de dados SQL Server ' SCH1 '.  
  
2.  **Esquema para esquema:** Nesse modo, o esquema DB2 ' SCH1 ' será mapeado por padrão para ' SCH1 ' SQL Server esquema no banco de dados de SQL Server padrão fornecido na caixa de diálogo de conexão.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Esquema para o banco de dados  
  
### <a name="conversion-ways-of-merge-statement"></a>Maneiras de conversão da instrução MERGE  
  
-   Se você selecionar **usando inserir, atualizar, excluir instrução**, o SSMA converterá a instrução merger em instruções INSERT, Update e Delete.  
  
-   Se você selecionar **usando a instrução MERGE**, o SSMA converterá a instrução merger na instrução MERGE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!WARNING]  
> Essa opção de configuração de projeto está disponível apenas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Usando a instrução MERGE  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>Converter chamadas para subprogramas que usam argumentos padrão  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as funções não dão suporte à omissão de parâmetros na chamada de função. Além disso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as funções e procedimentos não dão suporte a expressões como valores de parâmetro padrão.  
  
-   Se você selecionar **Sim** e uma chamada de função omitir parâmetros, o SSMA irá inserir a palavra-chave **Default** na função e chamará a posição correta. Em seguida, ele marcará a chamada com um aviso.  
  
-   Se você selecionar **não**, o SSMA marcará as chamadas de função como erros.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="convert-count-function-to-count_big"></a>Converter função de contagem em COUNT_BIG  
Se suas funções de contagem provavelmente retornarem valores maiores que 2.147.483.647, que é 2<sup>31</sup>-1, você deve converter as funções para COUNT_BIG.  
  
-   Se você selecionar **Sim**, o SSMA converterá todos os usos de COUNT para COUNT_BIG.  
  
-   Se você selecionar **não**, as funções permanecerão como contagem. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro se a função retornar um valor maior que 2<sup>31</sup>-1.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/completo:** Ok  
  
**Modo otimista:** Não  
  
### <a name="convert-forall-statement-to-while-statement"></a>Converter instrução FORALL para instrução WHILE  
Define como o SSMA tratará loops FORALL em elementos de coleção PL/SQL.  
  
-   Se você selecionar **Sim**, o SSMA criará um loop while em que os elementos da coleção são recuperados um a um.  
  
-   Se você selecionar **não**, o SSMA gerará um conjunto de linhas da coleção usando o método Nodes () e o usará como uma única tabela. Isso é mais eficiente, mas torna o código de saída menos legível.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Ok  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>Converter chaves estrangeiras com ação referencial SET NULL na coluna que não é nula  
O DB2 permite a criação de restrições Foreign Key, em que uma ação SET NULL não poderia ser executada porque nulos não são permitidos na coluna referenciada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Não permite essa configuração de chave estrangeira.  
  
-   Se você selecionar **Sim**, o SSMA gerará ações referenciais como no DB2, mas será necessário fazer alterações manuais antes de carregar a restrição para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, você pode escolher nenhuma ação em vez de definir nulo.  
  
-   Se você selecionar **não**, a restrição será marcada como um erro.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Não  
  
### <a name="convert-function-calls-to-procedure-calls"></a>Converter chamadas de função em chamadas de procedimento  
Algumas funções do DB2 são definidas como transações autônomas ou contêm instruções que não seriam válidas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nesses casos, o SSMA cria um procedimento e uma função que é um wrapper para o procedimento. A função convertida chama o procedimento de implementação.  
  
O SSMA pode converter chamadas para a função de wrapper em chamadas para o procedimento. Isso cria um código mais legível e pode melhorar o desempenho. No entanto, o contexto nem sempre permite; por exemplo, você não pode substituir uma chamada de função na lista de seleção por uma chamada de procedimento. O SSMA tem algumas opções para abranger os casos comuns:  
  
-   Se você selecionar **sempre**, o SSMA tentará converter chamadas de função de wrapper em chamadas de procedimento. Se o contexto atual não permitir essa conversão, uma mensagem de erro será produzida. Dessa forma, nenhuma chamada de função é deixada no código gerado.  
  
-   Se você selecionar **quando possível**, o SSMA fará uma movimentação para chamadas de procedimento somente se a função tiver parâmetros de saída. Quando a movimentação não é possível, o atributo de saída do parâmetro é removido. Em todos os outros casos, o SSMA deixa chamadas de função.  
  
-   Se você selecionar **nunca**, o SSMA deixará todas as chamadas de função como chamadas de função. Às vezes, essa opção pode ser inaceitável devido a motivos de desempenho.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Quando possível  
  
### <a name="convert-lock-table-statements"></a>Converter instruções de tabela de bloqueio  
O SSMA pode converter muitas instruções LOCK TABLE em dicas de tabela. O SSMA não pode converter quaisquer instruções de tabela de bloqueio que contenham cláusulas de partição, subpartição, @dblink e nowait e marcará essas instruções com mensagens de erro de conversão.  
  
-   Se você selecionar **Sim**, o SSMA converterá as instruções de tabela de bloqueio com suporte em dicas de tabela.  
  
-   Se você selecionar **não**, o SSMA marcará todas as instruções da tabela de bloqueio com mensagens de erro de conversão.  
  
A tabela a seguir mostra como o SSMA converte os modos de bloqueio do DB2:  
  
|Modo de bloqueio do DB2|Dica de tabela SQL Server|  
|-|-|  
|COMPARTILHAMENTO DE LINHA|HOLDLOCK DE BLOQUEIO|  
|LINHA EXCLUSIVA|XLOCK, HOLDLOCK|  
|COMPARTILHAMENTO DE ATUALIZAÇÃO = COMPARTILHAMENTO DE LINHA|HOLDLOCK DE BLOQUEIO|  
|COMPARTILHAR|TABLOCK, HOLDLOCK|  
|LINHA DE COMPARTILHAMENTO EXCLUSIVA|TABLOCK, XLOCK, HOLDLOCK|  
|Exclude|TABLOCKX, HOLDLOCK|  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>Converter instruções OPEN-FOR para parâmetros de CURSOR OUT de referência  
No DB2, a instrução OPEN-FOR pode ser usada para retornar um conjunto de resultados para o parâmetro OUT de um subprograma do CURSOR REF do tipo. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , procedimentos armazenados retornam diretamente os resultados de instruções SELECT.  
  
O SSMA pode converter muitas instruções OPEN-FOR em instruções SELECT.  
  
-   Se você selecionar **Sim**, o SSMA converterá a instrução Open-for em uma instrução SELECT, que retorna o conjunto de resultados para o cliente.  
  
-   Se você selecionar **não**, o SSMA irá gerar uma mensagem de erro no código convertido e no painel de saída.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>Converter o registro como uma lista de variáveis separadas  
O SSMA pode converter registros do DB2 em variáveis separadas e em variáveis XML com estrutura específica.  
  
-   Se você selecionar **Sim**, o SSMA converterá o registro em uma lista de variáveis separadas, quando possível.  
  
-   Se você selecionar **não**, o SSMA converterá o registro em variáveis XML com estrutura específica.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>Converter chamadas de função SUBST para chamadas de função de subcadeias  
O SSMA pode converter chamadas de função SUBST do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamadas de função de **subcadeia de caracteres** , dependendo do número de parâmetros. Se o SSMA não puder converter uma chamada de função SUBST ou o número de parâmetros não for suportado, o SSMA converterá a chamada de função SUBST em uma chamada de função personalizada do SSMA.  
  
-   Se você selecionar **Sim**, o SSMA converterá chamadas de função subst que usam três parâmetros em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **substring**. Outras funções de SUBSTr serão convertidas para chamar a função personalizada do SSMA.  
  
-   Se você selecionar **não**, o SSMA converterá a chamada de função subst em uma chamada de função personalizada do SSMA.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Ok  
  
**Modo completo:** Não  
  
### <a name="convert-subtypes"></a>Converter subtipos  
O SSMA pode converter subtipos PL/SQL de duas maneiras:  
  
-   Se você selecionar **Sim**, o SSMA criará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um tipo definido pelo usuário de um subtipo e o usará para cada variável desse subtipo.  
  
-   Se você selecionar **não**, o SSMA substituirá todas as declarações de origem do subtipo pelo tipo subjacente e converterá o resultado como de costume. Nesse caso, nenhum tipo adicional é criado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Não  
  
### <a name="convert-synonyms"></a>Converter sinônimos  
Os sinônimos para os seguintes objetos DB2 podem ser migrados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Tabelas e tabelas de objeto  
  
-   Exibições e exibições de objeto  
  
-   Procedimentos armazenados e funções  
  
-   Exibições materializadas  
  
Os sinônimos para os seguintes objetos DB2 podem ser substituídos por referências diretas para os objetos:  
  
-   Sequências  
  
-   Pacotes  
  
-   Objetos de esquema de classe Java  
  
-   Tipos de objeto definidos pelo usuário  
  
Não é possível migrar outros sinônimos. O SSMA irá gerar mensagens de erro para o sinônimo e todas as referências que usam o sinônimo.  
  
-   Se você selecionar **Sim**, o SSMA criará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sinônimos e referências diretas a objetos de acordo com as listas anteriores.  
  
-   Se você selecionar **não**, o SSMA criará referências diretas de objeto para todos os sinônimos listados aqui.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="convert-to_chardate-format"></a>Converter TO_CHAR (data, formato)  
O SSMA pode converter o TO_CHAR DB2 (data, Format) em procedimentos do banco de dados sysdb.  
  
-   Se você selecionar **usando TO_CHAR_DATE função**, o SSMA converterá a TO_CHAR (data, formato) na função TO_CHAR_DATE usando o idioma Inglês para conversão.  
  
-   Se você selecionar **usando a função TO_CHAR_DATE_LS (NLS Care)**, o SSMA converterá a TO_CHAR (data, formato) na função TO_CHAR_DATE_LS usando o idioma da sessão para conversão  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Usando a função TO_CHAR_DATE  
  
**Modo completo:** Usando a função TO_CHAR_DATE_LS (atendimento NLS)  
  
### <a name="convert-transaction-processing-statements"></a>Converter instruções de processamento de transação  
O SSMA pode converter instruções de processamento de transações do DB2:  
  
-   Se você selecionar **Sim**, o SSMA converterá instruções de processamento de transações do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instruções.  
  
-   Se você selecionar **não**, o SSMA marcará as instruções de processamento da transação como erros de conversão.  
  
> [!NOTE]  
> O DB2 abre transações implicitamente. Para emular esse comportamento no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você deve adicionar BEGIN TRANSACTION instruções manualmente em que deseja que suas transações sejam iniciadas. Como alternativa, você pode executar o comando SET IMPLICIT_TRANSACTIONS ON no início da sessão. O SSMA adiciona o conjunto de IMPLICIT_TRANSACTIONS automaticamente ao converter sub-rotinas com transações autônomas.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>Emular comportamento nulo do DB2 em cláusulas de ORDENAção  
Os valores nulos são ordenados de forma diferente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e DB2:  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , os valores nulos são os valores mais baixos em uma lista ordenada. Em uma lista crescente, os valores nulos serão exibidos primeiro.  
  
-   No DB2, os valores nulos são os valores mais altos em uma lista ordenada. Por padrão, os valores nulos aparecem por último em uma lista de ordem crescente.  
  
-   O DB2 tem as últimas cláusulas NULL e NULLs, o que permite alterar o modo como as ordens do DB2 são nulas.  
  
O SSMA pode emular o comportamento de pedidos do DB2 por meio da verificação de valores nulos. Em seguida, ele primeiro ordena por valores nulos na ordem especificada e, em seguida, ordena por outros valores.  
  
-   Se você selecionar **Sim**, o SSMA converterá a instrução do DB2 de uma maneira que emula o comportamento de ordenação do DB2.  
  
-   Se você selecionar **não**, o SSMA ignorará as regras do DB2 e gerará uma mensagem de erro quando encontrar as cláusulas or NULLs primeiro e as últimas.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Ok  
  
### <a name="emulate-row-count-exceptions-in-select"></a>Emular exceções de contagem de linhas em SELECT  
Se uma instrução SELECT com uma cláusula INTO não retornar nenhuma linha, o DB2 gerará uma exceção NO_DATA_FOUND. Se a instrução retornar duas ou mais linhas, a exceção TOO_MANY_ROWS será gerada. A instrução convertida no não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará nenhuma exceção se a contagem de linhas for diferente de uma.  
  
-   Se você selecionar **Sim**, o SSMA adicionará a chamada para o procedimento sysdb db_error_exact_one_row_check depois de cada instrução SELECT. Esse procedimento emula as exceções de NO_DATA_FOUND e TOO_MANY_ROWS. Esse é o padrão e permite a reprodução do comportamento do DB2 o mais próximo possível. Você deve sempre escolher **Sim** se o código-fonte tiver manipuladores de exceção que processam esses erros. Observe que, se a instrução SELECT ocorrer dentro de uma função definida pelo usuário, esse módulo será convertido em um procedimento armazenado, pois a execução de procedimentos armazenados e a geração de exceções não é compatível com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto de função.  
  
-   Se você selecionar **não**, nenhuma exceção será gerada. Isso pode ser útil quando o SSMA converte uma função definida pelo usuário e você deseja que ela permaneça uma função no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="generate-error-for-dbms_sqlparse"></a>Gerar erro para DBMS_SQL. PASSAR  
  
-   Se você selecionar **erro**, o SSMA gerará erro na conversão DBMS_SQL. Passar.  
  
-   Se você selecionar **aviso**, o SSMA gerará um aviso na DBMS_SQL de conversão. Passar.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ao  
  
### <a name="generate-rowid-column"></a>Gerar coluna de ROWID  
Quando o SSMA cria tabelas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ele pode criar uma coluna de ROWID. Quando os dados são migrados, cada linha Obtém um novo valor UNIQUEIDENTIFIER gerado pela função NEWID ().  
  
-   Se você selecionar **Sim**, a coluna de ROWID será criada em todas as tabelas e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará GUIDs à medida que você inserir valores. Sempre escolha **Sim** se você estiver planejando usar o SSMA Tester.  
  
-   Se você selecionar **não**, as colunas de ROWID não serão adicionadas às tabelas.  
  
-   **Adicionar coluna de ROWID para tabelas com gatilhos** adicionar ROWID para as tabelas que contêm gatilhos.  
  
> [!WARNING]  
> A configuração padrão no caso de SQL Server 2005, SQL Server 2008 e SQL Server 2012 e 2014 é **Adicionar a coluna de ROWID para tabelas com gatilhos**.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Adicionar coluna de ROWID para tabelas com gatilhos  
  
**Modo completo:** Ok  
  
### <a name="generate-unique-index-on-rowid-column"></a>Gerar índice exclusivo na coluna de ROWID  
Especifica se o SSMA gera uma coluna de índice exclusivo na coluna gerada pelo ROWID ou não. Se a opção for definida como "Sim", o índice exclusivo será gerado e, se for definido como "não", o índice exclusivo não será gerado na coluna de ROWID.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="local-modules-conversion"></a>Conversão de módulos locais  
Define o tipo de subprograma aninhado do DB2 (declarado na conversão de procedimento armazenado autônomo ou função).  
  
-   Se você selecionar **embutido**, as chamadas aninhadas do subprograma serão substituídas por seu corpo.  
  
-   Se você selecionar **procedimentos armazenados**, o subprograma aninhado será convertido em um procedimento armazenado SQL Server e suas chamadas serão substituídas nesta chamada de procedimento.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Linha  
  
### <a name="use-isnull-in-string-concatenation"></a>Usar ISNULL em concatenação de cadeia de caracteres  
DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornam resultados diferentes quando as concatenações de cadeia de caracteres incluem valores nulos. O DB2 trata o valor nulo como um conjunto de caracteres vazio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Retorna NULL.  
  
-   Se você selecionar **Sim**, o SSMA substituirá o caractere de concatenação do DB2 (| |) pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caractere de concatenação (+). O SSMA também verifica as expressões em ambos os lados da concatenação para valores nulos.  
  
-   Se você selecionar **não**, o SSMA substituirá os caracteres de concatenação, mas não verificará se há valores nulos.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
### <a name="use-isnull-in-replace-function-calls"></a>Usar ISNULL em substituir chamadas de função  
A instrução ISNULL é usada em substituir chamadas de função para emular o comportamento do DB2. As seguintes opções estão presentes para essa configuração:  
  
-   YES  
  
-   Não  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Ok  
  
### <a name="use-isnull-in-concat-function-calls"></a>Usar ISNULL em chamadas de função CONCAT  
A instrução ISNULL é usada em chamadas de função CONCAT para emular o comportamento do DB2. As seguintes opções estão presentes para essa configuração:  
  
-   YES  
  
-   Não  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Ok  
  
### <a name="use-native-convert-function-when-possible"></a>Use a função de conversão nativa quando possível  
  
-   Se você selecionar **Sim**, o SSMA converterá o TO_CHAR (data, formato) na função de conversão nativa quando possível.  
  
-   Se você selecionar **não**, o SSMA converterá o TO_CHAR (data, formato) em TO_CHAR_DATE ou TO_CHAR_DATE_LS (ele será definido pelas opções "converter TO_CHAR (data, formato)").  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Ok  
  
**Modo completo:** Não  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>Usar selecionar... FOR XML ao converter SELECT... EM para variável de registro  
Especifica se um conjunto de resultados XML deve ser gerado quando você seleciona em uma variável de registro.  
  
-   Se você selecionar **Sim**, a instrução SELECT retornará XML.  
  
-   Se você selecionar **não**, a instrução SELECT retornará um conjunto de resultados.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Não  
  
## <a name="returning-clause-conversion"></a>Conversão de cláusula de retorno  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>Converter a cláusula de retorno na instrução DELETE para a saída  
O DB2 fornece uma cláusula de retorno como uma maneira de obter imediatamente valores excluídos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece essa funcionalidade com a cláusula OUTPUT.  
  
-   Se você selecionar **Sim**, o SSMA converterá cláusulas de retorno em instruções DELETE para cláusulas de saída. Como os gatilhos em uma tabela podem alterar valores, o valor retornado pode ser diferente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relação ao que estava no DB2.  
  
-   Se você selecionar **não**, o SSMA gerará uma instrução SELECT antes de excluir instruções para recuperar os valores retornados.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>Converter a cláusula de retorno na instrução INSERT para a saída  
O DB2 fornece uma cláusula de retorno como uma maneira de obter imediatamente os valores inseridos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece essa funcionalidade com a cláusula OUTPUT.  
  
-   Se você selecionar **Sim**, o SSMA converterá uma cláusula de retorno em uma instrução INSERT para output. Como os gatilhos em uma tabela podem alterar valores, o valor retornado pode ser diferente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relação ao que estava no DB2.  
  
-   Se você selecionar **não**, o SSMA emulará a funcionalidade do DB2 inserindo e, em seguida, selecionando valores de uma tabela de referência.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>Converter a cláusula de retorno na instrução UPDATE para a saída  
O DB2 fornece uma cláusula de retorno como uma maneira de obter imediatamente valores atualizados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece essa funcionalidade com a cláusula OUTPUT.  
  
-   Se você selecionar **Sim**, o SSMA converterá cláusulas de retorno em instruções UPDATE para cláusulas de saída. Como os gatilhos em uma tabela podem alterar valores, o valor retornado pode ser diferente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relação ao que estava no DB2.  
  
-   Se você selecionar **não**, o SSMA gerará instruções SELECT após as instruções UPDATE para recuperar valores retornados.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Ok  
  
## <a name="sequence-conversion"></a>Conversão de sequência  
  
### <a name="convert-sequence-generator"></a>Converter gerador de sequência  
No DB2, você pode usar uma sequência para gerar identificadores exclusivos.  
  
O SSMA pode converter sequências para o seguinte.  
  
-   Usando o gerador de sequência SQL Server (essa opção só está disponível ao converter para SQL Server 2012 e SQL Server 2014).  
  
-   Usando o gerador de sequência do SSMA.  
  
-   Usando a identidade da coluna.  
  
A opção padrão ao converter para SQL Server 2012 ou SQL Server 2014 é usar SQL Server gerador de sequência. No entanto, SQL Server 2012 e SQL Server 2014 não dão suporte à obtenção do valor de sequência atual (como a do método currval de sequência do DB2). Consulte o site do blog da equipe do SSMA para obter diretrizes sobre a migração do método currval Sequence de sequência do DB2.  
  
O SSMA também fornece uma opção para converter a sequência do DB2 para o emulador de sequência do SSMA. Essa é a opção padrão quando você converte para SQL Server antes de 2012  
  
Por fim, você também pode converter a sequência atribuída a uma coluna na tabela para SQL Server valores de identidade. Você deve especificar o mapeamento entre as sequências para uma coluna de identidade na guia **tabela** do DB2  
  
### <a name="convert-currval-outside-triggers"></a>Converter gatilhos CURRVAL externos  
Visível somente quando o gerador de sequência de conversão é definido como **usando a identidade da coluna**. Como as sequências do DB2 são objetos separados das tabelas, muitas tabelas que usam sequências usam um gatilho para gerar e inserir um novo valor de sequência. O SSMA comenta essas instruções ou marca-as como erros quando o comentário gerar erros.  
  
-   Se você selecionar **Sim**, o SSMA marcará todas as referências a gatilhos externos na sequência convertida currval com um aviso.  
  
-   Se você selecionar **não**, o SSMA marcará todas as referências a gatilhos externos na sequência convertida currval com um erro.  
  
## <a name="see-also"></a>Consulte Também  
[Referência da interface do usuário &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
