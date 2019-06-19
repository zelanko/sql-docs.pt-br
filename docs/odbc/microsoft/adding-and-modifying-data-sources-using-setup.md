---
title: Adicionando e modificando dados usando a instalação de fontes | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 953563285d3c62a8523079a604cf607f2e0edf62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63219106"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Adicionar e modificar fontes de dados usando a instalação
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Uma fonte de dados identifica um caminho para os dados que podem incluir uma biblioteca de rede, servidor, banco de dados e outros atributos – nesse caso, a fonte de dados é o caminho para um banco de dados Oracle. Para se conectar a uma fonte de dados, o Gerenciador de Driver verifica o registro do Windows para obter informações de conexão específica.  
  
 A entrada do registro criada pelo administrador de fonte de dados ODBC é usada pelos drivers de Gerenciador de Driver ODBC e ODBC. Esta entrada contém informações sobre cada fonte de dados e seu driver associado. Antes de você pode se conectar a uma fonte de dados, suas informações de conexão devem ser adicionadas ao registro.  
  
 Para adicionar e configurar fontes de dados, use o [administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md). O administrador de ODBC atualiza suas informações de conexão de fonte de dados. Conforme você adiciona fontes de dados, o administrador de ODBC atualiza as informações de registro para você.  
  
### <a name="to-add-a-data-source-for-windows"></a>Para adicionar uma fonte de dados para Windows  
  
1.  Abra o administrador de fonte de dados ODBC.  
  
2.  Na caixa de diálogo Administrador de fonte de dados ODBC, clique em Adicionar. A caixa de diálogo Criar nova fonte de dados é exibida.  
  
3.  Selecione o Microsoft ODBC para Oracle e, em seguida, clique em Concluir. O Microsoft ODBC para a caixa de diálogo de configuração do Oracle é exibida.  
  
4.  Na caixa Nome da fonte de dados, digite o nome da fonte de dados que você deseja acessar. Ele pode ser qualquer nome que você escolher.  
  
5.  Na caixa Descrição, digite a descrição para o driver. Esse campo opcional descreve o driver de banco de dados que a fonte de dados se conecta ao. Ele pode ser qualquer nome que você escolher.  
  
6.  Na caixa de nome de usuário, digite seu nome de usuário de banco de dados (sua ID de usuário de banco de dados).  
  
7.  Na caixa do servidor, digite o Alias de banco de dados ou conectar-se a cadeia de caracteres para o mecanismo do servidor Oracle que você deseja acessar.  
  
8.  Clique em Okey para adicionar essa fonte de dados.  
  
> [!NOTE]  
>  A caixa de diálogo de fontes de dados é exibida e o administrador de ODBC atualiza as informações de registro. O usuário nomear e conecte-se a cadeia de caracteres que você digitou tornam-se os valores de conexão padrão para esta fonte de dados quando você se conecta a ele.  
  
1.  Clique em criar opções mais especificações sobre o Driver ODBC para a instalação do Oracle:  
  
    -   **Tradução** -clique em Selecionar para escolher um conversor de dados carregado. O padrão é \<tradutor não >.  
  
    -   **Desempenho** -comentários de incluir a caixa de seleção de funções de catálogo que especifica se o driver retorna colunas de comentários para o [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) conjunto de resultados. O Driver ODBC para Oracle fornece acesso mais rápido quando esse valor não está definido.  
  
         Os SINÔNIMOS incluem na caixa de seleção de colunas do SQL Especifica se o driver retorna informações de coluna. **Tamanho do buffer** Especifica o tamanho, em bytes, alocada para receber dados buscados. O driver otimiza a busca de forma que uma busca no servidor Oracle retorne linhas suficientes para preencher um buffer do tamanho especificado. Valores maiores tendem a aumentar o desempenho ao buscar muitos dados.  
  
    -   **Personalização** -caixa de seleção o impor ODBC DayOfWeek padrão Especifica se o conjunto de resultados estarão em conformidade com o formato de dia da semana especificado do ODBC (domingo = 1; Sábado = 7). Se essa caixa de seleção estiver desmarcada, o valor de Oracle específica de localidade é retornado.  
  
         O SQLDescribeCol **sempre retorna um valor de precisão** caixa de seleção Especifica se o driver deve retornar um valor diferente de zero para o *cbColDef* argumento de **SQLDescribeCol**. Esse atributo de cadeia de caracteres de conexão se aplica somente às colunas onde houver sem escala definidas para Oracle, por exemplo, calculado numéricas colunas e as colunas definidas como número sem uma escala ou precisão. Um **SQLDescribeCol** chamar retorna 130 para a precisão quando Oracle não fornece essas informações. Se essa caixa de seleção estiver desmarcada, o driver retornará 0 para esses tipos de colunas.  
  
2.  Clique em Adicionar para adicionar outra fonte de dados, ou clique em Fechar para sair.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Para modificar uma fonte de dados para Windows  
  
1.  Abra o administrador de fonte de dados ODBC. Clique na guia DSN apropriada.  
  
2.  Selecione a fonte de dados Oracle que você deseja modificar e, em seguida, clique em configurar. O Microsoft ODBC para a caixa de diálogo de configuração do Oracle é exibida.  
  
3.  Modifique os campos de fonte de dados aplicável e, em seguida, clique em Okey.  
  
 Quando você tiver terminado de modificar as informações na caixa de diálogo, o administrador de ODBC atualiza as informações de registro.
