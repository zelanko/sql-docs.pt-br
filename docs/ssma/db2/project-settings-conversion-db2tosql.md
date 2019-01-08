---
title: Configurações (conversão) (DB2ToSQL) do projeto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a446fd4ce116ee19aa8b38d1ae6d8213e35c16e1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52392470"
---
# <a name="project-settings-conversion-db2tosql"></a>Configurações do projeto (conversão) (DB2ToSQL)
A página de conversão do **configurações do projeto** caixa de diálogo contém configurações que personalizam como SSMA converte a sintaxe do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe.  
  
O painel de conversão está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo:  
  
-   Para especificar configurações para todos os projetos do SSMA, na **ferramentas** menu, clique em **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida ou alterada de  **Versão de destino de migração** lista suspensa e, em seguida, clique em **gerais** na parte inferior do painel esquerdo e, em seguida, clique **conversão**.  
  
-   Para especificar configurações para o projeto atual, no **ferramentas** menu, clique em **configurações do projeto**, em seguida, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **Conversão**.  
  
## <a name="conversion-messages"></a>Mensagens de conversão  
  
### <a name="generate-messages-about-issues-applied"></a>Gerar mensagens sobre problemas aplicados  
Especifica se o SSMA gera mensagens informativas durante a conversão, exibe-os no painel de saída e adiciona-os no código convertido.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Não  
  
## <a name="miscellaneous-options"></a>Opções diversas  
  
### <a name="cast-rownum-expressions-as-integers"></a>Expressões de ROWNUM conversão como inteiros  
Quando o SSMA converte expressões ROWNUM, ele converte a expressão em uma cláusula TOP, seguida pela expressão. O exemplo a seguir mostra ROWNUM em uma instrução DELETE do DB2:  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
O exemplo a seguir mostra a resultante [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
Parte superior requer que a expressão de cláusulas TOP é avaliada como um inteiro. Se o inteiro for negativo, a instrução produzirá um erro.  
  
-   Se você selecionar **Sim**, SSMA converte a expressão como um número inteiro.  
  
-   Se você selecionar **não**, SSMA marcará todas as expressões de não inteiro como um erro no código convertido.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/completo:** Não  
  
**Modo otimista:** Sim  
  
### <a name="default-schema-mapping"></a>Mapeamento de esquema padrão  
Essa configuração especifica como os esquemas do DB2 são mapeadas para esquemas SQL Server. Duas opções estão disponíveis nesta configuração:  
  
1.  **Esquema de banco de dados:** Nesse esquema do DB2 de modo 'sch1' será mapeado por padrão ao esquema do SQL Server 'dbo' no banco de dados do SQL Server 'sch1'.  
  
2.  **Esquema ao esquema:** nesse modo DB2 o esquema 'sch1' será mapeado por padrão ao esquema do SQL Server 'sch1' no banco de dados do SQL Server padrão fornecido na caixa de diálogo de conexão.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Esquema de banco de dados  
  
### <a name="conversion-ways-of-merge-statement"></a>Maneiras de conversão de instrução MERGE  
  
-   Se você selecionar **usando INSERT, UPDATE, DELETE instrução**, SSMA converte a instrução de FUSÃO em Inserir, atualizar e excluir instruções.  
  
-   Se você selecionar **instrução usando MERGE**, o SSMA converte a instrução de FUSÃO em instrução MERGE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!WARNING]  
> Essa opção de configuração do projeto está disponível apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Usando a instrução MERGE  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>Converter chamadas para subprogramas que usam argumentos padrão  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções não dão suporte a omissão de parâmetros na chamada de função. Além disso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimentos e funções não têm suporte para expressões como valores de parâmetro padrão.  
  
-   Se você selecionar **Yes** e uma chamada de função omite parâmetros, o SSMA para inserir a palavra-chave **padrão** na função e chamada na posição correta. Em seguida, ele marcará a chamada com um aviso.  
  
-   Se você selecionar **não**, SSMA irá marcar as chamadas de função como erros.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="convert-count-function-to-countbig"></a>Converter função COUNT para COUNT_BIG  
Se suas funções de contagem provavelmente retornar valores maiores que 2.147.483.647, que é 2<sup>31</sup>-1, você deve converter as funções em COUNT_BIG.  
  
-   Se você selecionar **Sim**, SSMA converterá todos os usos da contagem de COUNT_BIG.  
  
-   Se você selecionar **não**, as funções permanecerão como contagem. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro se a função retorna um valor maior que 2<sup>31</sup>-1.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/completo:** Sim  
  
**Modo otimista:** Não  
  
### <a name="convert-forall-statement-to-while-statement"></a>Converter instrução FORALL WHILE instrução  
Define como o SSMA tratará FORALL loops em elementos de coleção de PL/SQL.  
  
-   Se você selecionar **Sim**, SSMA cria um loop WHILE no qual os elementos da coleção são recuperados individualmente.  
  
-   Se você selecionar **não**, SSMA gera um conjunto de linhas da coleção usando o método () de nós e usa-o como uma única tabela. Isso é mais eficiente, mas torna o código de saída menos legível.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Sim  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>Chaves estrangeiras de Convert com a ação referencial SET NULL na coluna é NOT NULL  
DB2 permite a criação de restrições de chave estrangeira, onde uma ação SET NULL não pôde, possivelmente, ser executada porque os valores nulos não são permitidos na coluna referenciada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite essa configuração de chave estrangeira.  
  
-   Se você selecionar **Yes**, o SSMA irá gerar ações referenciais como no DB2, mas você precisará fazer alterações manuais antes de carregar a restrição [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, você pode escolher NO ACTION, em vez de SET NULL.  
  
-   Se você selecionar **não**, a restrição será marcada como um erro.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Não  
  
### <a name="convert-function-calls-to-procedure-calls"></a>Converter chamadas de função para chamadas de procedimento  
Algumas funções do DB2 são definidas como transações autônomas ou conter instruções que não é válidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nesses casos, o SSMA cria um procedimento e uma função que é um wrapper para o procedimento. A função convertida chama o procedimento de implementação.  
  
O SSMA pode converter chamadas para a função de wrapper em chamadas para o procedimento. Isso cria um código mais legível e pode melhorar o desempenho. No entanto, o contexto não sempre que ele; Por exemplo, você não pode substituir uma chamada de função na lista de seleção com uma chamada de procedimento. O SSMA tem algumas opções para abranger os casos comuns:  
  
-   Se você selecionar **sempre**, SSMA tenta converter as chamadas de função de wrapper em chamadas de procedimento. Se o contexto atual não permite essa conversão, uma mensagem de erro será produzida. Dessa forma, nenhuma chamada de função é deixada no código gerado.  
  
-   Se você selecionar **quando possível**, SSMA faz uma movimentação para chamadas de procedimento somente se a função tem parâmetros de saída. Quando a movimentação não é possível, o atributo de saída do parâmetro é removido. Em todos os outros casos, o SSMA deixa chamadas de função.  
  
-   Se você selecionar **nunca**, SSMA deixará todas as chamadas de função como chamadas de função. Às vezes, essa opção pode ser inaceitável devido a motivos de desempenho.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Quando possível  
  
### <a name="convert-lock-table-statements"></a>Converter instruções de bloqueio de tabela  
O SSMA pode converter a muitas instruções de bloqueio de tabela em dicas de tabela. O SSMA não é possível converter qualquer instrução de bloqueio de tabela que contêm a partição, SUBPARTIÇÃO, @dblinke cláusulas NOWAIT e o marcará tais instruções com mensagens de erro de conversão.  
  
-   Se você selecionar **Sim**, SSMA irá converter instruções de bloqueio de tabela com suporte para dicas de tabela.  
  
-   Se você selecionar **não**, SSMA marcará todas as instruções de bloqueio de tabela com mensagens de erro de conversão.  
  
A tabela a seguir mostra como o SSMA converte os modos de bloqueio do DB2:  
  
|||  
|-|-|  
|DB2 Modo de bloqueio|Dica de tabela do SQL Server|  
|COMPARTILHAMENTO DE LINHA|ROWLOCK, HOLDLOCK|  
|EXCLUSIVO DE LINHA|ROWLOCK, XLOCK, HOLDLOCK|  
|ATUALIZAÇÃO DE COMPARTILHAMENTO = COMPARTILHAMENTO DE LINHA|ROWLOCK, HOLDLOCK|  
|COMPARTILHAR|TABLOCK, HOLDLOCK|  
|COMPARTILHAMENTO DE LINHA EXCLUSIVA|TABLOCK, XLOCK, HOLDLOCK|  
|EXCLUSIVO|TABLOCKX, HOLDLOCK|  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>Converter instruções FOR aberto para parâmetros de REF CURSOR OUT  
No DB2, a instrução FOR aberto pode ser usada para retornar um conjunto de resultados para uma subprograma-OUT de parâmetro de tipo REF CURSOR. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], procedimentos armazenados diretamente retornam os resultados de instruções SELECT.  
  
O SSMA pode converter a muitas instruções FOR aberto em instruções SELECT.  
  
-   Se você selecionar **Sim**, SSMA converte a instrução FOR aberto em uma instrução SELECT, que retorna o conjunto de resultados para o cliente.  
  
-   Se você selecionar **não**, SSMA gerará uma mensagem de erro no código convertido e no painel de saída.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>Converter o registro como uma lista de variáveis separa  
SSMA pode converter os registros de DB2 em separa variáveis e em variáveis XML com a estrutura específica.  
  
-   Se você selecionar **Sim**, SSMA converte o registro em uma lista de variáveis separa quando possível.  
  
-   Se você selecionar **não**, SSMA converte o registro em variáveis XML com a estrutura específica.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>Converter SUBSTR chamadas de função para chamadas de função de subcadeia de caracteres  
O SSMA pode converter DB2 SUBSTR chamadas de função em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **subcadeia de caracteres** chamadas de função, dependendo do número de parâmetros. Se o SSMA não é possível converter uma chamada de função SUBSTR ou não há suporte para o número de parâmetros, SSMA irá converter a chamada de função SUBSTR em uma chamada de função personalizada do SSMA.  
  
-   Se você selecionar **Yes**, SSMA converterá as chamadas de função SUBSTR que usam três parâmetros na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **subcadeia de caracteres**. Outras funções SUBSTR serão convertidas para chamar a função personalizada do SSMA.  
  
-   Se você selecionar **não**, SSMA irá converter a chamada de função SUBSTR em uma chamada de função personalizada do SSMA.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Sim  
  
**Modo completo:** Não  
  
### <a name="convert-subtypes"></a>Converter subtipos  
O SSMA pode converter os subtipos de PL/SQL de duas maneiras:  
  
-   Se você selecionar **Sim**, o SSMA criará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definida pelo usuário de um subtipo de tipo e usá-lo para cada variável desse subtipo.  
  
-   Se você selecionar **não**, SSMA irá substituir todas as declarações de código-fonte do subtipo com o tipo subjacente e converter o resultado como de costume. Nesse caso, não há tipos adicionais são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Não  
  
### <a name="convert-synonyms"></a>Converter sinônimos  
Sinônimos para os seguintes objetos do DB2 podem ser migrados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Tabelas e tabelas de objeto  
  
-   Modos de exibição e objeto  
  
-   Procedimentos armazenados e funções  
  
-   Exibições materializadas  
  
Sinônimos para os seguintes objetos do DB2 podem ser substituídos por referências diretas aos objetos:  
  
-   Sequências  
  
-   Packages  
  
-   Objetos de esquema de classe de Java  
  
-   Tipos de objeto definido pelo usuário  
  
Outros sinônimos não podem ser migrados. O SSMA irá gerar mensagens de erro para o sinônimo e todas as referências que usam o sinônimo.  
  
-   Se você selecionar **Yes**, o SSMA criará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sinônimos e referências de objeto de acordo com as listas anteriores.  
  
-   Se você selecionar **não**, SSMA criará referências de objeto para todos os sinônimos listados aqui.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="convert-tochardate-format"></a>Converter TO_CHAR (data, formato)  
O SSMA pode converter TO_CHAR(date, format) DB2 em procedimentos do banco de dados sysdb.  
  
-   Se você selecionar **função TO_CHAR_DATE usando**, SSMA converte o TO_CHAR (data, formato) em TO_CHAR_DATE função usando do idioma inglês para conversão.  
  
-   Se você selecionar **função usando TO_CHAR_DATE_LS (NLS cuidado)**, SSMA converte o TO_CHAR (data, formato) em TO_CHAR_DATE_LS função usando do idioma da sessão para conversão  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Usando a função TO_CHAR_DATE  
  
**Modo completo:** Usando a função TO_CHAR_DATE_LS (NLS cuidado)  
  
### <a name="convert-transaction-processing-statements"></a>Converter instruções de processamento de transação  
O SSMA pode converter as instruções de processamento de transações do DB2:  
  
-   Se você selecionar **Yes**, o SSMA converte instruções de processamento de transação do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instruções.  
  
-   Se você selecionar **não**, SSMA marca as instruções, como erros de conversão de processamento de transações.  
  
> [!NOTE]  
> DB2 abre implicitamente a transações. Para emular esse comportamento na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve adicionar instruções BEGIN TRANSACTION manualmente onde você deseja que suas transações para iniciar. Como alternativa, você pode executar o comando SET IMPLICIT_TRANSACTIONS ON no início de sua sessão. O SSMA adiciona automaticamente SET IMPLICIT_TRANSACTIONS ON durante a conversão de sub-rotinas com transações autônomas.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>Emular o comportamento do nulo DB2 nas cláusulas ORDER BY  
Valores nulos são ordenados de forma diferente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e DB2:  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nulo valores são os valores mais baixos em uma lista ordenada. Em uma lista em ordem crescente, valores NULL aparecerão primeiros.  
  
-   No DB2, valores NULL são os valores mais altos em uma lista ordenada. Por padrão, valores NULL aparecem por últimos em uma lista em ordem crescente.  
  
-   DB2 tem cláusulas valores nulos e valores nulos sobrenome, que permite que você altere como DB2 ordena os valores nulos.  
  
O SSMA pode emular o comportamento de DB2 ORDER BY, verificando os valores NULL. Ele primeiro ordena por valores NULL, na ordem especificada e, em seguida, pedidos por outros valores.  
  
-   Se você selecionar **Sim**, SSMA converterá a instrução de DB2 de forma que emula o comportamento do DB2 ORDER BY.  
  
-   Se você selecionar **não**, SSMA vai ignorar as regras do DB2 e gerar uma mensagem de erro quando ele encontra as cláusulas de valores nulos e valores nulos sobrenome.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Sim  
  
### <a name="emulate-row-count-exceptions-in-select"></a>Emular as exceções de contagem de linha em SELECT  
Se uma instrução SELECT com uma cláusula INTO não retornar nenhuma linha, o DB2 gerará uma exceção NO_DATA_FOUND. Se a instrução retorna duas ou mais linhas, a exceção TOO_MANY_ROWS será gerada. A instrução convertida em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não gera qualquer exceção se a contagem de linhas é diferente de uma.  
  
-   Se você selecionar **Sim**, SSMA adiciona a chamada para sysdb procedimento db_error_exact_one_row_check após cada instrução SELECT. Esse procedimento emula as exceções NO_DATA_FOUND e TOO_MANY_ROWS. Esse é o padrão e permite reproduzir DB2 comportamento mais próximo possível. Você sempre deve escolher **Sim** se o código-fonte tem manipuladores de exceção que processam esses erros. Observe que, se a instrução SELECT ocorrer dentro de uma função definida pelo usuário, esse módulo será convertido em um procedimento armazenado, porque a execução de procedimentos armazenados e gerando exceções não é compatível com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto de função.  
  
-   Se você selecionar **não**, nenhuma exceção será gerada. Isso pode ser útil quando SSMA converte uma função definida pelo usuário e você deseja que ele permaneça uma função em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="generate-error-for-dbmssqlparse"></a>Gere erro para DBMS_SQL. ANALISAR  
  
-   Se você selecionar **erro**, SSMA gerar erro na conversão DBMS_SQL. ANALISE.  
  
-   Se você selecionar **aviso**, SSMA Gerar aviso na conversão DBMS_SQL. ANALISE.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Erro  
  
### <a name="generate-rowid-column"></a>Gerar coluna ROWID  
Quando o SSMA cria tabelas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele pode criar uma coluna ROWID. Quando os dados são migrados, cada linha obtém um novo valor de identificador exclusivo gerado pela função NEWID ().  
  
-   Se você selecionar **Yes**, a coluna ROWID é criada em todas as tabelas e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera GUIDs assim que você inserir valores. Escolha sempre **Sim** se você estiver planejando usar o testador SSMA.  
  
-   Se você selecionar **não**, colunas ROWID não são adicionadas às tabelas.  
  
-   **Adicionar coluna ROWID para tabelas com disparadores** adicionar ROWID para as tabelas que contêm os gatilhos.  
  
> [!WARNING]  
> É a configuração padrão no caso do SQL Server 2005, SQL Server 2008 e SQL Server 2012 e 2014 **coluna adicionar ROWID para tabelas com disparadores**.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Adicionar coluna ROWID para tabelas com disparadores  
  
**Modo completo:** Sim  
  
### <a name="generate-unique-index-on-rowid-column"></a>Gerar um índice exclusivo na coluna ROWID  
Especifica se o SSMA gera a coluna de índice exclusivo na coluna ROWID gerado ou não. Se a opção for definida como "Sim", o índice exclusivo é gerado e se ele for definido como "Não", o índice exclusivo não é gerado na coluna de ROWID.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="local-modules-conversion"></a>Conversão de módulos locais  
Define o tipo de conversão do DB2 aninhados subprograma (declarada em autônomo armazenado procedimento ou função).  
  
-   Se você selecionar **embutido**, as chamadas aninhadas subprograma serão substituídas pelo seu corpo.  
  
-   Se você selecionar **procedimentos armazenados**subprograma aninhada será convertida em um procedimento armazenado do SQL Server e suas chamadas serão substituídas nessa chamada de procedimento.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** embutido  
  
### <a name="use-isnull-in-string-concatenation"></a>Use ISNULL em concatenação de cadeia de caracteres  
DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornar resultados diferentes quando concatenações de cadeia de caracteres incluem valores nulos. DB2 tratará o valor nulo como um conjunto de caracteres vazia. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna NULL.  
  
-   Se você selecionar **Sim**, o SSMA substitui o caractere de concatenação de DB2 (|) com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caracteres de concatenação (+). O SSMA também verifica as expressões em ambos os lados da concatenação de valores nulos.  
  
-   Se você selecionar **não**, SSMA substitui os caracteres de concatenação, mas não verifica a existência de valores nulos.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
### <a name="use-isnull-in-replace-function-calls"></a>Use ISNULL em chamadas de função REPLACE  
Instrução de ISNULL é usada em chamadas de função REPLACE para emular o comportamento do DB2. As opções a seguir estão presentes para essa configuração:  
  
-   YES  
  
-   Não  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Sim  
  
### <a name="use-isnull-in-concat-function-calls"></a>Use ISNULL em chamadas de função CONCAT  
Instrução de ISNULL é usada em chamadas de função CONCAT para emular o comportamento do DB2. As opções a seguir estão presentes para essa configuração:  
  
-   YES  
  
-   Não  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Não  
  
**Modo completo:** Sim  
  
### <a name="use-native-convert-function-when-possible"></a>Use a função convert nativo quando possível  
  
-   Se você selecionar **Sim**, SSMA converte o TO_CHAR (data, formato) em função de conversão nativo quando possível.  
  
-   Se você selecionar **não**, SSMA converte o TO_CHAR (data, formato) em TO_CHAR_DATE ou TO_CHAR_DATE_LS (ele é definido pelas opções "Converter TO_CHAR(date, format)").  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Sim  
  
**Modo completo:** Não  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>Use SELECT... FOR XML ao converter selecione... INTO para a variável de registro  
Especifica se deve gerar um resultado XML definido quando você seleciona em uma variável de registro.  
  
-   Se você selecionar **Sim**, a instrução SELECT retorna o XML.  
  
-   Se você selecionar **não**, a instrução SELECT retorna um conjunto de resultados.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Não  
  
## <a name="returning-clause-conversion"></a>RETORNANDO a conversão da cláusula  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>Converter a cláusula RETURNING na instrução DELETE para saída  
DB2 fornece uma cláusula RETURNING como uma maneira de obter imediatamente valores excluídos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece essa funcionalidade com a cláusula OUTPUT.  
  
-   Se você selecionar **Sim**, SSMA converterá RETORNANDO cláusulas em instruções DELETE em cláusulas de saída. Como gatilhos em uma tabela podem alterar valores, o valor retornado pode ser diferente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que era no DB2.  
  
-   Se você selecionar **não**, SSMA irá gerar uma instrução SELECT antes de instruções DELETE para recuperar valores retornados.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>Converter a cláusula RETURNING na instrução INSERT para saída  
DB2 fornece uma cláusula RETURNING como uma maneira de obter imediatamente os valores inseridos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece essa funcionalidade com a cláusula OUTPUT.  
  
-   Se você selecionar **Sim**, SSMA converterá uma cláusula RETURNING em uma instrução INSERT para saída. Como gatilhos em uma tabela podem alterar valores, o valor retornado pode ser diferente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que era no DB2.  
  
-   Se você selecionar **não**, SSMA emula a funcionalidade do DB2, inserindo e, em seguida, selecionando valores de uma tabela de referência.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>Converter a cláusula RETURNING na instrução UPDATE para saída  
DB2 fornece uma cláusula RETURNING como uma maneira de obter imediatamente os valores atualizados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece essa funcionalidade com a cláusula OUTPUT.  
  
-   Se você selecionar **Sim**, SSMA converterá RETORNANDO cláusulas em instruções UPDATE em cláusulas de saída. Como gatilhos em uma tabela podem alterar valores, o valor retornado pode ser diferente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que era no DB2.  
  
-   Se você selecionar **não**, SSMA gerará instruções SELECT após instruções UPDATE para recuperar valores de retornados.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Sim  
  
## <a name="sequence-conversion"></a>Conversão de sequência  
  
### <a name="convert-sequence-generator"></a>Converter o gerador de sequência  
No DB2, você pode usar uma sequência para gerar identificadores exclusivos.  
  
O SSMA pode converter sequências ao seguinte.  
  
-   Usando o gerador de sequência do SQL Server (essa opção só está disponível ao converter para o SQL Server 2012 e SQL Server 2014).  
  
-   Usando o gerador de sequência do SSMA.  
  
-   Usando a identidade de coluna.  
  
A opção padrão ao converter para o SQL Server 2012 ou SQL Server 2014 é usar o gerador de sequência do SQL Server. No entanto, o SQL Server 2012 e SQL Server 2014 não suporta obtendo o valor de sequência atual (como a do método do DB2 sequência currval). Consulte o site de blog de equipe do SSMA para obter orientação sobre o método de currval de sequência de DB2 migrando.  
  
O SSMA também fornece uma opção para converter a sequência de DB2 ao emulador de sequência do SSMA. Isso é a opção padrão quando você converte em SQL Server antes de 2012  
  
Por fim, você também pode converter sequência atribuída a uma coluna na tabela para valores de identidade do SQL Server. Você deve especificar o mapeamento entre as sequências para uma coluna de identidade no DB2 **tabela** guia  
  
### <a name="convert-currval-outside-triggers"></a>Converter CURRVAL fora gatilhos  
Visível somente quando o gerador de sequência converter é definido como **usando a identidade de coluna**. Como sequências de DB2 são objetos separados de tabelas, muitas tabelas do que usam sequências de usam um gatilho para gerar e inserir um novo valor de sequência. SSMA essas instruções como comentário ou marcando-as como erros quando o fora de comentário gerarem erros.  
  
-   Se você selecionar **Sim**, SSMA marcará todas as referências para fora de gatilhos em convertido sequenciar CURRVAL com um aviso.  
  
-   Se você selecionar **não**, SSMA marcará todas as referências para fora de gatilhos em convertido sequenciar CURRVAL com um erro.  
  
## <a name="see-also"></a>Consulte também  
[Referência da Interface do usuário &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
