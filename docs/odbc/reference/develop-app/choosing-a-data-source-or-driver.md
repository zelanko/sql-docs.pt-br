---
title: Escolhendo uma Fonte de Dados ou Driver | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303367"
---
# <a name="choosing-a-data-source-or-driver"></a>Escolher uma fonte de dados ou um driver
A fonte de dados ou driver usado por um aplicativo às vezes é codificado no aplicativo. Por exemplo, um aplicativo personalizado escrito por um departamento do MIS para transferir dados de uma fonte de dados para outra conteria os nomes dessas fontes de dados - o aplicativo simplesmente não funcionaria com nenhuma outra fonte de dados. Outro exemplo é uma aplicação vertical, como uma usada para entrada de pedidos. Tal aplicativo sempre usa a mesma fonte de dados, que tem um esquema predefinido conhecido pelo aplicativo.  
  
 Outros aplicativos selecionam a fonte de dados ou o driver em tempo de execução. Geralmente, são aplicativos genéricos que fazem consultas ad hoc, como uma planilha que usa o ODBC para importar dados. Esses aplicativos geralmente listam as fontes de dados ou drivers disponíveis e permitem que os usuários escolham os com quem querem trabalhar. Se um aplicativo genérico lista fontes de dados, drivers ou ambos frequentemente depende se o aplicativo usa drivers baseados em DBMS ou baseados em arquivos.  
  
 Os drivers baseados em DBMS geralmente exigem um conjunto complexo de informações de conexão, como o endereço da rede, o protocolo de rede, o nome do banco de dados e assim por diante. O objetivo de uma fonte de dados é ocultar todas essas informações. Portanto, o paradigma de fonte de dados se presta a ser usado com drivers baseados em DBMS. Um aplicativo pode exibir uma lista de fontes de dados para o usuário de uma das duas maneiras. Ele pode chamar **SQLDriverConnect** com a palavra-chave **DSN** (Data Source Name) e sem valor associado; o Gerenciador de driver exibirá uma lista de nomes de origem de dados. Se o aplicativo quiser controle sobre a aparência da lista, ele chama **SQLDataSources** para recuperar uma lista de fontes de dados disponíveis e constrói sua própria caixa de diálogo. Esta função é implementada pelo Driver Manager e pode ser chamada antes de qualquer driver ser carregado. O aplicativo então chama uma função de conexão e passa-a o nome da fonte de dados escolhida.  
  
 Se uma fonte de dados não for especificada, a fonte de dados padrão indicada pelas informações do sistema será usada. (Para obter mais informações, consulte [Subchave padrão](../../../odbc/reference/install/default-subkey.md).) Se **o SQLConnect** for chamado usando um argumento *ServerName* que não pode ser encontrado, é um ponteiro nulo ou é "DEFAULT", o Gerenciador de driver se conecta à fonte de dados padrão. A fonte de dados padrão também é usada se a seqüência de conexão usada em uma chamada para **SQLDriverConnect** ou **SQLBrowseConnect** contiver a palavra-chave **DSN** definida como "DEFAULT" ou se a fonte de dados especificada não for encontrada. Além disso, a fonte de dados padrão é usada se a seqüência de conexão usada em uma chamada para **SQLDriverConnect** não contiver a palavra-chave **DSN.**  
  
 Com drivers baseados em arquivos, é possível usar um paradigma de arquivo. Para dados armazenados no computador local, os usuários frequentemente sabem que seus dados estão em um determinado arquivo, como Employee.dbf. Em vez de selecionar uma fonte de dados desconhecida, é mais fácil para esses usuários selecionar o arquivo que eles conhecem. Para implementar isso, o aplicativo primeiro chama **SQLDrivers**. Esta função é implementada pelo Driver Manager e pode ser chamada antes de qualquer driver ser carregado. **SQLDrivers** retorna uma lista de drivers disponíveis; ele também retorna valores para as palavras-chave **FileUsage** e **FileExtns.** A palavra-chave **FileUsage** explica se os drivers baseados em arquivos tratam os arquivos como tabelas, assim como o Xbase ou como bancos de dados, assim como o Microsoft® Access. A palavra-chave **FileExtns** lista as extensões de nome de arquivo que o driver reconhece, como .dbf para um driver Xbase. Usando essas informações, o aplicativo constrói uma caixa de diálogo através da qual o usuário escolhe um arquivo. Com base na extensão do arquivo escolhido, o aplicativo se conecta ao driver ligando para **SQLDriverConnect** com a palavra-chave **DRIVER.**  
  
 Não há nada que impeça um aplicativo de usar uma fonte de dados com um driver baseado em arquivos ou ligar para o **SQLDriverConnect** com a palavra-chave **DRIVER** para se conectar a um driver baseado em DBMS. Aqui estão vários usos comuns da palavra-chave **DRIVER** para drivers baseados em DBMS:  
  
-   **Não criando fontes de dados.** Por exemplo, um aplicativo personalizado pode usar um driver e um banco de dados específicos. Se o nome do driver e todas as informações necessárias para se conectar ao banco de dados forem codificados no aplicativo, os usuários não precisem criar uma fonte de dados em seu computador para executar o aplicativo. Tudo o que eles devem fazer é instalar o aplicativo e o driver.  
  
     Uma desvantagem desse método é que o aplicativo deve ser recompilado e redistribuído se as informações de conexão mudarem. Se um nome de origem de dados for codificado no aplicativo em vez de informações completas de conexão, cada usuário deve alterar apenas as informações na fonte de dados.  
  
-   **Acessando um DBMS específico uma única vez.** Por exemplo, uma planilha que recupera dados ligando para funções ODBC pode conter a palavra-chave **DRIVER** para identificar um driver específico. Como o nome do motorista é significativo para qualquer usuário que tenha esse driver, a planilha pode ser passada entre esses usuários. Se a planilha contivesse um nome de origem de dados, cada usuário teria que criar a mesma fonte de dados para usar a planilha.  
  
-   **Navegando no sistema para todos os bancos de dados acessíveis a um determinado driver.** Para obter mais informações, consulte [Conectando com SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md), mais tarde nesta seção.
