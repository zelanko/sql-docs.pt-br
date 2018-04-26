---
title: Configurações (conversão) (SybaseToSQL) do projeto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffffc3badb8d65d5809e293e0c1ffb526409e4a9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="project-settings-conversion-sybasetosql"></a>Configurações de projeto (conversão) (SybaseToSQL)
A página de conversão do **configurações de projeto** caixa de diálogo contém configurações que personalizam como o SSMA converte a sintaxe do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL Azure.  
  
O painel de conversão está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo:  
  
-   Se você deseja especificar as configurações para todos os projetos do SSMA, no **ferramentas** menu, selecione **configurações de projeto padrão**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **conversão**.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu, selecione **configurações de projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **conversão**.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure e ASE usar códigos de erro diferente.  
  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) SSMA mostra no painel de saída ou a lista de erros quando ele encontra uma referência a **@@ERROR**  no código ASE.  
  
-   Se você selecionar **converter e marcar com aviso**, SSMA converterá as instruções e marcá-los com os comentários de aviso.  
  
-   Se você selecionar **marca com o erro**, SSMA ignorará a conversão e marcar as instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** converter e marcar com aviso  
  
**Modo completo:** marca com erro  
  
**Conversão de operador LIKE**  
Especifica se deve converter como operandos para corresponder Sybase ASE comportamento. O ponto é Sybase corta os espaços em branco em um padrão de like. A solução é fazer uma conversão de expressão da direita para um tipo de dados de comprimento fixo com uma precisão máxima.  
  
-   Selecione **conversão Simple** converter expressões sem qualquer correção.  
  
-   Para usar a seleção de comportamento ASE **convertido em comprimento fixo.**  
  
Quando você seleciona um modo de conversão na caixa de modo, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/Optimistic**: conversão Simple  
  
**Modo de inteira**: convertido em comprimento fixo  
  
**CONVERTER OU CONVERTER CADEIAS DE CARACTERES VAZIAS PARA TIPOS NUMÉRICOS**  
Especifica como lidar com cadeias de caracteres vazias ou em branco dentro de expressões CONVERT ou CAST com tipo numérico como argumento de tipo de dados. As seguintes opções estão disponíveis para essa configuração:  
  
-   Selecione **conversão Simple** converter expressões sem qualquer correção.  
  
-   Se **como zero numérico de cadeia de caracteres vazia** for selecionada, o parâmetro de cadeia de caracteres {s} será substituído pelo ltrim(rtrim({s})) caso quando "", em seguida, 0 else {s} EXPRESSÃO de EXTREMIDADE  
  
Quando você seleciona um modo de conversão na caixa de modo, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/Optimistic**: conversão Simple  
  
**Modo de inteira**: como zero numérico de cadeia de caracteres vazia  
  
**Concatenação de nulos**  
Essa configuração especifica como converter a concatenação de cadeia de caracteres com NULL. As seguintes opções podem ser definidas para essa configuração específica:  
  
-   **Envolver com a função ISNULL:** se essa opção for definida, cada não constante string_expression em concatenação será ajustado com ISNULL(string_expression) e valores nulos serão substituídos pela cadeia de caracteres vazia.  
  
-   **Manter a sintaxe atual**  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** manter a sintaxe atual  
  
**Modo completo:** Wrap com a função ISNULL  
  
**Conversão de cadeias de caracteres vazias**  
Essa configuração especifica como converter cadeias de caracteres vazias. As seguintes opções podem ser definidas para essa configuração específica:  
  
-   **Substitua todas as expressões de cadeia de caracteres com espaço**  
  
-   **Substituir constantes de cadeia de caracteres vazia com espaço**  
  
-   Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ comportamento do SQL Azure, selecione **manter a sintaxe atual**.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** manter a sintaxe atual  
  
**Modo completo:** substituir todas as expressões de cadeia de caracteres com espaço  
  
**Converter e CONVERSÃO de conversão de cadeia de caracteres binária**  
A conversão de valores binários para números pode retornar valores diferentes em diferentes plataformas. Por exemplo, em x86 processadores, CONVERT (inteiro, 0x00000100) retorna 65536 no ASE e 256 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. ASE também retorna valores diferentes dependendo da ordem de byte.  
  
Use esta configuração para controlar como o SSMA converte converter e expressões que contêm valores binários:  
  
-   Selecione **conversão Simple** converter expressões sem avisos ou correção. Use essa configuração se você souber que o servidor ASE tem uma ordem de byte que não requer qualquer alteração do valor binário.  
  
-   Selecione **converter e corrigir** ter SSMA converter e corrigir as expressões para uso em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. A ordem de byte em constantes de literal será revertida. Todos os outros valores binários (como binários variáveis e colunas) serão marcados com erros. Use esse valor se você souber que o servidor de ASE tem uma ordem de byte que requer alterações em valores binários.  
  
-   Selecione **converter e marcar com aviso** ter SSMA converter e corrigir as expressões e marcar todos convertidos expressões com comentários de aviso.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão:** converter e marcar com aviso  
  
**Modo otimista:** conversão Simple  
  
**Modo completo:** converter e corrigir  
  
**SQL dinâmico**  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) SSMA mostra no painel de saída ou a lista de erros quando ele encontra SQL dinâmico no código ASE.  
  
-   Se você selecionar **converter e marcar com aviso**, SSMA converterá o SQL dinâmico e marcar as instruções com comentários de aviso.  
  
-   Se você selecionar **marca com o erro**, SSMA ignorará a conversão e marcar as instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** converter e marcar com aviso  
  
**Modo completo:** marca com erro  
  
**Conversão de verificação de igualdade**  
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure, se a configuração de ANSI_NULLS é on, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure retorna UNKNOWN quando qualquer comparação de igualdade contém um valor nulo. Se ANSI_NULLS for off, comparações de igualdade que contêm valores nulos retornam true quando a coluna comparada e expressão ou duas expressões são nulas. Por igualdade padrão (ANSINULL OFF) Sybase ASE comparações se comportam como [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure com ANSI_NULLS OFF.  
  
-   Se você selecionar **conversão Simple**, SSMA converterá o código ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ sintaxe SQL Azure sem verificações extras para valores nulos. Use esta configuração se ANSI_NULLS for off em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure ou se você quiser revisar comparações de igualdade em uma base por caso.  
  
-   Se você selecionar **valores nulos considere**, SSMA adicionará verifica se há valores nulos, usando as cláusulas IS NULL e IS NOT NULL.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** conversão Simple  
  
**Modo completo:** considere NULL valores  
  
**Cadeias de caracteres de formato**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure não oferece mais suporte a *format_string* argumento em instruções PRINT e RAISERROR. O *format_string* variável suporte colocando parâmetros substituíveis diretamente na cadeia de caracteres e, em seguida, substituir os parâmetros em tempo de execução. Em vez disso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] requer a cadeia de caracteres completa usando uma cadeia de caracteres literal ou uma cadeia de caracteres criada usando uma variável. Para obter mais informações, consulte o "impressão ([!INCLUDE[tsql](../../includes/tsql_md.md)])" tópico [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
Quando o SSMA encontra um *format_string* argumento, ele pode construir uma cadeia de caracteres literal usando as variáveis ou criar uma nova variável e criar uma cadeia de caracteres usando essa variável.  
  
-   Para usar uma literal de cadeia de caracteres para funções PRINT e RAISERROR, selecione **criar nova cadeia de caracteres**.  
  
    Nesse modo, se uma instrução PRINT ou RAISERROR não usa espaços reservados e variáveis locais, a instrução é inalterada. Caracteres duplos porcentagem (%) são alterados para um único caractere de porcentagem de % em literais de cadeia de caracteres de impressão.  
  
    Se uma instrução PRINT ou RAISERROR usa espaços reservados e um ou mais variáveis locais, como o exemplo a seguir:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    O SSMA converterá a seguinte sintaxe:  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    Se *format_string* é uma variável, como a seguinte instrução:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    O SSMA não é possível fazer uma conversão de cadeia de caracteres simples e deve criar uma nova variável:  
  
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
    Quando usa **criar nova cadeia de caracteres** modo, o SSMA supõe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] opção CONCAT_NULL_YIELDS_NULL está OFF. Portanto, não verifica SSMA para argumentos nulos.  
  
-   Para criar uma nova variável para cada instrução PRINT e RAISERROR e, em seguida, usar essa variável para o valor de cadeia de caracteres do SSMA, selecione **criar nova variável**.  
  
    Nesse modo, se uma instrução PRINT ou RAISERROR não usa espaços reservados e variáveis locais, o SSMA substitui todos os caracteres de porcentagem duplos (%) com caracteres de porcentagem simples de acordo com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ sintaxe SQL Azure.  
  
    Se uma instrução PRINT ou RAISERROR usa espaços reservados e um ou mais variáveis locais, como o exemplo a seguir:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    O SSMA converterá a seguinte sintaxe:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    Se *format_string* é uma variável, como a seguinte instrução:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    O SSMA cria uma nova variável assim, verificando os valores nulos em cada argumento:  
  
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
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** criar nova cadeia de caracteres  
  
**Modo completo:** criar nova variável  
  
**Inserir um valor explícito em uma coluna de carimbo de hora**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure não oferece suporte para inserir valores explícitos em uma coluna de carimbo de hora.  
  
-   Para excluir colunas de carimbo de hora de instruções INSERT, selecione **excluir coluna**.  
  
-   Para imprimir uma mensagem de erro toda vez que uma coluna de carimbo de hora é em uma instrução INSERT, selecione **marca com o erro**. Nesse modo, as instruções INSERT não serão convertidas em serão marcadas com comentários de erro.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** excluir coluna  
  
**Modo completo:** marca com erro  
  
**Armazenar objetos temporários definidos nos procedimentos**  
Essa configuração especifica se as definições de objetos temporários que aparecem nos procedimentos devem ser armazenadas em uma fonte de metadados durante a conversão.  
  
-   Selecione **Sim** para armazenar em metadados.  
  
-   Selecione **não** se os objetos não precisam ser armazenados.  
  
**Modo padrão/otimista:** Sim  
  
**Modo completo:** não  
  
**Conversão de tabela de proxy**  
Especifica se as tabelas de proxy ASE são convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ tabelas do SQL Azure, ou são não convertido e o código está marcado com comentários de erro.  
  
-   Selecione **converter** para converter as tabelas de proxy em tabelas regulares.  
  
-   Selecione **marca com o erro** simplesmente marcar o código de proxy de tabela com comentários de erro.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão Optimistic/inteira:** marca com erro  
  
**Número de mensagens base RAISERROR**  
Mensagens de usuário ASE são armazenadas em cada banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mensagens de usuário são armazenadas e disponibilizadas por meio de centralmente o **messages** exibição do catálogo. Além de mensagens de usuário ASE começam em 20000, mas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mensagens de erro começam em 50001.  
  
Essa configuração especifica o número para adicionar ao número de mensagens de usuário de ASE para convertê-lo para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mensagem do usuário. Se seu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tem mensagens de usuário na **messages** modo de exibição de catálogo, talvez você precise alterar esse número para um valor mais alto. Isso é para que os números de mensagem convertido não entrem em conflito com os números de mensagem existente.  
  
Observe o seguinte:  
  
-   Mensagens ASE no intervalo 19999 17000 derivam da tabela de sistema sysmessages e não são convertidas.  
  
-   Se o número da mensagem que é referenciado na instrução RAISERROR é uma constante, o SSMA adicionará o número de mensagens base à constante para determinar o número de mensagem do novo usuário.  
  
-   Se o número da mensagem que é referenciado é uma variável ou expressão, o SSMA criará uma variável local intermediário.  
  
-   No modo otimista, SSMA supõe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] opção CONCAT_NULL_YIELDS_NULL está desativado e não faz nenhuma verificação para argumentos nulos.  
  
-   No modo completo, o SSMA procura argumentos nulos.  
  
-   RAISERROR com ERRORDATA *lista* não é convertido.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão otimista/inteira:** 30001  
  
**Objetos do sistema**  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) SSMA mostra no painel de saída ou a lista de erros quando encontra o uso de objetos de sistema ASE.  
  
-   Se você selecionar **converter e marcar com aviso**, SSMA converterá as referências a objetos de sistema e marcará instruções com comentários de aviso.  
  
-   Se você selecionar **marca com o erro**, SSMA não converterá as referências a objetos de sistemas e marcará instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** converter e marcar com aviso  
  
**Modo completo:** marca com erro  
  
**Identificadores não resolvidos**  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) SSMA mostra no painel de saída ou a lista de erros quando ele não é possível resolver um identificador.  
  
-   Se você selecionar **converter e marcar com aviso**, SSMA tentará converter as referências a identificadores não resolvidos e marcará instruções com comentários de aviso.  
  
-   Se você selecionar **marca com o erro**, SSMA não converterá referências a identificadores não resolvidos e marcará instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** converter e marcar com aviso  
  
**Modo completo:** marca com erro  
  
## <a name="system-function-options"></a>Opções de função do sistema  
**Função CHARINDEX**  
Em ASE, CHARINDEX retornará NULL somente se todas as expressões de entrada forem NULL. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure retornará NULL se qualquer expressão de entrada é NULL.  
  
-   Para usar o comportamento de ASE, selecione **função Replace**. Todas as chamadas para a função CHARINDEX é substituída por uma chamada à função definida pelo usuário CHARINDEX_VARCHAR ou CHARINDEX_NVARCHAR, com base no tipo de parâmetros passados (criado no banco de dados de usuário sob o nome do esquema 's2ss') para emular o comportamento do Sybase ASE.  
  
-   Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ comportamento do SQL Azure, selecione **manter a sintaxe atual**.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** manter a sintaxe atual  
  
**Modo completo:** função Replace  
  
**Função DATALENGTH**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] / SQL Azure e ASE diferem no valor retornado pela função DATALENGTH quando o valor é um único espaço. Nesse caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure retorna 0 e ASE retorna 1.  
  
-   Para usar o comportamento de ASE, selecione **função Replace**. Todas as chamadas para a função DATALENGTH são substituídas por expressão CASE para emular o comportamento do Sybase ASE.  
  
-   Para usar o padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] / comportamento do SQL Azure, selecione **manter a sintaxe atual**.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** manter a sintaxe atual  
  
**Modo completo:** função Replace  
  
**Função INDEX_COL**  
ASE dá suporte a um recurso opcional *user_id* argumento da função INDEX_COL; no entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure não oferece suporte para esse argumento. Se você usar o *user_id* argumento, essa função não pode ser convertida em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ sintaxe SQL Azure.  
  
-   Para usar o comportamento de ASE, selecione **função Convert**. Se o código contém a *user_id* argumento, o SSMA exibirá um erro.  
  
-   Para exibir uma mensagem de erro toda vez que INDEX_COL for encontrado, selecione **marca com o erro**. O SSMA não converterá referências à função e marcará a instrução com comentários de erro.  
  
**Modo padrão Optimistic/inteira:** marca com erro  
  
**Função INDEX_COLORDER**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure não tem uma função de sistema INDEX_COLORDER.  
  
-   Para usar o comportamento de ASE, selecione **função Convert**. Todas as chamadas para a função INDEX_COLORDER é substituída por uma chamada para uma função definida pelo usuário com o mesmo nome INDEX_COLORDER (criado no banco de dados de usuário sob o nome do esquema 's2ss') que emula o comportamento do Sybase ASE.  
  
-   Para imprimir uma mensagem de erro toda vez que INDEX_COLORDER for encontrado, selecione **marca com o erro**. O SSMA não converterá referências à função e marcará a instrução com comentários de erro.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão Optimistic/inteira:** marca com erro  
  
**As funções LEFT e RIGHT**  
Esquerda e direita funções Sybase se comportam de maneira diferente para parâmetro de comprimento negativo.  
  
-   Para usar o comportamento de ASE, selecione **função Replace**. O parâmetro de comprimento, em seguida, é substituído por expressão de caso que retornaria null para um valor negativo.  
  
-   Para usar o comportamento do SQL Server, selecione **manter a sintaxe atual**  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** manter a sintaxe atual  
  
**Modo completo:** função Replace  
  
> [!NOTE]  
> Se o parâmetro de comprimento é um valor literal e não é uma expressão complexa, o valor de comprimento é substituído sempre com null independentemente da configuração de projeto.  
  
**Função NEXT_IDENTITY**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure não tem uma função de sistema NEXT_IDENTITY.  
  
-   Para usar o comportamento de ASE, selecione **função Convert**. Todas as chamadas para a função NEXT_IDENTITY é substituído por expressão (IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value) que emula o comportamento do Sybase ASE.  
  
-   Para imprimir uma mensagem de erro toda vez que NEXT_IDENTITY for encontrado, selecione **marca com o erro**. O SSMA não converterá referências à função e marcará a instrução com comentários de erro.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão Optimistic/inteira:** marca com erro  
  
**Função PATINDEX**  
Especifica se a função PATINDEX para coincidir com o comportamento do Sybase ASE convert. O ponto é Sybase corta os espaços em branco em um padrão de pesquisa. A solução é fazer uma conversão de expressão de valor para um tamanho fixo do tipo com uma precisão máxima de dados e aplicam a função rtrim para pesquisar padrão.  
  
-   Para usar a seleção de comportamento ASE **usar**.  
  
-   Para usar o padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ comportamento do SQL Azure, selecione **não use**.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** não usar  
  
**Modo completo:** Use  
  
**Função REPLICATE**  
A função REPLICATE repete uma cadeia de caracteres do número de vezes especificado. Em ASE, se você especificar para repetir a cadeia de caracteres zero vezes, o resultado será nulo. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure, o resultado é uma cadeia de caracteres vazia.  
  
-   Para usar o comportamento de ASE, selecione **função Replace**. Todas as chamadas para a função REPLICATE é substituída por uma chamada à função definida pelo usuário REPLICATE_VARCHAR ou REPLICATE_NVARCHAR, com base no tipo de parâmetros passados (criado no banco de dados de usuário sob o nome do esquema 's2ss') para emular o comportamento do Sybase ASE.  
  
-   Para usar o padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ comportamento do SQL Azure, selecione **função Replace**.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo de inteira modo otimista/padrão:** função Replace  
  
**Função TRIM (LTRIM, RTRIM)**  
Essa configuração especifica se deve substituir chamadas para funções Trim (LTRIM, RTRIM) com as funções de sintaxe equivalente Sybase ASE ou para manter a sintaxe atual. As opções a seguir estão presentes para essa configuração específica:  
  
-   **Função Replace**  
  
-   **Manter a sintaxe atual**  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo de inteira modo otimista/padrão:** função Replace  
  
**Função SUBSTRING**  
Em ASE, a função `SUBSTRING(expression, start, length)` retorna NULL se for especificado um valor de início maior que o número de caracteres na expressão, ou se o comprimento é igual a zero. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure, a expressão equivalente retorna uma cadeia de caracteres vazia.  
  
-   Para usar o comportamento de ASE, selecione **função Replace**. Todas as chamadas para a função SUBSTRING é substituída por uma chamada à função definida pelo usuário SUBSTRING_VARCHAR ou SUBSTRING_NVARCHAR ou SUBSTRING_VARBINARY, com base no tipo de parâmetros passados (criado no banco de dados de usuário sob o nome do esquema 's2ss') para emular o comportamento do Sybase ASE.  
  
-   Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] / comportamento do SQL Azure, selecione **manter a sintaxe atual**.  
  
Quando você seleciona um modo de conversão no **modo** caixa, SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** manter a sintaxe atual  
  
**Modo completo:** função Replace  
  
## <a name="tables"></a>TABLES  
**Adicionar a chave primária**  
Cria uma nova chave primária no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabela do SQL Azure se uma tabela não tem chave primária ou índice exclusivo.  
  
-   **Modo padrão**: falso  
  
-   **Modo otimista**: falso  
  
-   **Modo de inteira**: True  
  
> [!NOTE]  
> Quando conectado ao SQL Azure, é por padrão True.  
  
## <a name="see-also"></a>Consulte também  
[Referência da Interface de usuário &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
