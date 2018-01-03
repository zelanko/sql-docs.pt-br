---
title: Escolha de dados de um fonte ou Driver | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 496b9a40dfa1beb27144eead8d8ab9b03056b000
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="choosing-a-data-source-or-driver"></a>Escolha de dados de um fonte ou Driver
A fonte de dados ou driver usado por um aplicativo às vezes é embutido no aplicativo. Por exemplo, um aplicativo personalizado escrito por um departamento de MIS para transferir dados de uma fonte de dados para outro conterá os nomes das fontes de dados, o aplicativo simplesmente não funciona com outras fontes de dados. Outro exemplo é um aplicativo vertical, como aquele usado para entrada de ordem. Esse aplicativo sempre usa a mesma fonte de dados, que tem um esquema predefinido conhecido pelo aplicativo.  
  
 Outros aplicativos selecione a fonte de dados ou driver em tempo de execução. Normalmente, esses são aplicativos genéricos que fazer consultas ad hoc, como uma planilha que usa ODBC para importar dados. Esses aplicativos geralmente listam as fontes de dados disponíveis ou drivers e permitir que os usuários escolher aqueles que desejam trabalhar com. Se um aplicativo genérico lista fontes de dados, drivers ou ambos frequentemente depende se o aplicativo usa drivers baseados em DBMS ou baseada em arquivo.  
  
 Drivers baseados em DBMS normalmente requerem um conjunto complexo de informações de conexão, como o endereço de rede, o protocolo de rede, nome do banco de dados e assim por diante. A finalidade de uma fonte de dados é ocultar todas essas informações. Portanto, o paradigma de fonte de dados se presta a ser usado com drivers baseados em DBMS. Um aplicativo pode exibir uma lista de fontes de dados para o usuário de uma das duas maneiras. Ele pode chamar **SQLDriverConnect** com o **DSN** palavra-chave (nome de fonte de dados) e nenhum valor associada; o Gerenciador de Driver exibirá uma lista de nomes de fonte de dados. Se o aplicativo deseja controlar a aparência da lista, ele chama **SQLDataSources** para recuperar uma lista de disponíveis fontes de dados e cria sua própria caixa de diálogo. Essa função é implementada pelo Gerenciador de Driver e pode ser chamada antes de todos os drivers são carregados. Em seguida, o aplicativo chama uma função de conexão e passa o nome da fonte de dados escolhido.  
  
 Se uma fonte de dados não for especificada, a fonte de dados padrão indicada pelas informações de sistema será usada. (Para obter mais informações, consulte [padrão subchave](../../../odbc/reference/install/default-subkey.md).) Se **SQLConnect** é chamado usando um *ServerName* argumento não pode ser encontrado, um ponteiro nulo, ou "Padrão", o Gerenciador de Driver se conecta à fonte de dados padrão. O padrão de fonte de dados também é usada se a conexão de cadeia de caracteres que é usado em uma chamada para **SQLDriverConnect** ou **SQLBrowseConnect** contém o **DSN** palavra-chave definida como "padrão "ou se a fonte de dados especificado não foi encontrada. Além disso, o padrão de fonte de dados será usada se a conexão de cadeia de caracteres que é usado em uma chamada para **SQLDriverConnect** não contém o **DSN** palavra-chave.  
  
 Com drivers baseados em arquivo, é possível usar um paradigma de arquivo. Para dados armazenados no computador local, os usuários frequentemente saber que os dados estão em um arquivo específico, como Employee. dbf. Em vez de selecionar uma fonte de dados desconhecido, é mais fácil para que esses usuários selecionar o arquivo que eles saibam. Para implementar isso, o aplicativo primeiro chama **SQLDrivers**. Essa função é implementada pelo Gerenciador de Driver e pode ser chamada antes de todos os drivers são carregados. **SQLDrivers** retorna uma lista de drivers disponíveis; ele também retorna valores para o **FileUsage** e **FileExtns** palavras-chave. O **FileUsage** palavra-chave explica se drivers baseados em arquivo tratam arquivos como tabelas, como não Xbase ou, como bancos de dados, como faz o Microsoft® Access. O **FileExtns** palavra-chave lista as extensões de nome de arquivo de driver reconhece, como. dbf para um driver Xbase. Usando essas informações, o aplicativo cria uma caixa de diálogo por meio do qual o usuário escolhe um arquivo. Com base na extensão do arquivo escolhido, o aplicativo se conecta ao driver chamando **SQLDriverConnect** com o **DRIVER** palavra-chave.  
  
 Não há nada para parar um aplicativo usando uma fonte de dados com um driver com base em arquivo ou chamar **SQLDriverConnect** com o **DRIVER** palavra-chave para se conectar a um driver de DBMS. Aqui estão vários usos comuns para o **DRIVER** palavra-chave de drivers baseados em DBMS:  
  
-   **Não criar fontes de dados.** Por exemplo, um aplicativo personalizado pode usar um driver específico e o banco de dados. Se o nome do driver e todas as informações necessárias para se conectar ao banco de dados é inserido no código do aplicativo, os usuários não precisam criar uma fonte de dados em seu computador para executar o aplicativo. Todos eles devem fazer é instalar o aplicativo e o driver.  
  
     Uma desvantagem desse método é que o aplicativo deve ser recompilado e redistribuído se altera as informações de conexão. Se um nome de fonte de dados é inserido no código do aplicativo em vez das informações de conexão completa, cada usuário deve alterar apenas as informações na fonte de dados.  
  
-   **Acessando um DBMS específico em uma única vez.** Por exemplo, uma planilha que recupera dados chamando funções ODBC pode conter o **DRIVER** palavra-chave para identificar um driver específico. Como o nome do driver é significativo para todos os usuários que têm esse driver, a planilha pode ser passada entre os usuários. Se a planilha contiver um nome de fonte de dados, cada usuário teria que criar a mesma fonte de dados para usar a planilha.  
  
-   **O sistema para todos os bancos de dados acessíveis para um determinado driver de navegação.** Para obter mais informações, consulte [conectando com SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md), mais adiante nesta seção.
