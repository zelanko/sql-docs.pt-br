---
title: Interface de programação padrão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a241ea92af6c1273039cc45daab232a1fbe763a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081844"
---
# <a name="standard-programming-interface"></a>Interface de programação padrão
A interface de programação é talvez o candidato mais óbvio para padronização. Na verdade, quando o ODBC estava sendo desenvolvido, o ANSI e o ISO já forneciam padrões para SQL e módulos SQL inseridos. Embora não existam padrões para uma CLI de banco de dados, o grupo de acesso do SQL – um consórcio do setor de fornecedores de banco de dados – estava considerando a possibilidade de criar um; partes do ODBC mais tarde se tornaram a base para seu trabalho.  
  
 Um dos requisitos do ODBC era que um único binário de aplicativo tinha que trabalhar com vários DBMSs. É por esse motivo que o ODBC não usa as linguagens SQL ou Module inseridas. Embora o idioma nas linguagens SQL e Module inseridas seja padronizado, cada um está vinculado a precompiladores específicos do DBMS. Portanto, os aplicativos devem ser recompilados para cada DBMS e os binários resultantes só funcionam com um único DBMS. Embora isso seja aceitável para os aplicativos de baixo volume encontrados nos mundos do Minicomputer e do mainframe, ele é inaceitável no mundo do computador pessoal. Primeiro, ele é um pesadelo logística para fornecer várias versões de software de alto volume, com encolhimento reduzido aos clientes; em segundo lugar, os aplicativos de computador pessoal geralmente precisam acessar vários DBMS simultaneamente.  
  
 Por outro lado, uma interface de nível de chamada pode ser implementada por meio de bibliotecas, ou drivers de banco de dados, que residem em cada computador local; um driver diferente é necessário para cada DBMS. Como os sistemas operacionais modernos podem carregar essas bibliotecas (como bibliotecas de vínculo dinâmico no sistema operacional Microsoft® Windows®) em tempo de execução, um único aplicativo pode acessar dados de DBMSs diferentes sem recompilação e também pode acessar dados de vários bancos de dados simultaneamente. À medida que novos drivers de banco de dados ficam disponíveis, os usuários podem apenas instalá-los em seus computadores sem precisar modificar, recompilar ou vincular novamente seus aplicativos de banco de dados. Além disso, uma interface de nível de chamada era um bom candidato ao ODBC, pois o Windows – a plataforma para a qual o ODBC foi originalmente desenvolvido – já fez uso extensivo dessas bibliotecas.
