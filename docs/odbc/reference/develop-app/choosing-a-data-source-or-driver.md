---
title: Escolha de dados de um fonte ou Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c238b89f6fefbb158c50531d28d2c234c64f64bf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507634"
---
# <a name="choosing-a-data-source-or-driver"></a>Escolher uma fonte de dados ou um driver
A fonte de dados ou o driver usado por um aplicativo às vezes é embutido em código no aplicativo. Por exemplo, um aplicativo personalizado escrito por um departamento de MIS para transferir dados de uma fonte de dados para outro contém os nomes desses dados de fontes – o aplicativo simplesmente não funcionariam com outras fontes de dados. Outro exemplo é um aplicativo vertical, como aquele usado para entrada de ordem. Esse aplicativo sempre usa a mesma fonte de dados, que tem um esquema predefinido conhecido pelo aplicativo.  
  
 Outros aplicativos selecione a fonte de dados ou o driver no tempo de execução. Normalmente, esses são aplicativos genéricos que fazer consultas ad hoc, como uma planilha que usa o ODBC para importar dados. Esses aplicativos geralmente listam as fontes de dados disponíveis ou os drivers e permitir que os usuários a escolher aqueles que desejam trabalhar com. Se um aplicativo genérico lista fontes de dados, drivers ou ambos com frequência depende se o aplicativo usa os drivers com base em arquivo ou DBMS.  
  
 Drivers baseados em DBMS geralmente exigem um conjunto complexo de informações de conexão, como o endereço de rede, protocolo de rede, nome do banco de dados e assim por diante. A finalidade de uma fonte de dados é ocultar todas essas informações. Portanto, o paradigma de fonte de dados presta-se para usar com drivers baseados em DBMS. Um aplicativo pode exibir uma lista de fontes de dados para o usuário em uma das duas maneiras. Ele pode chamar **SQLDriverConnect** com o **DSN** palavra-chave (nome de fonte de dados) e nenhum valor associado; o Gerenciador de Driver exibirá uma lista de nomes de fonte de dados. Se o aplicativo deseja controlar a aparência da lista, ele chama **SQLDataSources** para recuperar uma lista de disponíveis fontes de dados e constrói sua própria caixa de diálogo. Essa função é implementada pelo Gerenciador de Driver e pode ser chamada antes que todos os drivers são carregados. O aplicativo, em seguida, chama uma função de conexão e passa o nome da fonte de dados escolhido.  
  
 Se uma fonte de dados não for especificada, a fonte de dados padrão indicada pelas informações do sistema é usada. (Para obter mais informações, consulte [subchave padrão](../../../odbc/reference/install/default-subkey.md).) Se **SQLConnect** é chamado usando uma *ServerName* argumento que não pode ser encontrado, for um ponteiro nulo ou é "Padrão", o Gerenciador de Driver se conecta à fonte de dados padrão. O padrão de fonte de dados também será usada se a conexão de cadeia de caracteres que é usado em uma chamada para **SQLDriverConnect** ou **SQLBrowseConnect** contém o **DSN** palavra-chave é definido como "padrão "ou se a fonte de dados especificado não for encontrada. Além disso, o padrão de fonte de dados será usada se a conexão de cadeia de caracteres que é usado em uma chamada para **SQLDriverConnect** não contém o **DSN** palavra-chave.  
  
 Com drivers baseados em arquivo, é possível usar um paradigma de arquivo. Para dados armazenados no computador local, os usuários frequentemente sabem que seus dados estão em um arquivo específico, como Employee. dbf. Em vez de selecionar uma fonte de dados desconhecido, é mais fácil para esses usuários selecionar o arquivo que eles conhecem. Para implementar isso, o aplicativo primeiro chama **SQLDrivers**. Essa função é implementada pelo Gerenciador de Driver e pode ser chamada antes que todos os drivers são carregados. **SQLDrivers** retorna uma lista de drivers disponíveis; ele também retorna valores para o **FileUsage** e **FileExtns** palavras-chave. O **FileUsage** palavra-chave explica se drivers baseados em arquivo tratam arquivos como tabelas, como não Xbase, ou seja, como bancos de dados, como faz o Microsoft® Access. O **FileExtns** palavra-chave lista as extensões de nome de arquivo de driver reconhece, como. dbf para um driver do Xbase. Usando essas informações, o aplicativo constrói uma caixa de diálogo por meio do qual o usuário escolhe um arquivo. Com base na extensão do arquivo escolhido, o aplicativo, em seguida, conecta-se para o driver chamando **SQLDriverConnect** com o **DRIVER** palavra-chave.  
  
 Não há nada para interromper um aplicativo usando uma fonte de dados com um driver com base em arquivo ou chamando **SQLDriverConnect** com o **DRIVER** palavra-chave para se conectar a um driver baseados em DBMS. Aqui estão vários usos comuns do **DRIVER** palavra-chave para drivers baseados em DBMS:  
  
-   **Não criar fontes de dados.** Por exemplo, um aplicativo personalizado pode usar um driver específico e o banco de dados. Se o nome do driver e todas as informações necessárias para se conectar ao banco de dados é embutido em código no aplicativo, os usuários não precisarão criar uma fonte de dados em seu computador para executar o aplicativo. Tudo o que eles devem fazer é instalar o aplicativo e o driver.  
  
     Uma desvantagem desse método é que o aplicativo deve ser recompilado e redistribuído se as informações de conexão for alterada. Se um nome de fonte de dados é embutido no código do aplicativo em vez de informações de conexão completa, cada usuário deve alterar apenas as informações na fonte de dados.  
  
-   **Acessando um DBMS específico em uma única vez.** Por exemplo, uma planilha que recupera dados chamando funções ODBC pode conter os **DRIVER** palavra-chave para identificar um driver específico. Como o nome do driver é significativo para todos os usuários que têm esse driver, a planilha pode ser passada entre esses usuários. Se a planilha continha um nome de fonte de dados, cada usuário precisa que criar a mesma fonte de dados para usar a planilha.  
  
-   **O sistema para todos os bancos de dados acessíveis para um determinado driver de navegação.** Para obter mais informações, consulte [conectando com SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md), mais adiante nesta seção.
