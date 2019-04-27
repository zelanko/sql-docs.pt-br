---
title: Project Settings (Conversion) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 4d7f290459e1da736605acad941602399ec3ea53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62664658"
---
# <a name="project-settings-conversion-sybasetosql"></a>Configurações do projeto (conversão) (SybaseToSQL)
A página de conversão do **configurações do projeto** caixa de diálogo contém configurações que personalizam como SSMA converte a sintaxe do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a sintaxe do SQL Azure.  
  
O painel de conversão está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo:  
  
-   Se você deseja especificar configurações para todos os projetos do SSMA, na **ferramentas** menu, selecione **configurações do projeto padrão**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **Conversão**.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **Conversão**.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure e o ASE usam códigos de erro diferentes.  
  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que SSMA mostra no painel de saída ou a lista de erros quando encontra uma referência a **@@ERROR**  no código do ASE.  
  
-   Se você selecionar **converter e marcar com aviso**, SSMA converterá as instruções e marcá-los com comentários de aviso.  
  
-   Se você selecionar **marca com o erro**, SSMA ignorará a conversão e marcar as instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Converter e marcar com aviso  
  
**Modo completo:** Marcar com erro  
  
**Conversão de operador LIKE**  
Especifica se deve converter como operandos para corresponder ao comportamento de ASE do Sybase. O ponto é Sybase corta os espaços em branco em um padrão de semelhança. A solução alternativa é fazer uma conversão de expressão da direita para um tipo de dados de comprimento fixo com uma precisão máxima.  
  
-   Selecione **conversão simples** para converter as expressões sem qualquer correção.  
  
-   Para usar o ASE comportamento select **convertido para o comprimento fixo.**  
  
Quando você seleciona um modo de conversão na caixa de modo, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista**: Conversão simples  
  
**Modo de inteira**: Converter em comprimento fixo  
  
**CONVERTER OU CONVERTER CADEIAS DE CARACTERES VAZIAS PARA TIPOS NUMÉRICOS**  
Especifica como lidar com cadeias de caracteres vazias ou em branco dentro de expressões de CONVERT ou CAST com um tipo numérico como argumento de tipo de dados. As seguintes opções estão disponíveis para essa configuração:  
  
-   Selecione **conversão simples** para converter as expressões sem qualquer correção.  
  
-   Se **cadeia de caracteres vazia como zero numérico** estiver selecionada, o parâmetro de cadeia de caracteres {s} será substituído pelo ltrim(rtrim({s})) maiusculas quando "", em seguida, 0 else {s} EXPRESSÃO final  
  
Quando você seleciona um modo de conversão na caixa de modo, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista**: Conversão simples  
  
**Modo de inteira**: A cadeia de caracteres vazia como zero numérico  
  
**Concatenação de NULL**  
Essa configuração especifica como converter a concatenação de cadeia de caracteres com NULL. As opções a seguir podem ser definidas para essa configuração específica:  
  
-   **Encapsular com a função ISNULL:** Se essa opção for definida, cada não constante string_expression em concatenação será encapsulado com ISNULL(string_expression) e valores nulos serão substituídos pela cadeia de caracteres vazia.  
  
-   **Manter a sintaxe atual**  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Encapsular com a função ISNULL  
  
**Conversão de cadeias de caracteres vazias**  
Essa configuração especifica como converter cadeias de caracteres vazias. As opções a seguir podem ser definidas para essa configuração específica:  
  
-   **Substitua todas as expressões de cadeia de caracteres de espaço**  
  
-   **Substitua as constantes de cadeia de caracteres vazia com espaço**  
  
-   Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ comportamento do SQL Azure, selecione **manter sintaxe atual**.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Substitua todas as expressões de cadeia de caracteres de espaço  
  
**Converter e CONVERSÃO de conversão de cadeia de caracteres binária**  
A conversão de valores binários para números pode retornar valores diferentes em diferentes plataformas. Por exemplo, em x86 processadores, CONVERT (integer, 0x00000100) retorna 65536 em ASE e 256 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. ASE também retorna valores diferentes dependendo da ordem de byte.  
  
Use essa configuração para controlar como converter converte SSMA e expressões CASE que contêm valores binários:  
  
-   Selecione **conversão simples** para converter as expressões sem avisos ou correção. Use essa configuração se você souber que o servidor de ASE tem uma ordem de byte que não requer qualquer alteração do valor binário.  
  
-   Selecione **converter e corrija** ter o SSMA converter e corrigir as expressões para uso em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A ordem de byte em constantes de literais será revertida. Todos os outros valores binários (como binárias variáveis e colunas) serão marcados com erros. Use esse valor se você souber que o servidor de ASE tem uma ordem de byte que requer alterações em valores binários.  
  
-   Selecione **converter e marcar com aviso** ter SSMA converta e corrigir as expressões e marcar todos convertidos em expressões com comentários de aviso.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão:** Converter e marcar com aviso  
  
**Modo otimista:** Conversão simples  
  
**Modo completo:** Converter e corrigir  
  
**SQL dinâmico**  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que SSMA mostra no painel de saída ou a lista de erros quando encontra SQL dinâmico no código do ASE.  
  
-   Se você selecionar **converter e marcar com aviso**, SSMA converterá SQL dinâmico e marcar as instruções com comentários de aviso.  
  
-   Se você selecionar **marca com o erro**, SSMA ignorará a conversão e marcar as instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Converter e marcar com aviso  
  
**Modo completo:** Marcar com erro  
  
**Conversão de verificação de igualdade**  
Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure, se a configuração de ANSI_NULLS for on, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure retorna UNKNOWN quando qualquer comparação de igualdade contém um valor nulo. Se ANSI_NULLS for off, comparações de igualdade que contêm valores nulos retornam true quando a coluna comparada e expressão ou duas expressões são nulas. Por igualdade padrão (ANSINULL desativado) Sybase ASE comparações se comportam como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure com ANSI_NULLS OFF.  
  
-   Se você selecionar **conversão simples**, o SSMA converterá o código do ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ sintaxe de SQL Azure sem verificações adicionais para valores nulos. Use esta configuração se ANSI_NULLS for off em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure ou se você quiser revisar comparações de igualdade em uma base por caso.  
  
-   Se você selecionar **valores nulos considere**, SSMA adicionará as verificações de valores nulos, usando as cláusulas IS NULL e IS NOT NULL.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Conversão simples  
  
**Modo completo:** Considere a possibilidade de valores NULL  
  
**Cadeias de caracteres de formato**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure não é compatível com o *format_string* argumento em instruções PRINT e RAISERROR. O *format_string* colocando parâmetros substituíveis diretamente na cadeia de caracteres e, em seguida, substituindo os parâmetros em tempo de execução com suporte de variável. Em vez disso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que a cadeia de caracteres completa, usando um literal de cadeia de caracteres ou uma cadeia de caracteres criada usando uma variável. Para obter mais informações, consulte a "impressão ( [!INCLUDE[tsql](../../includes/tsql-md.md)])" tópico no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
Quando o SSMA encontra uma *format_string* argumento, ele pode criar uma cadeia de caracteres literal usando as variáveis ou criar uma nova variável e criar uma cadeia de caracteres, usando essa variável.  
  
-   Para usar uma cadeia de caracteres literal para funções PRINT e RAISERROR, selecione **criar nova cadeia de caracteres**.  
  
    Nesse modo, se uma instrução PRINT ou RAISERROR não usa espaços reservados e variáveis locais, a instrução permanecerá inalterada. Double caracteres de porcentagem (%) são alteradas para um único caractere de porcentagem de % em literais de cadeia de caracteres de impressão.  
  
    Se uma instrução PRINT ou RAISERROR usa espaços reservados e um ou mais variáveis locais, como no exemplo a seguir:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    O SSMA irá convertê-lo para a seguinte sintaxe:  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    Se *format_string* é uma variável, como na instrução a seguir:  
  
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
    Quando ele usa **criar nova cadeia de caracteres** modo, o SSMA supõe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opção CONCAT_NULL_YIELDS_NULL está OFF. Portanto, não verifica SSMA para argumentos nulos.  
  
-   Para criar uma nova variável para cada instrução PRINT e RAISERROR e, em seguida, use essa variável para o valor de cadeia de caracteres que o SSMA, selecione **criar nova variável**.  
  
    Nesse modo, se uma instrução PRINT ou RAISERROR não usa espaços reservados e variáveis locais, o SSMA substitui todos os caracteres de porcentagem duplos (%) com caracteres únicos de porcentagem em conformidade com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ sintaxe de SQL Azure.  
  
    Se uma instrução PRINT ou RAISERROR usa espaços reservados e um ou mais variáveis locais, como no exemplo a seguir:  
  
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
    Se *format_string* é uma variável, como na instrução a seguir:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    O SSMA cria uma nova variável da seguinte maneira, verificando os valores nulos em cada argumento:  
  
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
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Criar nova cadeia de caracteres  
  
**Modo completo:** Criar nova variável  
  
**Inserir um valor explícito em uma coluna de carimbo de hora**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure não oferece suporte para inserir valores explícitos em uma coluna de carimbo de hora.  
  
-   Para excluir colunas de carimbo de hora de instruções INSERT, selecione **excluir coluna**.  
  
-   Para imprimir uma mensagem de erro sempre que uma coluna de carimbo de hora é em uma instrução INSERT, selecione **marca com o erro**. Nesse modo, as instruções INSERT não serão convertidas em serão marcadas com comentários de erro.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Excluir coluna  
  
**Modo completo:** Marcar com erro  
  
**Objetos temporários definidos nos procedimentos de Store**  
Essa configuração especifica se as definições de objetos temporários que aparecem nos procedimentos devem ser armazenadas nos metadados do código-fonte durante a conversão.  
  
-   Selecione **Sim** para armazenar em metadados.  
  
-   Selecione **não** se os objetos não precisam ser armazenados.  
  
**Modo padrão/otimista:** Sim  
  
**Modo completo:** Não  
  
**Conversão da tabela de proxy**  
Especifica se as tabelas de proxy do ASE serão convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ tabelas do SQL Azure ou são não convertido e o código está marcado com comentários de erro.  
  
-   Selecione **converter** para converter as tabelas de proxy em tabelas regulares.  
  
-   Selecione **marca com o erro** simplesmente marcar o código de proxy de tabela com comentários de erro.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Marcar com erro  
  
**Número de mensagens base RAISERROR**  
Mensagens de usuário do ASE são armazenadas em cada banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagens de usuário são armazenadas e disponibilizadas por meio de centralmente as **sys. messages** exibição do catálogo. Além da mensagens de usuário do ASE começam em 20000, mas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagens de erro começam em 50001.  
  
Essa configuração especifica o número a ser adicionado para o número de mensagem de usuário do ASE para convertê-lo para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem do usuário. Se sua [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem mensagens de usuário na **sys. messages** exibição do catálogo, talvez você precise alterar esse número para um valor mais alto. Isso é para que os números de mensagem convertida não entrem em conflito com números de mensagem existente.  
  
Observe o seguinte:  
  
-   Mensagens de ASE no intervalo 17000 19999 são da tabela do sistema sysmessages e não são convertidas.  
  
-   Se o número da mensagem que é referenciado na instrução RAISERROR é uma constante, o SSMA adicionará o número de mensagens base para a constante para determinar o novo número de mensagem do usuário.  
  
-   Se o número da mensagem que é referenciado é uma variável ou expressão, o SSMA criará uma variável local intermediário.  
  
-   No modo otimista, SSMA presume que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opção CONCAT_NULL_YIELDS_NULL está desativado e não faz nenhuma verificação para argumentos nulos.  
  
-   No modo completo, o SSMA procura por argumentos nulos.  
  
-   RAISERROR com ERRORDATA *lista* não é convertido.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** 30001  
  
**Objetos do sistema**  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que SSMA mostra no painel de saída ou a lista de erros quando encontra o uso de objetos de sistema ASE.  
  
-   Se você selecionar **converter e marcar com aviso**, SSMA converterá as referências a objetos de sistema e o marcará as instruções com comentários de aviso.  
  
-   Se você selecionar **marca com o erro**, SSMA não converterá as referências a objetos de sistemas e irá marcar as instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Converter e marcar com aviso  
  
**Modo completo:** Marcar com erro  
  
**Identificadores não resolvidos**  
Use essa configuração para especificar o tipo de mensagem (aviso ou erro) que mostra o SSMA no painel de saída ou a lista de erros quando ele não é possível resolver um identificador.  
  
-   Se você selecionar **converter e marcar com aviso**, SSMA tentará converter as referências para identificadores não resolvidos e o marcará as instruções com comentários de aviso.  
  
-   Se você selecionar **marca com o erro**, SSMA não converterá as referências para identificadores não resolvidos e o marcará as instruções com comentários de erro.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Converter e marcar com aviso  
  
**Modo completo:** Marcar com erro  
  
## <a name="system-function-options"></a>Opções de função do sistema  
**Função CHARINDEX**  
Em ASE, CHARINDEX retornará NULL somente se todas as expressões de entrada forem NULL. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ O SQL Azure retornará NULL se qualquer expressão de entrada é NULL.  
  
-   Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a função CHARINDEX é substituída por uma chamada à função definida pelo usuário CHARINDEX_VARCHAR ou CHARINDEX_NVARCHAR, com base no tipo de parâmetros passados (criado no banco de dados de usuário sob o nome do esquema 's2ss') para emular o comportamento do Sybase ASE.  
  
-   Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ comportamento do SQL Azure, selecione **manter sintaxe atual**.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Função Replace  
  
**Função DATALENGTH**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] / SQL Azure e o ASE diferem no valor retornado pela função DATALENGTH quando o valor é um único espaço. Nesse caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure retorna 0 e o ASE retorna 1.  
  
-   Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a função DATALENGTH são substituídas por expressão CASE para emular o comportamento do Sybase ASE.  
  
-   Para usar o padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] / comportamento do SQL Azure, selecione **manter sintaxe atual**.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Função Replace  
  
**Função INDEX_COL**  
ASE dá suporte a um recurso opcional *user_id* argumento para a função INDEX_COL; no entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure não oferece suporte a esse argumento. Se você usar o *user_id* argumento, essa função não pode ser convertida em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ sintaxe de SQL Azure.  
  
-   Para usar o comportamento do ASE, selecione **converter função**. Se o código contém a *user_id* argumento, o SSMA exibirá um erro.  
  
-   Para exibir uma mensagem de erro toda vez que INDEX_COL for encontrado, selecione **marca com o erro**. SSMA não converterá referências à função e o marcará a instrução com comentários de erro.  
  
**Modo padrão/otimista/completo:** Marcar com erro  
  
**Função INDEX_COLORDER**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure não tem uma função de sistema INDEX_COLORDER.  
  
-   Para usar o comportamento do ASE, selecione **converter função**. Todas as chamadas para a função INDEX_COLORDER é substituída por uma chamada para uma função definida pelo usuário com o mesmo nome INDEX_COLORDER (criada no banco de dados de usuário sob o nome do esquema 's2ss'), que emula o comportamento do Sybase ASE.  
  
-   Para imprimir uma mensagem de erro toda vez que INDEX_COLORDER for encontrado, selecione **marca com o erro**. SSMA não converterá referências à função e o marcará a instrução com comentários de erro.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Marcar com erro  
  
**Funções LEFT e RIGHT**  
Esquerda e direita de funções no Sybase se comportam de forma diferente para parâmetro de comprimento negativo.  
  
-   Para usar o comportamento do ASE, selecione **função Replace**. O parâmetro de comprimento, em seguida, é substituído por expressão de caso que retornaria nulo para o valor negativo.  
  
-   Para usar o comportamento do SQL Server, selecione **manter sintaxe atual**  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Função Replace  
  
> [!NOTE]  
> Se o parâmetro de comprimento é um valor literal e não uma expressão complexa, o valor de comprimento sempre é substituído com null, independentemente da configuração do projeto.  
  
**Função NEXT_IDENTITY**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure não tem uma função de sistema NEXT_IDENTITY.  
  
-   Para usar o comportamento do ASE, selecione **converter função**. Todas as chamadas para a função NEXT_IDENTITY é substituída por expressão (IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value) que emula o comportamento do Sybase ASE.  
  
-   Para imprimir uma mensagem de erro toda vez que NEXT_IDENTITY for encontrado, selecione **marca com o erro**. SSMA não converterá referências à função e o marcará a instrução com comentários de erro.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista/completo:** Marcar com erro  
  
**Função PATINDEX**  
Especifica se deve converter a função PATINDEX para corresponder ao comportamento de ASE do Sybase. O ponto é Sybase corta os espaços em branco em um padrão de pesquisa. A solução alternativa é fazer uma conversão de expressão de valor com um comprimento fixo de tipo com uma precisão máxima de dados e aplicam a função rtrim para pesquisar o padrão.  
  
-   Para usar a seleção de comportamento do ASE **usar**.  
  
-   Para usar o padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ comportamento do SQL Azure, selecione **não use**.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Não usar  
  
**Modo completo:** Use  
  
**Função REPLICATE**  
A função REPLICATE repete uma cadeia de caracteres do número de vezes especificado. Em ASE, se você especificar para repetir a cadeia de caracteres zero vezes, o resultado é nulo. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure, o resultado é uma cadeia de caracteres vazia.  
  
-   Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a função REPLICATE é substituída por uma chamada à função definida pelo usuário REPLICATE_VARCHAR ou REPLICATE_NVARCHAR, com base no tipo de parâmetros passados (criado no banco de dados de usuário sob o nome do esquema 's2ss') para emular o comportamento do Sybase ASE.  
  
-   Para usar o padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ comportamento do SQL Azure, selecione **função Replace**.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo de modo/completo/otimista de padrão:** Função Replace  
  
**Função TRIM (LTRIM, RTRIM)**  
Essa configuração especifica se é para substituir chamadas para funções Trim (LTRIM, RTRIM) com as funções de sintaxe equivalente Sybase ASE ou para manter a sintaxe atual. As opções a seguir estão presentes para essa configuração específica:  
  
-   **Função Replace**  
  
-   **Manter a sintaxe atual**  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo de modo/completo/otimista de padrão:** Função Replace  
  
**Função SUBSTRING**  
Em ASE, a função `SUBSTRING(expression, start, length)` retorna NULL se for especificado um valor de início maior que o número de caracteres na expressão, ou se o comprimento é igual a zero. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure, a expressão equivalente retorna uma cadeia de caracteres vazia.  
  
-   Para usar o comportamento do ASE, selecione **substituir função**. Todas as chamadas para a função de subcadeia de caracteres é substituída por uma chamada à função definida pelo usuário SUBSTRING_VARCHAR ou SUBSTRING_NVARCHAR ou SUBSTRING_VARBINARY, com base no tipo de parâmetros passados (criada no banco de dados de usuário sob o nome do esquema 's2ss') para emular o Comportamento do Sybase ASE.  
  
-   Para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] / comportamento do SQL Azure, selecione **manter sintaxe atual**.  
  
Quando você seleciona um modo de conversão na **modo** caixa, o SSMA aplica-se a configuração a seguir:  
  
**Modo padrão/otimista:** Manter a sintaxe atual  
  
**Modo completo:** Função Replace  
  
## <a name="tables"></a>TABLES  
**Adicione a chave primária**  
Cria uma nova chave primária no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tabela do SQL Azure se uma tabela do Access não tem nenhuma chave primária ou índice exclusivo.  
  
-   **Modo padrão**: Falso  
  
-   **Modo otimista**: Falso  
  
-   **Modo de inteira**: True  
  
> [!NOTE]  
> Quando conectado ao SQL Azure, é por padrão True.  
  
## <a name="see-also"></a>Consulte também  
[Referência da Interface do usuário &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
