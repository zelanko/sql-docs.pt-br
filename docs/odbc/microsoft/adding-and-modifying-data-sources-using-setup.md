---
title: Adicionando e modificando fontes de dados usando a configuração | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae76abc902e4687e5d9891871d7d5d60598b3abc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281406"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Adicionar e modificar fontes de dados usando a instalação
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Uma fonte de dados identifica um caminho para dados que podem incluir uma biblioteca de rede, servidor, banco de dados e outros atributos - neste caso, a fonte de dados é o caminho para um banco de dados Oracle. Para se conectar a uma fonte de dados, o Driver Manager verifica o registro do Windows para obter informações específicas de conexão.  
  
 A entrada de registro criada pelo Administrador de Origem de Dados oDBC é usada pelo Gerenciador de Driver oDBC e drivers ODBC. Esta entrada contém informações sobre cada fonte de dados e seu driver associado. Antes de se conectar a uma fonte de dados, suas informações de conexão devem ser adicionadas ao registro.  
  
 Para adicionar e configurar fontes de dados, use o [Administrador de Fonte de Dados oDBC](../../odbc/admin/odbc-data-source-administrator.md). O administrador do ODBC atualiza as informações de conexão de origem de dados. À medida que você adiciona fontes de dados, o administrador do ODBC atualiza as informações do registro para você.  
  
### <a name="to-add-a-data-source-for-windows"></a>Para adicionar uma fonte de dados para o Windows  
  
1.  Abra o administrador de origem de dados do ODBC.  
  
2.  Na caixa de diálogo Administrador de origem de dados ODBC, clique em Adicionar. A caixa de diálogo Creat New Data Source é exibida.  
  
3.  Selecione ODBC da Microsoft para Oracle e clique em Concluir. A caixa de diálogo Configuração do Microsoft ODBC para Oracle é exibida.  
  
4.  Na caixa Nome de origem de dados, digite o nome da fonte de dados que deseja acessar. Pode ser qualquer nome que você escolher.  
  
5.  Na caixa Descrição, digite a descrição do motorista. Este campo opcional descreve o driver de banco de dados ao que a fonte de dados se conecta. Pode ser qualquer nome que você escolher.  
  
6.  Na caixa Nome de Usuário, digite o nome do usuário do banco de dados (iD do usuário do banco de dados).  
  
7.  Na caixa Servidor, digite o Alias do banco de dados ou conecte a seqüência para o mecanismo Oracle Server que você deseja acessar.  
  
8.  Clique em OK para adicionar essa fonte de dados.  
  
> [!NOTE]  
>  A caixa de diálogo Fontes de dados é exibida e o administrador do ODBC atualiza as informações do registro. O nome de usuário e a seqüência de conexão que você digitou tornam-se os valores de conexão padrão para esta fonte de dados quando você se conectar a ele.  
  
1.  Clique em Opções para fazer mais especificações sobre a configuração do ODBC Driver for Oracle:  
  
    -   **Tradução** - Clique em Selecionar para escolher um tradutor de dados carregado. O padrão \<é Não tradutor>.  
  
    -   **Desempenho** - A caixa de seleção Incluir observações em funções de catálogo especifica se o driver retorna colunas de observações para o conjunto de resultados [sqlColumns.](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) O Driver ODBC para Oracle fornece acesso mais rápido quando esse valor não é definido.  
  
         A caixa de seleção Incluir SINÔNIMOS em Colunas SQL especifica se o driver retorna as informações da coluna. **O Tamanho do buffer** especifica o tamanho, em bytes, alocado para receber dados obtidos. O driver otimiza a busca para que uma busca do Servidor Oracle retorne linhas suficientes para preencher um buffer do tamanho especificado. Valores maiores tendem a aumentar o desempenho ao buscar muitos dados.  
  
    -   **Personalização** - A caixa de seleção Padrão Enforce ODBC DayOfWeek especifica se o conjunto de resultados estará em conformidade com o formato de dia da semana especificado pela ODBC (domingo = 1; Sábado = 7). Se esta caixa de seleção for limpa, o valor Oracle específico do local será devolvido.  
  
         O SQLDescribeCol **sempre retorna um valor para** caixa de seleção de precisão especifica se o driver deve ou não retornar um valor não-zero para o argumento *cbColDef* do **SQLDescribeCol**. Esse atributo de seqüência de conexão se aplica apenas a colunas onde não há escala definida pelo Oracle, como colunas numéricas computadas e colunas definidas como NÚMERO sem precisão ou escala. Uma chamada **SQLDescribeCol** retorna 130 para a precisão quando a Oracle não fornece essas informações. Se esta caixa de seleção for limpa, o driver retornará 0 para estes tipos de colunas.  
  
2.  Clique em Adicionar para adicionar outra fonte de dados ou clique em Fechar para sair.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Para modificar uma fonte de dados para o Windows  
  
1.  Abra o administrador de origem de dados do ODBC. Clique na guia DSN apropriada.  
  
2.  Selecione a fonte de dados Oracle que deseja modificar e clique em Configurar. A caixa de diálogo Configuração do Microsoft ODBC para Oracle é exibida.  
  
3.  Modifique os campos de origem de dados aplicáveis e clique em OK.  
  
 Quando você terminar de modificar as informações nesta caixa de diálogo, o administrador do ODBC atualiza as informações do registro.
