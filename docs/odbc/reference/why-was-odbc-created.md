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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 871919554975f04fae0aeaa1b8e6ec684c6650a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714143"
---
# <a name="why-was-odbc-created"></a>Por que o ODBC foi criado?
Historicamente, as empresas usavam um único DBMS. Todo o acesso de banco de dados foi feito por meio de front-end de sistema ou de aplicativos escritos para trabalhar exclusivamente com esse sistema. No entanto, conforme o uso de computadores cresceu e mais hardware e software que se tornaram disponíveis, as empresas iniciado para adquirir DBMSs diferentes. Os motivos eram muitos: As pessoas que compraram o que era mais barato, o que era mais rápido, o que eles já sabiam, o que era mais recente do mercado, o que funcionou melhor para um único aplicativo. Outros motivos eram reorganizações e fusões, em que os departamentos que anteriormente tinham um DBMS único agora tinham vários.  
  
 O problema aumentou ainda mais complexo com o advento dos computadores pessoais. Esses computadores colocados em um host de ferramentas para consultar, analisar e exibir dados, junto com um número de bancos de dados de baixo custo, fácil de usar. Daí em seguida diante, uma empresa geralmente tinha dados espalhados por uma grande variedade de áreas de trabalho, servidores e minicomputadores, armazenados em uma variedade de bancos de dados incompatíveis e acessados por um grande número de ferramentas diferentes, alguns dos quais podem chegar a todos os dados.  
  
 O desafio final veio com o advento da computação, de cliente/servidor que procura para tornar o uso mais eficiente dos recursos do computador. Baixo custo pessoal computadores (clientes) ficam na área de trabalho e fornecer os dois gráfico front-end para os dados e uma série de ferramentas de baixo custo, como planilhas, programas e construtores de relatórios de criação de gráficos. Minicomputadores e computadores de mainframe (os servidores) hospedam DBMSs, onde eles podem usar sua capacidade de computação e o local central para fornecer acesso a dados rápido e coordenada. Então, como foi o software de front-end a ser conectado aos bancos de dados back-end?  
  
 Um problema semelhante enfrentado fornecedores de software independentes (ISVs). Fornecedores de escrever um software de banco de dados para minicomputadores e mainframes geralmente eram forçados a grave uma versão de um aplicativo para cada DBMS ou escrever código específico do DBMS para cada DBMS quisessem para acessar. Fornecedores de escrever software para computadores pessoais tinham que escrever rotinas de acesso a dados para cada DBMS diferente com o qual eles queriam trabalhar. Geralmente, isso significava que uma enorme quantidade de recursos foram gastos de escrever e manter rotinas em vez de aplicativos de acesso a dados e aplicativos muitas vezes foram vendidos não sua qualidade mas se eles poderiam acessar dados em um determinado DBMS.  
  
 O que os dois conjuntos de desenvolvedores necessário era uma maneira de acessar dados em DBMSs diferentes. O grupo de mainframe e minicomputador precisava de uma maneira de mesclar dados de DBMSs diferentes em um único aplicativo, enquanto o grupo de computador pessoal necessário essa capacidade, bem como uma maneira de escrever um único aplicativo era independente de qualquer um DBMS. Em resumo, ambos os grupos necessários uma maneira interoperável para acessar dados; eles necessária conectividade aberta de banco de dados.
