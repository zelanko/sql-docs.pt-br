---
title: Por que o ODBC foi criado? | Microsoft Docs
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
helpviewer_keywords: ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 33cc5f63c34618f51196e173e58adbac58377f29
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="why-was-odbc-created"></a>Por que o ODBC foi criado?
Historicamente, empresas usaram um DBMS único. Todo o acesso de banco de dados foi feito por meio de front-end de sistema ou aplicativos escritos para funcionar exclusivamente com este sistema. No entanto, como o uso de computadores cresceu e mais hardware e software tornou-se disponível, as empresas iniciado para adquirir DBMSs diferentes. Os motivos foram muitas: pessoas compradas o que era mais barato, o que mais rápido, o que eles já soubessem, o que foi mais recente no mercado, o que funcionou melhor para um único aplicativo. Outros motivos foram reorganizações e fusões, onde departamentos que anteriormente tinham um DBMS único agora tinham vários.  
  
 O problema cresceu ainda mais complexo com o advento dos computadores pessoais. Esses computadores colocados em um host de ferramentas para consultar, analisar e exibir dados, juntamente com um número de bancos de dados de baixo custo, fácil de usar. Daí em seguida diante, uma empresa geralmente tinha dados espalhados por uma infinidade de desktops, servidores e minicomputadores, armazenados em uma variedade de bancos de dados incompatíveis e acessados por um grande número de ferramentas diferentes, alguns dos quais foi possível obter todos os dados.  
  
 O desafio final fornecida com o surgimento de computação, de cliente/servidor que tenta fazer o uso mais eficiente dos recursos do computador. PCs baixo custo (clientes) ficam na área de trabalho e fornecer ambos os gráfico front-end para os dados e um número de ferramentas de baixo custo, como planilhas, gráficos de programas e construtores de relatórios. Minicomputadores e mainframes (os servidores) hospedam DBMSs, onde eles podem usar sua capacidade de computação e o local central para fornecer acesso a dados rápida e coordenada. Então, como foi o software de front-end a ser conectado aos bancos de dados back-end?  
  
 Um problema semelhante que fornecedores de software independentes (ISVs). Geralmente, fornecedores de software de banco de dados para minicomputadores e mainframes de gravação foram forçados a escrever uma versão de um aplicativo para cada DBMS ou escrever código específico do DBMS para cada DBMS que desejem acessar. Fornecedores de software para computadores pessoais de gravação precisavam criar rotinas de acesso a dados para cada DBMS diferente com o qual eles querem trabalhar. Geralmente, isso significa que uma grande quantidade de recursos foram gastos escrevendo e mantendo rotinas em vez de aplicativos de acesso a dados e aplicativos geralmente foram vendidos não a qualidade mas se eles podem acessar os dados em um determinado DBMS.  
  
 O que os dois conjuntos de desenvolvedores necessário foi uma maneira de acessar dados em diferentes DBMSs. O grupo de mainframe e minicomputador precisava de uma forma para mesclar dados de DBMSs diferentes em um único aplicativo, enquanto o grupo de computador pessoal necessário essa capacidade, bem como uma maneira de gravar um único aplicativo que foi independente de qualquer um DBMS. Em resumo, ambos os grupos necessários forma interoperável para acessar dados. eles necessária conectividade aberta de banco de dados.
