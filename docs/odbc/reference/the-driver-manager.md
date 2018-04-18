---
title: O Gerenciador de Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f33e9b5ebd9ae699240170990b7daeeaefbea8e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="the-driver-manager"></a>O Gerenciador de Driver
O *Gerenciador de Driver* é uma biblioteca que gerencia a comunicação entre aplicativos e drivers. Por exemplo, em plataformas Microsoft® Windows®, o Gerenciador de Driver é uma biblioteca de vínculo dinâmico (DLL) que foi criada pela Microsoft e pode ser redistribuída por usuários do SDK do SP1 redistributable MDAC 2.8.  
  
 O Gerenciador de Driver existe principalmente como uma conveniência para autores de aplicativos e resolver vários problemas comuns a todos os aplicativos. Isso inclui determinar qual driver carregar com base em um nome de fonte de dados, carregar e descarregar drivers e chamando funções em drivers.  
  
 Para ver por que o segundo é um problema, considere o que aconteceria se o aplicativo chamado funções no driver diretamente. A menos que o aplicativo foi vinculado diretamente a um driver específico, seria necessário criar uma tabela de ponteiros para funções no driver e chamar essas funções pelo ponteiro. Usando o mesmo código para mais de um driver por vez, você adicionaria outro nível de complexidade. O aplicativo primeiro deve definir um ponteiro de função para apontar para a função correta no driver correto e, em seguida, chame a função através desse ponteiro.  
  
 O Gerenciador de Driver resolve esse problema, fornecendo um único local para chamar cada função. O aplicativo está vinculado as funções ODBC Gerenciador de Driver e chamadas no Gerenciador de Driver, não o driver. O aplicativo identifica a fonte de dados e o driver de destino com um *identificador de conexão*. Ao carregar um driver, o Gerenciador de Driver cria uma tabela de ponteiros para as funções no driver. Ele usa o identificador de conexão passado pelo aplicativo para localizar o endereço da função no driver de destino e chama a função pelo endereço.  
  
 A maior parte do tempo, o Gerenciador de Driver apenas transmite chamadas de função do aplicativo para o driver correto. No entanto, ele também implementa algumas funções (**SQLDataSources**, **SQLDrivers**, e **SQLGetFunctions**) e executa a verificação de erro básico. Por exemplo, o Gerenciador de Driver verifica identificadores não são ponteiros nulos, que são chamadas de funções na ordem correta, e que alguns argumentos de função são válidos. Para obter uma descrição completa dos erros verificados pelo Gerenciador de Driver, consulte a seção de referência para cada função e [tabelas de transição de estado do apêndice b: ODBC](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 A função principal final do Gerenciador de Driver é carregar e descarregar drivers. O aplicativo carrega e descarrega o Gerenciador de Driver. Quando desejar usar um driver específico, ele chama uma função de conexão (**SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**) no Gerenciador de Driver e especifica o nome de uma determinada fonte de dados ou driver, como "Contabilidade" ou "SQL Server". Usando esse nome, o Gerenciador de Driver pesquisas de informações de fonte de dados para o nome do arquivo do driver, como Sqlsrvr.dll. Em seguida, carrega o driver (supondo que ainda não foi carregado), armazena o endereço de cada função no driver e chama a função de conexão no driver que inicializa a próprio e conecta-se à fonte de dados.  
  
 Quando o aplicativo é feito usando o driver, ele chama **SQLDisconnect** no Gerenciador de Driver. O Gerenciador de Driver chamará essa função no driver, desconecta da fonte de dados. No entanto, o Gerenciador de Driver mantém o driver na memória, no caso do aplicativo se reconecta a ele. Ele descarrega o driver somente quando o aplicativo libera a conexão usada pelo driver ou usa a conexão para um driver diferente, e nenhuma outra conexão usa o driver. Para obter uma descrição completa da função do Gerenciador de Driver em carregar e descarregar drivers, consulte [do Gerenciador de Driver de função no processo de Conexão](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).
