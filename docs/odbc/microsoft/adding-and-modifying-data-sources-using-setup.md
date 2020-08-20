---
description: Adicionar e modificar fontes de dados usando a instalação
title: Adicionando e modificando fontes de dados usando a instalação | Microsoft Docs
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
ms.openlocfilehash: 8592c01897e691cdb6702c4efdfca6054655a793
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494736"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Adicionar e modificar fontes de dados usando a instalação
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Uma fonte de dados identifica um caminho para os dados que podem incluir uma biblioteca de rede, um servidor, um banco de dado e outros atributos – nesse caso, a fonte de dados é o caminho para um Oracle Database. Para se conectar a uma fonte de dados, o Gerenciador de driver verifica as informações de conexão específicas no registro do Windows.  
  
 A entrada do registro criada pelo administrador de fonte de dados ODBC é usada pelo Gerenciador de driver ODBC e drivers ODBC. Essa entrada contém informações sobre cada fonte de dados e seu driver associado. Antes que você possa se conectar a uma fonte de dados, suas informações de conexão devem ser adicionadas ao registro.  
  
 Para adicionar e configurar fontes de dados, use o [administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md). O Administrador ODBC atualiza as informações de conexão da fonte de dados. À medida que você adiciona fontes de dados, o Administrador ODBC atualiza as informações do registro para você.  
  
### <a name="to-add-a-data-source-for-windows"></a>Para adicionar uma fonte de dados ao Windows  
  
1.  Abra o administrador de fonte de dados ODBC.  
  
2.  Na caixa de diálogo administrador de fonte de dados ODBC, clique em Adicionar. A caixa de diálogo Criar nova fonte de dados é exibida.  
  
3.  Selecione Microsoft ODBC para Oracle e clique em concluir. A caixa de diálogo instalação do Microsoft ODBC para Oracle é exibida.  
  
4.  Na caixa nome da fonte de dados, digite o nome da fonte de dados que você deseja acessar. Pode ser qualquer nome que você escolher.  
  
5.  Na caixa Descrição, digite a descrição para o driver. Esse campo opcional descreve o driver de banco de dados ao qual a fonte de dado se conecta. Pode ser qualquer nome que você escolher.  
  
6.  Na caixa nome de usuário, digite o nome de usuário do banco de dados (sua ID de usuário do banco de dados).  
  
7.  Na caixa servidor, digite o alias do banco de dados ou a cadeia de conexão para o mecanismo de servidor Oracle que você deseja acessar.  
  
8.  Clique em OK para adicionar esta fonte de dados.  
  
> [!NOTE]  
>  A caixa de diálogo fontes de dados é exibida e o Administrador ODBC atualiza as informações do registro. O nome de usuário e a cadeia de conexão que você digitou se tornam os valores de conexão padrão para essa fonte de dados quando você se conecta a ele.  
  
1.  As opções de clique fazem mais especificações sobre a configuração do ODBC driver for Oracle:  
  
    -   **Tradução** -clique em selecionar para escolher um tradutor de dados carregado. O padrão é \<No Translator>.  
  
    -   **Desempenho** – a caixa de seleção incluir comentários em funções de catálogo especifica se o driver retorna colunas de comentários para o conjunto de resultados [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) . O ODBC driver for Oracle fornece acesso mais rápido quando esse valor não é definido.  
  
         A caixa de seleção incluir SINÔNIMOs em colunas SQL especifica se o driver retorna informações de coluna. O **tamanho do buffer** especifica o tamanho, em bytes, alocado para receber dados buscados. O driver otimiza a busca para que uma busca do servidor Oracle retorne linhas suficientes para preencher um buffer do tamanho especificado. Valores maiores tendem a aumentar o desempenho ao buscar muitos dados.  
  
    -   **Personalização** – a caixa de seleção aplicar ODBC DayOfWeek padrão especifica se o conjunto de resultados será compatível com o formato de dia da semana especificado do ODBC (domingo = 1; Sábado = 7). Se essa caixa de seleção estiver desmarcada, o valor da Oracle específico à localidade será retornado.  
  
         A caixa de seleção SQLDescribeCol **sempre retorna um valor para precisão** especifica se o driver deve ou não retornar um valor diferente de zero para o argumento *cbColDef* de **SQLDescribeCol**. Esse atributo de cadeia de conexão aplica-se somente a colunas em que não há nenhuma escala definida pela Oracle, como colunas numéricas computadas e colunas definidas como número sem precisão ou escala. Uma chamada **SQLDescribeCol** retorna 130 para a precisão quando o Oracle não fornece essas informações. Se essa caixa de seleção estiver desmarcada, o driver retornará 0 para esses tipos de colunas em vez disso.  
  
2.  Clique em Adicionar para adicionar outra fonte de dados ou clique em fechar para sair.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Para modificar uma fonte de dados do Windows  
  
1.  Abra o administrador de fonte de dados ODBC. Clique na guia DSN apropriada.  
  
2.  Selecione a fonte de dados do Oracle que você deseja modificar e clique em configurar. A caixa de diálogo instalação do Microsoft ODBC para Oracle é exibida.  
  
3.  Modifique os campos de fonte de dados aplicáveis e clique em OK.  
  
 Quando você terminar de modificar as informações nessa caixa de diálogo, o Administrador ODBC atualizará as informações do registro.
