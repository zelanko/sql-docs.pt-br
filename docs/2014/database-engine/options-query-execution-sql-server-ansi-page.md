---
title: Opções (página servidor ANSI SQL de execução da consulta) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAnsi
ms.assetid: 0f4c6887-0562-417e-806c-b5cffb1e7c5c
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e075de106a66ffee63c02ead06a3fc68548111a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089377"
---
# <a name="options-query-execution-sql-server-ansi-page"></a>Opções (página servidor ANSI SQL de execução da consulta)
  Juntas, essas opções SET padrão ANSI (ISO) definem o ambiente de processamento de consulta enquanto durar a consulta do usuário, a execução de um gatilho, ou um procedimento armazenado. Porém, essas opções SET não incluem todas as opções exigidas pelo padrão ISO. Use essa página para especificar que o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] irá executar as consultas usando todas ou uma parte das configurações especificadas no padrão ISO. As alterações feitas nessas opções são aplicadas apenas a novas consultas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para alterar as opções para as consultas atuais, clique em **Opções de Consulta** no menu **Consulta** ou clique com o botão direito do mouse na janela Consulta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e selecione **Opções de Consulta**. Na caixa de diálogo **Opções de Consulta** , em **Execução**, clique em **ANSI**.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **SET ANSI_DEFAULTS**  
 Marque essa caixa de seleção para selecionar todas as configurações ISO padrão. Nem todas as opções ISO são selecionadas por padrão.  
  
 **SET QUOTED_IDENTIFIER**  
 Quando essa caixa de seleção é marcada, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] segue as regras ISO relativas ao uso de aspas para delimitar identificadores e cadeias de caracteres literais. Identificadores delimitados por aspas podem ser palavras-chave reservadas da Transact-SQL ou podem conter caracteres que nem sempre são permitidos pelas regras da sintaxe Transact-SQL para identificadores. Esta caixa de seleção fica marcada por padrão.  
  
 **SET ANSI_NULL_DFLT_ON**  
 Quando esse valor é definido, todos os tipos de dados ou colunas definidos pelo usuário não são explicitamente definidos como NOT NULL durante uma instrução padrão CREATE TABLE ou ALTER TABLE, para permitir valores nulos. Esta caixa de seleção fica marcada por padrão.  
  
 **SET IMPLICIT_TRANSACTIONS**  
 Quando essa caixa de seleção é marcada, SET IMPLICIT_TRANSACTIONS define a conexão em modo de transação implícito. Quando essa caixa de seleção é desmarcada, a conexão volta ao modo de transação de confirmação automática. Para examinar as instruções que iniciam uma transação implícita quando selecionadas, consulte [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-implicit-transactions-transact-sql). Essa caixa de seleção é desmarcada por padrão.  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 Quando essa caixa de seleção é selecionada, qualquer cursor aberto é fechado automaticamente (conforme o padrão ISO), quando uma transação for confirmada. Quando esse valor for definido como OFF, os cursores permanecem abertos nos limites da transação, fechando apenas quando a conexão for fechada ou quando eles forem explicitamente fechados. Essa caixa de seleção é desmarcada por padrão.  
  
 **SET ANSI_PADDING**  
 Controla como a coluna armazena nomes de valores menores do que o tamanho definido da coluna, e a maneira como a coluna armazena valores com espaços em branco em dados **char**, **varchar**, **binários**e **varbinary** . Essa configuração afeta somente a definição de novas colunas. Depois que a coluna é criada, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] armazena os valores com base na configuração de quando a coluna foi criada. As colunas existentes não são afetadas por uma alteração posterior a essa configuração. Esta caixa de seleção fica marcada por padrão.  
  
 **SET ANSI_WARNINGS**  
 Especifica o comportamento ISO padrão em várias condições de erro:  
  
-   Quando essa caixa de seleção é marcada, se forem exibidos valores nulos em funções de agregação (como SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP ou COUNT), será gerada uma mensagem de aviso. Quando em OFF, nenhum aviso é emitido.  
  
-   Quando essa caixa de seleção é desmarcada, erros de estouro aritmético e de divisão por zero fazem com que a instrução a retorne e uma mensagem de erro seja gerada. Quando OFF, erros de estouro aritmético e de divisão por zero fazem com que valores nulos sejam retornados. O comportamento que leva um erro de estouro aritmético e de divisão por zero a fazer como que valores nulos sejam retornados ocorre, se houver uma tentativa de operação INSERT ou UPDATE em um **caractere**, **Unicode** ou coluna **binária**, na qual o comprimento do novo valor excede o tamanho máximo da coluna. Quando SET ANSI_WARNINGS estiver como ON, a operação INSERT ou UPDATE é cancelada, como especificado pelo padrão ISO. Espaços em branco à direita são ignorados em colunas de caracteres e valores nulos à direita são ignorados em colunas binárias. Quando OFF, os dados são truncados para o tamanho da coluna e a instrução obtém êxito.  
  
 Esta caixa de seleção fica marcada por padrão.  
  
 **SET ANSI_NULLS**  
 -   Especifica o comportamento compatível ISO dos operadores de comparação Igual a (=) e É diferente de (<>) quando usados com valores nulos. Quando SET ANSI_NULLS é selecionada, todas as comparações com um valor nulo são avaliadas como UNKNOWN, comportamento compatível com o padrão ISO. Quando SET ANSI_NULLS não é selecionada, comparações de todos os dados em relação a um valor nulo são avaliadas como TRUE. Esta caixa de seleção fica marcada por padrão.  
  
 **Restaurar Padrões**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
  
