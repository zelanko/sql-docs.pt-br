---
title: O Gerenciador de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 686a2b9673fb392f969a42f4cc86dd95a95668a6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286790"
---
# <a name="the-driver-manager"></a>O Gerenciador de Driver
O *Gerenciador de driver* é uma biblioteca que gerencia a comunicação entre aplicativos e drivers. Por exemplo, em plataformas Microsoft® Windows®, o Gerenciador de driver é uma DLL (biblioteca de vínculo dinâmico) escrita pela Microsoft e pode ser redistribuída por usuários do SDK redistribuível do MDAC 2,8 SP1.  
  
 O Gerenciador de driver existe principalmente como uma conveniência para os gravadores de aplicativos e resolve vários problemas comuns a todos os aplicativos. Isso inclui determinar qual driver carregar com base em um nome de fonte de dados, carregar e descarregar drivers e chamar funções em drivers.  
  
 Para ver por que o segundo é um problema, considere o que aconteceria se o aplicativo chamasse funções diretamente no driver. A menos que o aplicativo tenha sido vinculado diretamente a um driver específico, ele teria que criar uma tabela de ponteiros para as funções nesse driver e chamar essas funções por ponteiro. Usar o mesmo código para mais de um driver por vez adicionaria outro nível de complexidade. O aplicativo primeiro precisaria definir um ponteiro de função para apontar para a função correta no driver correto e, em seguida, chamar a função por meio desse ponteiro.  
  
 O Gerenciador de driver resolve esse problema fornecendo um único local para chamar cada função. O aplicativo é vinculado ao Gerenciador de driver e chama funções ODBC no Gerenciador de driver, não no driver. O aplicativo identifica o driver de destino e a fonte de dados com um *identificador de conexão*. Quando ele carrega um driver, o Gerenciador de driver cria uma tabela de ponteiros para as funções nesse driver. Ele usa o identificador de conexão passado pelo aplicativo para localizar o endereço da função no driver de destino e chama essa função por endereço.  
  
 Para a maior parte, o Gerenciador de driver apenas passa chamadas de função do aplicativo para o driver correto. No entanto, ele também implementa algumas funções (**Sqldatasourcees**, **sqldriveers**e **SQLGetFunctions**) e executa a verificação básica de erros. Por exemplo, o Gerenciador de driver verifica se os identificadores não são ponteiros nulos, se as funções são chamadas na ordem correta e se determinados argumentos de função são válidos. Para obter uma descrição completa dos erros verificados pelo Gerenciador de driver, consulte a seção de referência para cada função e [Apêndice B: tabelas de transição de estado ODBC](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 A função principal final do Gerenciador de driver é carregar e descarregar drivers. O aplicativo carrega e descarrega apenas o Gerenciador de driver. Quando desejar usar um driver específico, ele chamará uma função de conexão (**SQLConnect**, **SQLDriverConnect**ou **SQLBrowseConnect**) no Gerenciador de driver e especificará o nome de uma fonte de dados ou driver específico, como "accounting" ou "SQL Server". Usando esse nome, o Gerenciador de driver pesquisa as informações da fonte de dados para o nome do arquivo do driver, como sqlsrvr. dll. Em seguida, ele carrega o driver (supondo que ele ainda não esteja carregado), armazena o endereço de cada função no driver e chama a função de conexão no driver, que então se inicializa e se conecta à fonte de dados.  
  
 Quando o aplicativo é feito usando o driver, ele chama **SQLDisconnect** no Gerenciador de driver. O Gerenciador de driver chama essa função no driver, que se desconecta da fonte de dados. No entanto, o Gerenciador de driver mantém o driver na memória, caso o aplicativo se reconecte a ele. Ele descarrega o driver somente quando o aplicativo libera a conexão usada pelo driver ou usa a conexão para um driver diferente e nenhuma outra conexão usa o driver. Para obter uma descrição completa da função do Gerenciador de driver no carregamento e descarregamento de drivers, consulte [função do Gerenciador de driver no processo de conexão](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).
