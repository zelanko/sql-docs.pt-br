---
title: O Gerente de Motorista | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286790"
---
# <a name="the-driver-manager"></a>O Gerenciador de Driver
O *Driver Manager* é uma biblioteca que gerencia a comunicação entre aplicativos e drivers. Por exemplo, nas plataformas Microsoft® Windows®, o Driver Manager é uma biblioteca de links dinâmicos (DLL) que é escrita pela Microsoft e pode ser redistribuída pelos usuários do Redistributable MDAC 2.8 SP1 SDK.  
  
 O Driver Manager existe principalmente como uma conveniência para os escritores de aplicativos e resolve uma série de problemas comuns a todos os aplicativos. Isso inclui determinar qual driver carregar com base no nome de uma fonte de dados, carregar e descarregar drivers e chamar funções em drivers.  
  
 Para ver por que este último é um problema, considere o que aconteceria se o aplicativo ligasse diretamente para funções no driver. A menos que o aplicativo estivesse ligado diretamente a um driver específico, ele teria que construir uma tabela de ponteiros para as funções naquele driver e chamar essas funções por ponteiro. Usar o mesmo código para mais de um driver de cada vez adicionaria ainda outro nível de complexidade. O aplicativo teria primeiro que definir um ponteiro de função para apontar para a função correta no driver correto e, em seguida, chamar a função através desse ponteiro.  
  
 O Driver Manager resolve esse problema fornecendo um único lugar para chamar cada função. O aplicativo é vinculado ao Driver Manager e chama as funções oDBC no Driver Manager, não no driver. O aplicativo identifica o driver de destino e a fonte de dados com uma *alça de conexão*. Quando ele carrega um driver, o Driver Manager constrói uma tabela de ponteiros para as funções desse driver. Ele usa a alça de conexão passada pelo aplicativo para encontrar o endereço da função no driver de destino e chamadas que funcionam por endereço.  
  
 Na maioria das vezes, o Driver Manager apenas passa chamadas de função do aplicativo para o driver correto. No entanto, ele também implementa algumas funções (**SQLDataSources,** **SQLDrivers**e **SQLGetFunctions**) e realiza verificação básica de erros. Por exemplo, o Gerenciador de driver verifica se as alças não são ponteiros nulos, que as funções são chamadas na ordem correta e que certos argumentos de função são válidos. Para obter uma descrição completa dos erros verificados pelo Driver Manager, consulte a seção de referência para cada função e [o apêndice B: Tabelas de transição do estado ODBC](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 O papel principal final do Driver Manager é carregar e descarregar motoristas. O aplicativo carrega e descarrega apenas o Driver Manager. Quando ele quer usar um driver específico, ele chama uma função de conexão (**SQLConnect,** **SQLDriverConnect**ou **SQLBrowseConnect**) no Gerenciador de driver e especifica o nome de uma determinada fonte de dados ou driver, como "Contabilidade" ou "SQL Server". Usando esse nome, o Driver Manager pesquisa as informações de origem de dados para o nome do arquivo do driver, como Sqlsrvr.dll. Em seguida, ele carrega o driver (assumindo que ele ainda não está carregado), armazena o endereço de cada função no driver, e chama a função de conexão no driver, que então se inicia e se conecta à fonte de dados.  
  
 Quando o aplicativo é feito usando o driver, ele chama **SQLDisconnect** no Gerenciador de driver. O Gerenciador de driver sinstade essa função no driver, que se desconecta da fonte de dados. No entanto, o Driver Manager mantém o driver na memória caso o aplicativo se reconecte a ele. Ele descarrega o driver somente quando o aplicativo libera a conexão usada pelo motorista ou usa a conexão para um motorista diferente, e nenhuma outra conexão usa o motorista. Para obter uma descrição completa da função do Driver Manager no carregamento e descarga de drivers, consulte [a função do driver manager no processo de conexão](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).
