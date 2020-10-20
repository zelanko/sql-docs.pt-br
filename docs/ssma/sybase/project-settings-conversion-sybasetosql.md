---
description: Configurações do projeto (conversão) (SybaseToSQL)
title: Configurações do projeto (conversão) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1f4d616b964a1e9e9eed391e3386b16e9df54e44
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195528"
---
# <a name="project-settings-conversion-sybasetosql"></a>Configurações do projeto (conversão) (SybaseToSQL)

A página **conversão** da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA converte a sintaxe do SAP Adaptive Server Enterprise (ase) no ou na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe do SQL do Azure.

O painel de **conversão** está disponível nas caixas de diálogo **configurações do projeto** e **configurações padrão do projeto** :

- Se você quiser especificar configurações para todos os projetos do SSMA, no menu **ferramentas** , selecione **configurações de projeto padrão**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **conversão**.

- Para especificar as configurações do projeto atual, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **conversão**.

## <a name="miscellaneous-section"></a>Seção de diversos

### <a name="error"></a>@@ERROR

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL e ASE usam códigos de erro diferentes.

Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que o SSMA mostra no painel de saída ou de Lista de Erros quando encontra uma referência ao `@@ERROR` no código do ase.

- Se você selecionar **converter e marcar com aviso**, o SSMA converterá as instruções e as marcará com comentários de aviso.
- Se você selecionar **marcar com erro**, o SSMA ignorará a conversão e marcará as instruções com comentários de erro.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Converter e marcar com aviso|
|Otimistas|Converter e marcar com aviso|
|Completo|Marcar com erro|

### <a name="conversion-of-like-operator"></a>Conversão de operador LIKE

Especifica se os operandos devem ser convertidos `LIKE` para corresponder ao comportamento do SAP ASE. O ponto é que o ASE corta os espaços em branco à direita em um padrão semelhante. A solução alternativa é fazer uma conversão da expressão direita em um tipo de dados de comprimento fixo com precisão máxima.
  
- Selecione **conversão simples** para converter as expressões sem qualquer correção.
- Para usar o comportamento do ASE, selecione **conversão para comprimento fixo.**
  
Quando você seleciona um modo de conversão na caixa modo, o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Conversão simples|
|Otimistas|Conversão simples|
|Completo|Converter em comprimento fixo|

### <a name="convert-or-cast-empty-strings-to-numeric-types"></a>CONVERSÃO ou conversão de cadeias de caracteres vazias em tipos numéricos

Especifica como tratar cadeias de caracteres vazias ou em branco dentro de `CONVERT` `CAST` expressões or com tipo numérico como argumento DataType. As seguintes opções estão disponíveis para essa configuração:

- Selecione **conversão simples** para converter as expressões sem qualquer correção.
- Se a **cadeia de caracteres vazia como zero numeric** for selecionada, o parâmetro `{s}` de cadeia de caracteres será substituído por `CASE ltrim(rtrim({s})) WHEN "" THEN 0 else {s} END` expressão.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Conversão simples|
|Otimistas|Conversão simples|
|Completo|Cadeia de caracteres vazia como zero numérico|

### <a name="concatenation-of-null"></a>Concatenação de NULL

Essa configuração especifica como converter a concatenação de cadeia de caracteres com `NULL` . As opções a seguir podem ser definidas para essa configuração específica:

- Se a opção **encapsular com a função ISNULL** estiver selecionada, cada não constante `string_expression` na concatenação será encapsulada com `ISNULL(string_expression)` e `NULL` s será substituída por uma cadeia de caracteres vazia.
- **Manter a sintaxe atual** manterá a sintaxe original.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Manter a sintaxe atual|
|Otimistas|Manter a sintaxe atual|
|Completo|Encapsular com a função ISNULL|

### <a name="conversion-of-empty-strings"></a>Conversão de cadeias de caracteres vazias

Essa configuração especifica como converter cadeias de caracteres vazias. As opções a seguir podem ser definidas para essa configuração específica:

- **Substituir todas as expressões de cadeia de caracteres por espaço**
- **Substituir constantes de cadeia de caracteres vazias por espaço**

Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comportamento do SQL/Azure, selecione **manter a sintaxe atual**.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Manter a sintaxe atual|
|Otimistas|Manter a sintaxe atual|
|Completo|Substituir todas as expressões de cadeia de caracteres por espaço|

### <a name="convert-and-cast-binary-string-conversion"></a>CONVERTER e transmitir conversão de cadeia de caracteres binária

A conversão de valores binários em números pode retornar valores diferentes em plataformas diferentes. Por exemplo, em processadores x86, `CONVERT(integer, 0x00000100)` retorna `65536` no ASE, mas `256` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O ASE também retorna valores diferentes, dependendo da ordem de byte.

Use essa configuração para controlar como o SSMA converte `CONVERT` e `CAST` expressões que contêm valores binários:

- Selecione **conversão simples** para converter as expressões sem avisos ou correções. Use essa configuração se você souber que o servidor ASE tem uma ordem de bytes que não requer nenhuma alteração do valor binário.
- Selecione **converter e corrigir** para que o SSMA converta e corrija as expressões para uso em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A ordem de bytes em constantes literais será revertida. Todos os outros valores binários (como variáveis e colunas binárias) serão marcados com erros. Use esse valor se você souber que o servidor ASE tem uma ordem de bytes que requer alterações em valores binários.

Selecione **converter e marcar com aviso** para que o SSMA converta e corrija as expressões e marque todas as expressões convertidas com comentários de aviso.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Converter e marcar com aviso|
|Otimistas|Conversão simples|
|Completo|Converter e corrigir|

### <a name="dynamic-sql"></a>SQL dinâmico

Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que o SSMA mostra no painel de **saída** ou de **lista de erros** quando encontrar SQL dinâmico no código do ase.

- Se você selecionar **converter e marcar com aviso**, o SSMA converterá o SQL dinâmico e marcará as instruções com comentários de aviso.
- Se você selecionar **marcar com erro**, o SSMA ignorará a conversão e marcará as instruções com comentários de erro.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Converter e marcar com aviso|
|Otimistas|Converter e marcar com aviso|
|Completo|Marcar com erro|

### <a name="equality-check-conversion"></a>Conversão de verificação de igualdade

No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL, se a `ANSI_NULLS` configuração estiver ativada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL retornará `UNKNOWN` quando qualquer comparação de igualdade contiver um `NULL` valor. Se `ANSI_NULLS` for off, as comparações de igualdade que contêm `NULL` valores retornarão true quando a coluna comparada e a expressão ou duas expressões forem ambas `NULL` . Por padrão ( `ANSINULL OFF` ) as comparações de igualdade do SAP ASE se comportam como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL com `ANSI_NULLS OFF` .

- Se você selecionar **conversão simples**, o SSMA converterá o código do ase em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe SQL/Azure sem verificações adicionais de `NULL` valores. Use essa configuração se `ANSI_NULLS` estiver `OFF` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL/Azure ou se você quiser revisar comparações de igualdade de acordo com cada caso.
- Se você selecionar **considerar valores nulos**, o SSMA adicionará verificações de `NULL` valores usando `IS NULL` as `IS NOT NULL` cláusulas e.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Conversão simples|
|Otimistas|Conversão simples|
|Completo|Considerar valores nulos|

### <a name="format-strings"></a>Formatar cadeias de caracteres

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O/Azure SQL não dá mais suporte ao `format_string` argumento nas `PRINT` `RAISERROR` instruções e. O `format_string` argumento permitiu colocar parâmetros substituíveis diretamente na cadeia de caracteres e, em seguida, substituir os parâmetros em tempo de execução. Em vez disso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o requer a cadeia de caracteres completa usando um literal de cadeia de caracteres ou uma cadeia de caracteres criada usando uma variável. Para obter mais informações, consulte o tópico [Print ( [!INCLUDE[tsql](../../includes/tsql-md.md)] )](../../t-sql/language-elements/print-transact-sql.md) .

Quando o SSMA encontra um `format_string` argumento, ele pode criar um literal de cadeia de caracteres usando as variáveis ou criar uma nova variável e criar uma cadeia de caracteres usando essa variável.

- Para usar um literal de cadeia de caracteres para `PRINT` `RAISERROR` funções e, selecione **criar nova cadeia de caracteres**.

    Nesse modo, se uma instrução PRINT ou RAISERROR não usar espaços reservados e variáveis locais, a instrução será inalterada. Caracteres de porcentagem duplas (%%) são alterados para um caractere de porcentagem única em literais de cadeia de caracteres de impressão.

    Se uma instrução PRINT ou RAISERROR usar espaços reservados e uma ou mais variáveis locais, como no exemplo a seguir:

    ```sql
    PRINT 'Total: %1!%%', @percent
    ```

    O SSMA irá convertê-lo para a seguinte sintaxe:

    ```sql
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'
    ```

    Se `format_string` é uma variável, como na seguinte instrução:  

    ```sql
    PRINT @fmt, @arg1, @arg2
    ```

    O SSMA não pode fazer uma conversão de cadeia de caracteres simples e deve criar uma nova variável:

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 =
        REPLACE (@fmt, '%%', '%')
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        CAST (@arg1 AS varchar(max)))
    SET @print_format_1 =
        REPLACE (@print_format_1, '%2!',
        CAST (@arg2 AS varchar(max)))
    PRINT @print_format_1
    ```

    Quando ele usa **criar novo** modo de cadeia de caracteres, o SSMA pressupõe que a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opção `CONCAT_NULL_YIELDS_NULL` é `OFF` . Portanto, o SSMA não verifica argumentos nulos.

- Para que o SSMA crie uma nova variável para `PRINT` cada `RAISERROR` instrução e, em seguida, use essa variável para o valor da cadeia de caracteres, selecione **criar nova variável**.

    Nesse modo, se uma `PRINT` instrução ou não `RAISERROR` usar espaços reservados e variáveis locais, o SSMA substituirá todos os caracteres de porcentagem duplas ( `%%` ) por um único caractere de porcentagem para estar em conformidade com a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe SQL/Azure.

    Se uma `PRINT` `RAISERROR` instrução ou usar espaços reservados e uma ou mais variáveis locais, como no exemplo a seguir:

    ```sql
    PRINT 'Total: %1!%%', @percent
    ```

    O SSMA irá convertê-lo para a seguinte sintaxe:

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 = 'Total: %1!%'
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))
    PRINT @print_format_1
    ```

    Se `format_string` é uma variável, como na seguinte instrução:

    ```sql
    PRINT @fmt, @arg1, @arg2
    ```

    O SSMA cria uma nova variável da seguinte maneira, verificando valores nulos em cada argumento:

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 =
        REPLACE (@fmt, '%%', '%')
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        ISNULL(CAST (@arg1 AS varchar(max)),''))
    SET @print_format_1 =
        REPLACE (@print_format_1, '%2!',
        ISNULL(CAST (@arg2 AS varchar(max)),''))
    PRINT @print_format_1
    ```

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Criar nova cadeia de caracteres|
|Otimistas|Criar nova cadeia de caracteres|
|Completo|Criar nova variável|

### <a name="insert-an-explicit-value-into-a-timestamp-column"></a>Inserir um valor explícito em uma coluna de carimbo de data/hora

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL não dá suporte à inserção de valores explícitos em uma coluna timestamp.

- Para excluir colunas de carimbo de data/hora das `INSERT` instruções, selecione **Excluir coluna**.
- Para imprimir uma mensagem de erro toda vez que uma coluna de carimbo de data/hora estiver em uma `INSERT` instrução, selecione **marcar com erro**. Nesse modo, as `INSERT` instruções não serão convertidas e serão marcadas com comentários de erro.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Excluir coluna|
|Otimistas|Excluir coluna|
|Completo|Marcar com erro|

### <a name="store-temporary-objects-defined-in-procedures"></a>Armazenar objetos temporários definidos em procedimentos

Essa configuração especifica se as definições de objetos temporários que aparecem nos procedimentos devem ser armazenadas nos metadados de origem durante a conversão.

- Selecione **Sim** para armazenar em metadados.
- Selecione **não** se os objetos não precisarem ser armazenados.

|Mode|Valor|
|-|-|
|Padrão|Sim|
|Otimistas|Sim|
|Completo|Não|

### <a name="proxy-table-conversion"></a>Conversão de tabela de proxy

Especifica se as tabelas proxy do ASE são convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas SQL/Azure ou não são convertidas e o código é marcado com comentários de erro.

- Selecione **converter** para converter tabelas de proxy em tabelas regulares.
- Selecione **marcar com erro** para simplesmente marcar o código da tabela proxy com comentários de erro.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Marcar com erro|
|Otimistas|Marcar com erro|
|Completo|Marcar com erro|

### <a name="raiserror-base-message-number"></a>Número da mensagem base RAISERROR

As mensagens de usuário do ASE são armazenadas em cada banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as mensagens de usuário são armazenadas centralmente e disponibilizadas por meio da `sys.messages` exibição de catálogo. Além disso, as mensagens de usuário do ASE iniciam em `20000` , mas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as mensagens de erro iniciam em `50001` .

Essa configuração especifica o número a ser adicionado ao número de mensagem de usuário do ASE para convertê-lo em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem de usuário. Se seu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver mensagens de usuário na `sys.messages` exibição de catálogo, talvez seja necessário alterar esse número para um valor mais alto. Isso é para que os números de mensagem convertidos não entrem em conflito com os números de mensagem existentes.

Observe o seguinte:
  
- As mensagens do ase no intervalo `17000` - `19999` são da `sysmessages` tabela do sistema e não são convertidas.
- Se o número da mensagem referenciado na `RAISERROR` instrução for uma constante, o SSMA adicionará o número da mensagem base à constante para determinar o novo número da mensagem de usuário.
- Se o número da mensagem referenciado for uma variável ou expressão, o SSMA criará uma variável local intermediária.
- No **modo otimista**, o SSMA pressupõe que a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opção `CONCAT_NULL_YIELDS_NULL` é `OFF` e não faz nenhuma verificação de `NULL` argumentos.
- No **modo completo**, o SSMA verifica os `NULL` argumentos.
- `RAISERROR` o `arg-list` argumento with não é convertido.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|30001|
|Otimistas|30001|
|Completo|30001|

### <a name="system-objects"></a>Objetos do sistema

Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que o SSMA mostra no painel de **saída** ou de **lista de erros** quando encontra o uso de objetos do sistema ASE.

- Se você selecionar **converter e marcar com aviso**, o SSMA converterá as referências a objetos do sistema e marcará as instruções com comentários de aviso.
- Se você selecionar **marcar com erro**, o SSMA não converterá referências a objetos de sistemas e marcará instruções com comentários de erro.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Converter e marcar com aviso|
|Otimistas|Converter e marcar com aviso|
|Completo|Marcar com erro|

### <a name="unresolved-identifiers"></a>Identificadores não resolvidos

Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que o SSMA mostra no painel de **saída** ou de **lista de erros** quando ele não puder resolver um identificador.

- Se você selecionar **converter e marcar com aviso**, o SSMA tentará converter referências em identificadores não resolvidos e marcará as instruções com comentários de aviso.
- Se você selecionar **marcar com erro**, o SSMA não converterá as referências a identificadores não resolvidos e marcará as instruções com comentários de erro.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Converter e marcar com aviso|
|Otimistas|Converter e marcar com aviso|
|Completo|Marcar com erro|

## <a name="system-functions-section"></a>Seção funções do sistema

### <a name="charindex-function"></a>função CHARINDEX 

No ASE, `CHARINDEX` retorna `NULL` somente se todas as expressões de entrada forem `NULL` . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL retornará `NULL` se alguma expressão de entrada for `NULL` .

- Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a `CHARINDEX` função são substituídas por uma chamada para uma `CHARINDEX_VARCHAR`  `CHARINDEX_NVARCHAR` função definida pelo ou pelo usuário com base no tipo de parâmetros passado (criado no banco de dados de usuário sob o nome do esquema `s2ss` ) para emular o comportamento do SAP ASE.
- Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comportamento do SQL/Azure, selecione **manter a sintaxe atual**.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Manter a sintaxe atual|
|Otimistas|Manter a sintaxe atual|
|Completo|Função Replace|
  
### <a name="datalength-function"></a>função DATALENGTH

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL e ASE diferem no valor retornado pela `DATALENGTH` função quando o valor é um único espaço. Nesse caso, retornos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL `0` e ase retornam `1` .

- Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a `DATALENGTH` função são substituídas por uma `CASE` expressão para emular o comportamento do SAP ASE.
- Para usar o comportamento padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL/Azure, selecione **manter a sintaxe atual**.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Manter a sintaxe atual|
|Otimistas|Manter a sintaxe atual|
|Completo|Função Replace|

### <a name="index_col-function"></a>função INDEX_COL

O ASE dá suporte a um `user_id` argumento opcional para a `INDEX_COL` função; no entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL não dá suporte a esse argumento. Se você usar o `user_id` argumento, essa função não poderá ser convertida em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe SQL/Azure.

- Para usar o comportamento do ASE, selecione **converter função**. Se o código contiver o `user_id` argumento, o SSMA exibirá um erro.
- Para exibir uma mensagem de erro toda vez que `INDEX_COL` for encontrada, selecione **marcar com erro**. O SSMA não converterá referências para a função e marcará a instrução com comentários de erro.

|Mode|Valor|
|-|-|
|Padrão|Marcar com erro|
|Otimistas|Marcar com erro|
|Completo|Marcar com erro|

### <a name="index_colorder-function"></a>Função INDEX_COLORDER

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL não tem uma `INDEX_COLORDER` função de sistema.

- Para usar o comportamento do ASE, selecione **converter função**. Todas as chamadas para a `INDEX_COLORDER` função são substituídas por uma chamada para uma função definida pelo usuário com o mesmo nome `INDEX_COLORDER` (criado no banco de dados de usuário sob o nome do esquema `s2ss` ) que emula o comportamento do SAP ASE.
- Para imprimir uma mensagem de erro toda vez que `INDEX_COLORDER` for encontrada, selecione **marcar com erro**. O SSMA não converterá referências para a função e marcará a instrução com comentários de erro.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Marcar com erro|
|Otimistas|Marcar com erro|
|Completo|Marcar com erro|

### <a name="left-and-right-functions"></a>Funções esquerda e direita

`LEFT` as `RIGHT` funções e no ASE se comportam de forma diferente para o parâmetro de comprimento negativo.

- Para usar o comportamento do ASE, selecione **substituir função**. O parâmetro length é substituído por uma `CASE` expressão que retornaria um `NULL` valor negativo.
- Para usar o comportamento de SQL Server, selecione **manter a sintaxe atual**.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Manter a sintaxe atual|
|Otimistas|Manter a sintaxe atual|
|Completo|Função Replace|

> [!NOTE]
> Se o parâmetro de comprimento for um valor literal e não uma expressão complexa, o valor de comprimento será sempre substituído, `NULL` independentemente da configuração do projeto.

### <a name="next_identity-function"></a>Função NEXT_IDENTITY

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL não tem uma `NEXT_IDENTITY` função de sistema.

- Para usar o comportamento do ASE, selecione **converter função**. Todas as chamadas para `NEXT_IDENTITY` Function são substituídas por `(IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value)` uma expressão que emula o comportamento do SAP ASE.
- Para imprimir uma mensagem de erro toda vez que `NEXT_IDENTITY` for encontrada, selecione **marcar com erro**. O SSMA não converterá referências para a função e marcará a instrução com comentários de erro.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Marcar com erro|
|Otimistas|Marcar com erro|
|Completo|Marcar com erro|

**Modo padrão/otimista/completo:** Marcar com erro

### <a name="patindex-function"></a>função PATINDEX

Especifica se a função deve ser convertida `PATINDEX` para corresponder ao comportamento do SAP ASE. O ponto é que o ASE corta os espaços em branco à direita em um padrão de pesquisa. A solução alternativa é fazer uma conversão de expressão de valor em um tipo de dados de comprimento fixo com uma precisão máxima e aplicar `rtrim` a função ao padrão de pesquisa.

- Para usar o comportamento do ASE, selecione **usar**.  
- Para usar o comportamento padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL/Azure, selecione **não usar**.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Não usar|
|Otimistas|Não usar|
|Completo|Use|

### <a name="replicate-function"></a>função REPLICATE

A `REPLICATE` função repete uma cadeia de caracteres o número especificado de vezes. No ASE, se você especificar para repetir a cadeia de caracteres zero vezes, o resultado será `NULL` . No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL/Azure, o resultado é uma cadeia de caracteres vazia.

- Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a `REPLICATE` função são substituídas por uma chamada para uma `REPLICATE_VARCHAR` `REPLICATE_NVARCHAR` função definida pelo ou pelo usuário com base no tipo de parâmetros passado (criado no banco de dados de usuário sob o nome do esquema `s2ss` ) para emular o comportamento do SAP ASE.
- Para usar o comportamento padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL/Azure, selecione **substituir função**.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Função Replace|
|Otimistas|Função Replace|
|Completo|Função Replace|

### <a name="trim-ltrim-rtrim-function"></a>Função TRIM (LTRIM, RTRIM)

Essa configuração especifica se as chamadas devem ser substituídas `TRIM` `LTRIM` e `RTRIM` as funções com as funções de sintaxe equivalentes do SAP ase ou para manter a sintaxe atual. As seguintes opções estão presentes para essa configuração específica:

- **Função Replace**
- **Manter a sintaxe atual**

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Função Replace|
|Otimistas|Função Replace|
|Completo|Função Replace|

### <a name="substring-function"></a>função SUBSTRING

No ASE, a função `SUBSTRING(expression, start, length)` retorna `NULL` se um valor inicial maior que o número de caracteres na expressão for especificado ou se length for igual a zero. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL/Azure, a expressão equivalente retorna uma cadeia de caracteres vazia.

- Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para `SUBSTRING` Function são substituídas por uma chamada para `SUBSTRING_VARCHAR` ou `SUBSTRING_NVARCHAR` ou `SUBSTRING_VARBINARY` função definida pelo usuário com base no tipo de parâmetros passado (criado no banco de dados do usuário sob o nome do esquema `s2ss` ) para EMULAR o comportamento do SAP ASE.
- Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comportamento do SQL/Azure, selecione **manter a sintaxe atual**.

Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:

|Mode|Valor|
|-|-|
|Padrão|Manter a sintaxe atual|
|Otimistas|Manter a sintaxe atual|
|Completo|Função Replace|

## <a name="tables-section"></a>Seção de tabelas

### <a name="add-primary-key"></a>Adicionar chave primária

Cria uma nova chave primária na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela do ou SQL do Azure se uma tabela do SAP ase não tiver nenhuma chave primária ou índice exclusivo.

|Mode|Valor|
|-|-|
|Padrão|Não|
|Otimistas|Não|
|Completo|Sim|

> [!NOTE]
> Quando conectado ao SQL do Azure, é **Sim** por padrão.

## <a name="see-also"></a>Consulte Também

[Referência da interface do usuário (SybaseToSQL)](../../ssma/sybase/user-interface-reference-sybasetosql.md)
