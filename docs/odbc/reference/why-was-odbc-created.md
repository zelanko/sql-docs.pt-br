---
title: Por que o ODBC foi criado? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22173b0ad3dd8abf2d168b41a16a03bc414022ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302777"
---
# <a name="why-was-odbc-created"></a>Por que o ODBC foi criado?
Historicamente, as empresas usavam um único DBMS. Todo o acesso ao banco de dados foi feito através da parte frontal desse sistema ou através de aplicativos escritos para trabalhar exclusivamente com esse sistema. No entanto, à medida que o uso de computadores crescia e mais hardware e software de computador se tornavam disponíveis, as empresas começaram a adquirir diferentes DBMSs. Os motivos foram muitos: as pessoas compravam o que era mais barato, o que era mais rápido, o que já sabiam, o que era mais recente no mercado, o que funcionava melhor para uma única aplicação. Outras razões foram reorganizações e fusões, onde os departamentos que antes tinham um único DBMS agora tinham vários.  
  
 A questão ficou ainda mais complexa com o advento dos computadores pessoais. Esses computadores trouxeram uma série de ferramentas para consulta, análise e exibição de dados, juntamente com uma série de bancos de dados baratos e fáceis de usar. A partir de então, uma única corporação frequentemente tinha dados espalhados por uma miríade de desktops, servidores e minicomputadores, armazenados em uma variedade de bancos de dados incompatíveis, e acessados por um grande número de ferramentas diferentes, poucas das quais poderiam obter todos os dados.  
  
 O desafio final veio com o advento da computação cliente/servidor, que busca fazer o uso mais eficiente dos recursos computacionais. Computadores pessoais baratos (os clientes) sentam-se no desktop e fornecem tanto um front-end gráfico para os dados quanto uma série de ferramentas baratas, como planilhas, programas de gráficos e construtores de relatórios. Minicomputadores e computadores de mainframe (os servidores) hospedam os DBMSs, onde podem usar seu poder de computação e localização central para fornecer acesso rápido e coordenado de dados. Como, então, o software front-end foi conectado aos bancos de dados back-end?  
  
 Um problema semelhante enfrentou fornecedores independentes de software (ISVs). Os fornecedores que escreviam software de banco de dados para minicomputadores e mainframes eram geralmente forçados a escrever uma versão de um aplicativo para cada DBMS ou escrever código específico de DBMS para cada DBMS que quisessem acessar. Os fornecedores que escreviam software para computadores pessoais tinham que escrever rotinas de acesso a dados para cada DBMS diferente com o qual queriam trabalhar. Isso muitas vezes significava que uma enorme quantidade de recursos eram gastos escrevendo e mantendo rotinas de acesso a dados em vez de aplicativos, e os aplicativos eram frequentemente vendidos não em sua qualidade, mas em se eles poderiam acessar dados em um determinado DBMS.  
  
 O que ambos os conjuntos de desenvolvedores precisavam era uma maneira de acessar dados em diferentes DBMSs. O grupo de mainframe e minicomputador precisava de uma maneira de mesclar dados de diferentes DBMSs em um único aplicativo, enquanto o grupo de computador pessoal precisava dessa habilidade, bem como uma maneira de escrever um único aplicativo que fosse independente de qualquer DBMS. Em suma, ambos os grupos precisavam de uma maneira interoperável de acessar dados; eles precisavam de conectividade de banco de dados aberto.
