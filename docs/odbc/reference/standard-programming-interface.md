---
title: Interface de programação padrão | Microsoft Docs
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
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c91448833c6dacecaadfa4b0c11892e1a0c5e439
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="standard-programming-interface"></a>Interface de programação padrão
A interface de programação talvez é o candidato mais óbvio de padronização. Na verdade, quando estava sendo desenvolvido ODBC, ANSI e ISO já fornecido padrões para embedded SQL e SQL módulos. Embora nenhum padrões existiam para um banco de dados CLI, o grupo de acesso do SQL — um consórcio do setor de fornecedores de banco de dados — foi considerar a possibilidade de criar um; partes do ODBC posteriormente tornou-se a base para seu trabalho.  
  
 Um dos requisitos para o ODBC foi que um único aplicativo binário tinha que trabalhar com várias DBMSs. É por esse motivo que o ODBC não usar idiomas SQL ou módulo incorporados. Embora a linguagem em idiomas SQL e o módulo inseridos é padronizada, cada um é vinculada ao precompilers específicas do DBMS. Portanto, aplicativos devem ser recompilados para cada DBMS e os binários resultantes funcionam apenas com um único DBMS. Embora isto seja aceitável para os aplicativos de baixo volume encontrados nos mundos minicomputador e mainframe, ele é inaceitável do mundo de computador pessoal. Primeiro, ele é um pesadelo logístico para fornecer várias versões de software de alto volume, têm embalagem aos clientes; em segundo lugar, os aplicativos de computador pessoal geralmente precisam acessar vários DBMSs simultaneamente.  
  
 Por outro lado, uma interface de nível de chamada pode ser implementada por meio de bibliotecas ou drivers de banco de dados, que residem em cada computador local; um driver diferente é necessário para cada DBMS. Como os sistemas operacionais modernos pode carregar essas bibliotecas (assim como bibliotecas de vínculo dinâmico no sistema operacional Microsoft® Windows®) em tempo de execução, um único aplicativo pode acessar dados de diferentes DBMSs sem recompilação e também pode acessar dados de vários bancos de dados simultaneamente. Conforme novos drivers de banco de dados se tornam disponíveis, os usuários apenas podem instale-os em seus computadores sem a necessidade de modificar, recompile ou vincular novamente seus aplicativos de banco de dados. Além disso, uma interface de nível de chamada foi um bom candidato para ODBC porque Windows — a plataforma para a qual o ODBC foi originalmente desenvolvido — já feitas uso extensivo de tais bibliotecas.
