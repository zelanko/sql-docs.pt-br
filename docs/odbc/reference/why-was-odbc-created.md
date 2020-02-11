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
ms.openlocfilehash: 8cfdd0babe84d309391b3e1ca546c4e05fdf1331
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68049172"
---
# <a name="why-was-odbc-created"></a>Por que o ODBC foi criado?
Historicamente, as empresas usaram um único DBMS. Todo o acesso ao banco de dados foi feito por meio do front-end desse sistema ou por meio de aplicativos escritos para funcionar exclusivamente com esse sistema. No entanto, como o uso de computadores cresceu e mais hardware e software de computador foram disponibilizados, as empresas começaram a adquirir DBMSs diferentes. Os motivos foram muitos: as pessoas compraram o que era mais barato, o que era mais rápido, o que eles já sabiam, o que era mais recente no mercado, o que funcionou melhor para um único aplicativo. Outros motivos eram reorganizações e fusões, em que os departamentos que anteriormente tinham um único DBMS agora tinham vários.  
  
 O problema cresceu ainda mais complexo com o advento dos computadores pessoais. Esses computadores trouxeram uma série de ferramentas para consultar, analisar e exibir dados, juntamente com uma série de bancos de dado acessíveis e fáceis de usar. A partir de então, uma única corporação geralmente tinha dados espalhados por uma infinidade de áreas de trabalho, servidores e minicomputers, armazenados em uma variedade de bancos de dados incompatíveis e acessados por um grande número de ferramentas diferentes, alguns dos quais poderiam obter todos eles.  
  
 O desafio final veio com o advento da computação cliente/servidor, que busca fazer o uso mais eficiente dos recursos do computador. Os computadores pessoais de baixo custo (os clientes) ficam na área de trabalho e fornecem um front-end gráfico para os dados e uma série de ferramentas baratas, como planilhas, programas de gráficos e construtores de relatórios. Os computadores minicomputers e mainframe (os servidores) hospedam os DBMS, onde podem usar seus recursos de computação e local central para fornecer acesso rápido e coordenado aos dados. Qual é o software front-end a ser conectado aos bancos de dados back-end?  
  
 Um problema semelhante enfrenta fornecedores independentes de software (ISVs). Os fornecedores que escrevem software de banco de dados para minicomputers e mainframes normalmente eram forçados a escrever uma versão de um aplicativo para cada DBMS ou gravar código específico de DBMS para cada DBMS que quisessem acessar. Os fornecedores que escrevem software para computadores pessoais tinham que gravar rotinas de acesso a dados para cada DBMS diferente com o qual desejavam trabalhar. Isso geralmente significava que uma grande quantidade de recursos foi gasto escrevendo e mantendo rotinas de acesso a dados em vez de aplicativos, e os aplicativos geralmente eram vendidos sem a sua qualidade, mas se podiam acessar dados em um determinado DBMS.  
  
 Os dois conjuntos de desenvolvedores necessários eram uma maneira de acessar dados em DBMSs diferentes. O grupo de mainframe e Minicomputer precisava de uma maneira de mesclar dados de DBMSs diferentes em um único aplicativo, enquanto o grupo de computadores pessoais precisava dessa capacidade, bem como uma maneira de escrever um único aplicativo que era independente de um DBMS. Em suma, os dois grupos precisavam de uma maneira interoperável para acessar dados; Eles precisavam de conectividade aberta de banco de dados.
