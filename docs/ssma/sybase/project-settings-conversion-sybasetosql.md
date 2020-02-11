---
title: Configurações do projeto (conversão) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5d4936638fc9e283caafffc2f2a7cfdbed396920
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028758"
---
# <a name="project-settings-conversion-sybasetosql"></a>Configurações do projeto (conversão) (SybaseToSQL)
A página conversão da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA converte a sintaxe do Sybase Adaptive Server Enterprise [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ASE) em ou SQL Azure sintaxe.  
  
O painel de conversão está disponível nas caixas de diálogo **configurações do projeto** e **configurações padrão do projeto** :  
  
-   Se você quiser especificar configurações para todos os projetos do SSMA, no menu **ferramentas** , selecione **configurações de projeto padrão**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **conversão**.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **conversão**.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure e ASE usam códigos de erro diferentes.  
  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que o SSMA mostra no painel de saída ou de lista de erros quando encontra uma referência **a@ERROR @** no código do ase.  
  
-   Se você selecionar **converter e marcar com aviso**, o SSMA converterá as instruções e as marcará com comentários de aviso.  
  
-   Se você selecionar **marcar com erro**, o SSMA ignorará a conversão e marcará as instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Converter e marcar com aviso  
  
**Modo completo:** Marcar com erro  
  
**Conversão de operador LIKE**  
Especifica se os operandos LIKE devem ser convertidos para corresponder ao comportamento de ASE do Sybase. A questão é que o Sybase corta os espaços em branco à direita em um padrão semelhante. A solução alternativa é fazer uma conversão da expressão direita em um tipo de dados de comprimento fixo com precisão máxima.  
  
-   Selecione **conversão simples** para converter as expressões sem qualquer correção.  
  
-   Para usar o comportamento do ASE, selecione **conversão para comprimento fixo.**  
  
Quando você seleciona um modo de conversão na caixa modo, o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista**: conversão simples  
  
**Modo completo**: conversão em comprimento fixo  
  
**CONVERSÃO OU CONVERSÃO DE CADEIAS DE CARACTERES VAZIAS EM TIPOS NUMÉRICOS**  
Especifica como tratar cadeias de caracteres vazias ou em branco dentro de expressões CONVERT ou CAST com o tipo numeric como argumento DataType. As seguintes opções estão disponíveis para essa configuração:  
  
-   Selecione **conversão simples** para converter as expressões sem qualquer correção.  
  
-   Se **a cadeia de caracteres vazia como zero numeric** for selecionada, o parâmetro de cadeia de caracteres {s} será substituído pelo caso LTRIM (rtrim ({s})) quando for "", 0 else {s} End Expression  
  
Quando você seleciona um modo de conversão na caixa modo, o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista**: conversão simples  
  
**Modo completo**: cadeia de caracteres vazia como zero numérico  
  
**Concatenação de NULL**  
Essa configuração especifica como converter a concatenação de cadeia de caracteres com NULL. As opções a seguir podem ser definidas para essa configuração específica:  
  
-   **Encapsular com a função ISNULL:** Se essa opção for definida, cada ' string_expression ' não constante na concatenação será encapsulado com ISNULL (string_expression) e os valores nulos serão substituídos por uma cadeia de caracteres vazia.  
  
-   **Manter a sintaxe atual**  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Encapsular com a função ISNULL  
  
**Conversão de cadeias de caracteres vazias**  
Essa configuração especifica como converter cadeias de caracteres vazias. As opções a seguir podem ser definidas para essa configuração específica:  
  
-   **Substituir todas as expressões de cadeia de caracteres por espaço**  
  
-   **Substituir constantes de cadeia de caracteres vazias por espaço**  
  
-   Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]comportamento/SQL Azure, selecione **manter a sintaxe atual**.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Substituir todas as expressões de cadeia de caracteres por espaço  
  
**CONVERTER e transmitir conversão de cadeia de caracteres binária**  
A conversão de valores binários em números pode retornar valores diferentes em plataformas diferentes. Por exemplo, em processadores x86, CONVERTa (Integer, 0x00000100) retorna 65536 no ASE e 256 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no. O ASE também retorna valores diferentes, dependendo da ordem de byte.  
  
Use essa configuração para controlar como o SSMA converte as expressões CONVERT e CASE que contêm valores binários:  
  
-   Selecione **conversão simples** para converter as expressões sem avisos ou correções. Use essa configuração se você souber que o servidor ASE tem uma ordem de bytes que não requer nenhuma alteração do valor binário.  
  
-   Selecione **converter e corrigir** para que o SSMA converta e corrija as expressões para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]uso em. A ordem de bytes em constantes literais será revertida. Todos os outros valores binários (como variáveis e colunas binárias) serão marcados com erros. Use esse valor se você souber que o servidor ASE tem uma ordem de bytes que requer alterações em valores binários.  
  
-   Selecione **converter e marcar com aviso** para que o SSMA converta e corrija as expressões e marque todas as expressões convertidas com comentários de aviso.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão:** Converter e marcar com aviso  
  
**Modo otimista:** Conversão simples  
  
**Modo completo:** Converter e corrigir  
  
**SQL dinâmico**  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que o SSMA mostra no painel de saída ou de Lista de Erros quando encontrar SQL dinâmico no código do ASE.  
  
-   Se você selecionar **converter e marcar com aviso**, o SSMA converterá o SQL dinâmico e marcará as instruções com comentários de aviso.  
  
-   Se você selecionar **marcar com erro**, o SSMA ignorará a conversão e marcará as instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Converter e marcar com aviso  
  
**Modo completo:** Marcar com erro  
  
**Conversão de verificação de igualdade**  
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure, se a configuração de ANSI_NULLS estiver ativada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure retornará desconhecido quando qualquer comparação de igualdade contiver um valor nulo. Se ANSI_NULLS for off, as comparações de igualdade que contêm valores nulos retornarão true quando a coluna comparada e a expressão ou duas expressões forem nulas. Por padrão (ANSINULL OFF), as comparações de igualdade [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de ase do Sybase se comportam como/SQL Azure com ANSI_NULLS desativado.  
  
-   Se você selecionar **conversão simples**, o SSMA converterá o código do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ASE em/SQL Azure sintaxe sem verificações adicionais para valores nulos. Use essa configuração se ANSI_NULLS estiver desativada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure ou se desejar revisar comparações de igualdade de acordo com cada caso.  
  
-   Se você selecionar **considerar valores nulos**, o SSMA adicionará verificações de valores nulos usando as cláusulas is NULL e is NOT NULL.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Conversão simples  
  
**Modo completo:** Considerar valores nulos  
  
**Formatar cadeias de caracteres**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure não dá mais suporte ao argumento *FORMAT_STRING* nas instruções Print e RAISERROR. A variável *FORMAT_STRING* com suporte para colocar parâmetros substituíveis diretamente na cadeia de caracteres e, em seguida, substituir os parâmetros em tempo de execução. Em vez [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disso, o requer a cadeia de caracteres completa usando um literal de cadeia de caracteres ou uma cadeia de caracteres criada usando uma variável. Para obter mais informações, consulte o tópico " [!INCLUDE[tsql](../../includes/tsql-md.md)]imprimir ()" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos manuais online do.  
  
Quando o SSMA encontra um argumento *FORMAT_STRING* , ele pode criar um literal de cadeia de caracteres usando as variáveis ou criar uma nova variável e criar uma cadeia de caracteres usando essa variável.  
  
-   Para usar um literal de cadeia de caracteres para funções de impressão e RAISERROR, selecione **criar nova cadeia de caracteres**.  
  
    Nesse modo, se uma instrução PRINT ou RAISERROR não usar espaços reservados e variáveis locais, a instrução será inalterada. Caracteres de porcentagem duplas (%%) são alterados para um caractere de porcentagem única em literais de cadeia de caracteres de impressão.  
  
    Se uma instrução PRINT ou RAISERROR usar espaços reservados e uma ou mais variáveis locais, como no exemplo a seguir:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    O SSMA irá convertê-lo para a seguinte sintaxe:  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    Se *FORMAT_STRING* for uma variável, como na seguinte instrução:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    O SSMA não pode fazer uma conversão de cadeia de caracteres simples e deve criar uma nova variável:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        CAST (@arg1 AS varchar(max)))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        CAST (@arg2 AS varchar(max)))  
    PRINT @print_format_1  
    ```  
    Quando ele usa **criar novo** modo de cadeia de caracteres, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA pressupõe que a opção CONCAT_NULL_YIELDS_NULL está desativada. Portanto, o SSMA não verifica argumentos nulos.  
  
-   Para que o SSMA crie uma nova variável para cada instrução PRINT e RAISERROR e, em seguida, use essa variável para o valor da cadeia de caracteres, selecione **criar nova variável**.  
  
    Nesse modo, se uma instrução PRINT ou RAISERROR não usar espaços reservados e variáveis locais, o SSMA substituirá todos os caracteres de porcentagem duplas (%%) com caracteres de porcentagem única para obedecer à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sintaxe/SQL Azure.  
  
    Se uma instrução PRINT ou RAISERROR usar espaços reservados e uma ou mais variáveis locais, como no exemplo a seguir:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    O SSMA irá convertê-lo para a seguinte sintaxe:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    Se *FORMAT_STRING* for uma variável, como na seguinte instrução:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    O SSMA cria uma nova variável da seguinte maneira, verificando valores nulos em cada argumento:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@arg1 AS varchar(max)),''))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        ISNULL(CAST (@arg2 AS varchar(max)),''))  
    PRINT @print_format_1  
    ```  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Criar nova cadeia de caracteres  
  
**Modo completo:** Criar nova variável  
  
**Inserir um valor explícito em uma coluna de carimbo de data/hora**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure não oferece suporte à inserção de valores explícitos em uma coluna de carimbo de data/hora.  
  
-   Para excluir colunas de carimbo de data/hora das instruções INSERT, selecione **Excluir coluna**.  
  
-   Para imprimir uma mensagem de erro toda vez que uma coluna de carimbo de data/hora estiver em uma instrução INSERT, selecione **marcar com erro**. Nesse modo, as instruções INSERT não serão convertidas e serão marcadas com comentários de erro.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Excluir coluna  
  
**Modo completo:** Marcar com erro  
  
**Armazenar objetos temporários definidos em procedimentos**  
Essa configuração especifica se as definições de objetos temporários que aparecem nos procedimentos devem ser armazenadas nos metadados de origem durante a conversão.  
  
-   Selecione **Sim** para armazenar em metadados.  
  
-   Selecione **não** se os objetos não precisarem ser armazenados.  
  
**Modo padrão/otimista:** Ok  
  
**Modo completo:** Não  
  
**Conversão de tabela de proxy**  
Especifica se as tabelas proxy do ASE são [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]convertidas em/SQL Azure tabelas ou não são convertidas e o código é marcado com comentários de erro.  
  
-   Selecione **converter** para converter tabelas de proxy em tabelas regulares.  
  
-   Selecione **marcar com erro** para simplesmente marcar o código da tabela proxy com comentários de erro.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Marcar com erro  
  
**Número da mensagem base RAISERROR**  
As mensagens de usuário do ASE são armazenadas em cada banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]as mensagens do usuário são armazenadas centralmente e disponibilizadas por meio da exibição do catálogo **Sys. messages** . Além disso, as mensagens de usuário do ASE começam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] às 20000, mas as mensagens de erro começam em 50001.  
  
Essa configuração especifica o número a ser adicionado ao número de mensagem de usuário do ASE para convertê-lo em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem de usuário. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seu tiver mensagens de usuário na exibição de catálogo **Sys. messages** , talvez seja necessário alterar esse número para um valor mais alto. Isso é para que os números de mensagem convertidos não entrem em conflito com os números de mensagem existentes.  
  
Observe o seguinte:  
  
-   As mensagens do ASE no intervalo de 17000-19999 são da tabela do sistema sysmessages e não são convertidas.  
  
-   Se o número da mensagem referenciado na instrução RAISERROR for uma constante, o SSMA adicionará o número da mensagem base à constante para determinar o novo número da mensagem de usuário.  
  
-   Se o número da mensagem referenciado for uma variável ou expressão, o SSMA criará uma variável local intermediária.  
  
-   No modo otimista, o SSMA pressupõe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a opção CONCAT_NULL_YIELDS_NULL está desativada e não faz nenhuma verificação de argumentos nulos.  
  
-   No modo completo, o SSMA verifica argumentos nulos.  
  
-   RAISERROR com *lista* de ERRORDATA não é convertido.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** 30001  
  
**Objetos do sistema**  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que o SSMA mostra no painel de saída ou de Lista de Erros quando encontra o uso de objetos do sistema ASE.  
  
-   Se você selecionar **converter e marcar com aviso**, o SSMA converterá as referências a objetos do sistema e marcará as instruções com comentários de aviso.  
  
-   Se você selecionar **marcar com erro**, o SSMA não converterá referências a objetos de sistemas e marcará instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Converter e marcar com aviso  
  
**Modo completo:** Marcar com erro  
  
**Identificadores não resolvidos**  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que o SSMA mostra no painel de saída ou de Lista de Erros quando ele não puder resolver um identificador.  
  
-   Se você selecionar **converter e marcar com aviso**, o SSMA tentará converter referências em identificadores não resolvidos e marcará as instruções com comentários de aviso.  
  
-   Se você selecionar **marcar com erro**, o SSMA não converterá as referências a identificadores não resolvidos e marcará as instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Converter e marcar com aviso  
  
**Modo completo:** Marcar com erro  
  
## <a name="system-function-options"></a>Opções de função do sistema  
**função CHARINDEX **  
No ASE, CHARINDEX retornará NULL somente se todas as expressões de entrada forem nulas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure retornará NULL se qualquer expressão de entrada for nula.  
  
-   Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a função CHARINDEX são substituídas por uma chamada para CHARINDEX_VARCHAR ou CHARINDEX_NVARCHAR função definida pelo usuário com base no tipo de parâmetros passados (criados no banco de dados de usuário sob o 2SS ' s do nome do esquema ') para emular o comportamento do ASE do Sybase.  
  
-   Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]comportamento/SQL Azure, selecione **manter a sintaxe atual**.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Função Replace  
  
**função DATALENGTH**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure e ASE diferem no valor retornado pela função DATALENGTH quando o valor é um único espaço. Nesse caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure retorna 0 e ase retorna 1.  
  
-   Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a função DATALENGTH são substituídas por uma expressão CASE para emular o comportamento de ASE do Sybase.  
  
-   Para usar o comportamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] padrão/SQL Azure, selecione **manter a sintaxe atual**.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Função Replace  
  
**função INDEX_COL**  
O ASE dá suporte a um argumento opcional *user_id* para a função INDEX_COL; no entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure não oferece suporte a esse argumento. Se você usar o argumento *user_id* , essa função não poderá ser convertida em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure sintaxe.  
  
-   Para usar o comportamento do ASE, selecione **converter função**. Se o código contiver o argumento *user_id* , o SSMA exibirá um erro.  
  
-   Para exibir uma mensagem de erro toda vez que INDEX_COL for encontrado, selecione **marcar com erro**. O SSMA não converterá referências para a função e marcará a instrução com comentários de erro.  
  
**Modo padrão/otimista/completo:** Marcar com erro  
  
**Função INDEX_COLORDER**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure não tem uma função de sistema INDEX_COLORDER.  
  
-   Para usar o comportamento do ASE, selecione **converter função**. Todas as chamadas para INDEX_COLORDER função são substituídas por uma chamada para uma função definida pelo usuário com o mesmo nome INDEX_COLORDER (criado no banco de dados do usuário sob o 2SS ' s do nome do esquema) que emula o comportamento de ASE do Sybase.  
  
-   Para imprimir uma mensagem de erro toda vez que INDEX_COLORDER for encontrado, selecione **marcar com erro**. O SSMA não converterá referências para a função e marcará a instrução com comentários de erro.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Marcar com erro  
  
**Funções esquerda e direita**  
As funções Left e Right no Sybase se comportam de forma diferente para o parâmetro de comprimento negativo.  
  
-   Para usar o comportamento do ASE, selecione **substituir função**. O parâmetro length é substituído por uma expressão CASE que retornaria NULL para um valor negativo.  
  
-   Para usar o comportamento de SQL Server, selecione **manter a sintaxe atual**  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Função Replace  
  
> [!NOTE]  
> Se o parâmetro length for um valor literal e não uma expressão complexa, o valor de comprimento será sempre substituído por NULL, independentemente da configuração do projeto.  
  
**Função NEXT_IDENTITY**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure não tem uma função de sistema NEXT_IDENTITY.  
  
-   Para usar o comportamento do ASE, selecione **converter função**. Todas as chamadas para NEXT_IDENTITY função são substituídas por uma expressão (IDENT_CURRENT (valor do parâmetro) + IDENT_INCR (valor do parâmetro) que emula o comportamento de ASE do Sybase.  
  
-   Para imprimir uma mensagem de erro toda vez que NEXT_IDENTITY for encontrado, selecione **marcar com erro**. O SSMA não converterá referências para a função e marcará a instrução com comentários de erro.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista/completo:** Marcar com erro  
  
**função PATINDEX**  
Especifica se a função PATINDEX deve ser convertida para corresponder ao comportamento de ASE do Sybase. A questão é que o Sybase corta os espaços em branco à direita em um padrão de pesquisa. A solução alternativa é fazer uma conversão de expressão de valor em um tipo de dados de comprimento fixo com precisão máxima e aplicar a função RTrim ao padrão de pesquisa.  
  
-   Para usar o comportamento do ASE, selecione **usar**.  
  
-   Para usar o comportamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]padrão/SQL Azure, selecione **não usar**.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Não usar  
  
**Modo completo:** Utilizá  
  
**função REPLICATE**  
A função REPLICAte repete uma cadeia de caracteres do número de vezes especificado. No ASE, se você especificar para repetir a cadeia de caracteres zero vezes, o resultado será nulo. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure, o resultado é uma cadeia de caracteres vazia.  
  
-   Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a função REPLICAte são substituídas por uma chamada para REPLICATE_VARCHAR ou REPLICATE_NVARCHAR função definida pelo usuário com base no tipo de parâmetros passados (criados no banco de dados do usuário sob o 2SS ' s do nome do esquema) para emular o comportamento de ASE do Sybase.  
  
-   Para usar o comportamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]padrão/SQL Azure, selecione **substituir função**.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
Modo **padrão/otimista/modo completo:** Função Replace  
  
**Função TRIM (LTRIM, RTRIM)**  
Essa configuração especifica se as chamadas para as funções Trim (LTRIM, RTRIM) devem ser substituídas pelas funções de sintaxe do Sybase ASE-equivalente ou para manter a sintaxe atual. As seguintes opções estão presentes para essa configuração específica:  
  
-   **Função Replace**  
  
-   **Manter a sintaxe atual**  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
Modo **padrão/otimista/modo completo:** Função Replace  
  
**função SUBSTRING**  
No ASE, a função `SUBSTRING(expression, start, length)` retornará NULL se um valor inicial maior que o número de caracteres na expressão for especificado ou se length for igual a zero. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure, a expressão equivalente retorna uma cadeia de caracteres vazia.  
  
-   Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a função substring são substituídas por uma chamada para SUBSTRING_VARCHAR ou SUBSTRING_NVARCHAR ou SUBSTRING_VARBINARY função definida pelo usuário com base no tipo de parâmetros passados (criado no banco de dados do usuário sob o 2SS ' s do nome do esquema) para emular o Comportamento do Sybase ASE.  
  
-   Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comportamento/SQL Azure, selecione **manter a sintaxe atual**.  
  
Quando você seleciona um modo de conversão na caixa **modo** , o SSMA aplica a seguinte configuração:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Função Replace  
  
## <a name="tables"></a>TABLES  
**Adicionar chave primária**  
Cria uma nova chave primária na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure se uma tabela de acesso não tiver nenhuma chave primária ou índice exclusivo.  
  
-   **Modo padrão**: false  
  
-   **Modo otimista**: false  
  
-   **Modo completo**: verdadeiro  
  
> [!NOTE]  
> Quando conectado a SQL Azure, ele é true padrão.  
  
## <a name="see-also"></a>Consulte Também  
[Referência da interface do usuário &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
