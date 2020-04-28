---
title: Escolhendo uma fonte de dados ou um driver | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b10aafad95463f56ec0f5a029eac59a02cff003b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303367"
---
# <a name="choosing-a-data-source-or-driver"></a>Escolher uma fonte de dados ou um driver
A fonte de dados ou o driver usado por um aplicativo, às vezes, é embutido em código no aplicativo. Por exemplo, um aplicativo personalizado escrito por um departamento de MIS para transferir dados de uma fonte de dados para outra conteria os nomes dessas fontes de dados: o aplicativo simplesmente não funcionaria com nenhuma outra fonte de dados. Outro exemplo é um aplicativo vertical, como um usado para a entrada de pedidos. Esse aplicativo sempre usa a mesma fonte de dados, que tem um esquema predefinido conhecido pelo aplicativo.  
  
 Outros aplicativos selecione a fonte de dados ou o driver em tempo de execução. Normalmente, esses são aplicativos genéricos que fazem consultas ad hoc, como uma planilha que usa o ODBC para importar dados. Esses aplicativos geralmente listam as fontes de dados ou os drivers disponíveis e permitem que os usuários escolham aqueles com os quais desejam trabalhar. Se um aplicativo genérico lista fontes de dados, drivers ou ambos frequentemente depende se o aplicativo usa drivers baseados em DBMS ou em arquivo.  
  
 Os drivers baseados em DBMS geralmente exigem um conjunto complexo de informações de conexão, como o endereço de rede, o protocolo de rede, o nome do banco de dados e assim por diante. A finalidade de uma fonte de dados é ocultar todas essas informações. Portanto, o paradigma da fonte de dados se presta para uso com drivers baseados em DBMS. Um aplicativo pode exibir uma lista de fontes de dados para o usuário de uma das duas maneiras. Ele pode chamar **SQLDriverConnect** com a palavra-chave **DSN** (nome da fonte de dados) e nenhum valor associado; o Gerenciador de driver exibirá uma lista de nomes de fonte de dados. Se o aplicativo quiser controlar a aparência da lista, ele chamará **SqlDataSource** para recuperar uma lista de fontes de dados disponíveis e construirá sua própria caixa de diálogo. Essa função é implementada pelo Gerenciador de driver e pode ser chamada antes que qualquer driver seja carregado. Em seguida, o aplicativo chama uma função de conexão e passa o nome da fonte de dados escolhida.  
  
 Se uma fonte de dados não for especificada, a fonte de dados padrão indicada pelas informações do sistema será usada. (Para obter mais informações, consulte [subchave padrão](../../../odbc/reference/install/default-subkey.md).) Se **SQLConnect** for chamado usando um argumento *ServerName* que não pode ser encontrado, é um ponteiro NULL ou é "default", o Gerenciador de driver se conectará à fonte de dados padrão. A fonte de dados padrão também será usada se a cadeia de conexão usada em uma chamada para **SQLDriverConnect** ou **SQLBrowseConnect** contiver a palavra-chave **DSN** definida como "padrão" ou se a fonte de dados especificada não for encontrada. Além disso, a fonte de dados padrão será usada se a cadeia de conexão usada em uma chamada para **SQLDriverConnect** não contiver a palavra-chave **DSN** .  
  
 Com os drivers baseados em arquivo, é possível usar um paradigma de arquivo. Para dados armazenados no computador local, os usuários geralmente sabem que seus dados estão em um arquivo específico, como Employee. dbf. Em vez de selecionar uma fonte de dados desconhecida, é mais fácil para esses usuários selecionarem o arquivo que eles conhecem. Para implementar isso, o aplicativo chama primeiro o **SQLDrivers**. Essa função é implementada pelo Gerenciador de driver e pode ser chamada antes que qualquer driver seja carregado. **Sqldriveres** retorna uma lista de drivers disponíveis; Ele também retorna valores para as palavras-chave **fileusage** e **FileExtns** . A palavra-chave **Fileutilization** explica se os drivers baseados em arquivo tratam arquivos como tabelas, como se é Xbase, ou como bancos de dados, assim como o Microsoft® Access. A palavra-chave **FileExtns** lista as extensões de nome de arquivo que o driver reconhece, como. dbf para um driver Xbase. Usando essas informações, o aplicativo constrói uma caixa de diálogo por meio da qual o usuário escolhe um arquivo. Com base na extensão do arquivo escolhido, o aplicativo se conecta ao driver chamando **SQLDriverConnect** com a palavra-chave do **Driver** .  
  
 Não há nada para impedir um aplicativo de usar uma fonte de dados com um driver baseado em arquivo ou chamar **SQLDriverConnect** com a palavra-chave do **Driver** para se conectar a um driver baseado em DBMS. Aqui estão vários usos comuns da palavra-chave do **Driver** para drivers baseados em DBMS:  
  
-   **Não está criando fontes de dados.** Por exemplo, um aplicativo personalizado pode usar um determinado driver e banco de dados. Se o nome do driver e todas as informações necessárias para se conectar ao banco de dados forem embutidas em código no aplicativo, os usuários não precisarão criar uma fonte de dado em seu computador para executar o aplicativo. Tudo o que eles devem fazer é instalar o aplicativo e o driver.  
  
     Uma desvantagem desse método é que o aplicativo deve ser recompilado e redistribuído se as informações de conexão forem alteradas. Se um nome de fonte de dados for embutido em código no aplicativo em vez de informações de conexão completas, cada usuário deverá alterar apenas as informações na fonte de dados.  
  
-   **Acessar um DBMS específico uma única vez.** Por exemplo, uma planilha que recupera dados chamando funções ODBC pode conter a palavra-chave **Driver** para identificar um driver específico. Como o nome do driver é significativo para qualquer usuário que tenha esse driver, a planilha pode ser passada entre esses usuários. Se a planilha contiver um nome de fonte de dados, cada usuário teria que criar a mesma fonte de dados para usar a planilha.  
  
-   **Navegação no sistema para todos os bancos de dados acessíveis a um driver específico.** Para obter mais informações, consulte [conectando-se com o SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md), mais adiante nesta seção.
