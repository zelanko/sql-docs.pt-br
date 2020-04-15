---
title: Interface de Programação Padrão | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7767f113d0f70569ce253f0200cd35cb83915a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279992"
---
# <a name="standard-programming-interface"></a>Interface de programação padrão
A interface de programação é talvez o candidato mais óbvio para a padronização. De fato, quando o ODBC estava sendo desenvolvido, a ANSI e a ISO já fornecipadrões para módulos SQL e SQL incorporados. Embora não existisse padrões para um CLI de banco de dados, o SQL Access Group - um consórcio do setor de fornecedores de banco de dados - estava considerando a possibilidade de criar um; partes da ODBC mais tarde se tornaram a base para seu trabalho.  
  
 Um dos requisitos para o ODBC era que um único binário de aplicação tivesse que trabalhar com vários DBMSs. É por essa razão que o ODBC não usa sql ou linguagens incorporadas. Embora a linguagem em sql incorporado e linguagens de módulo seja padronizada, cada uma está vinculada a precompiladores específicos do DBMS. Assim, os aplicativos devem ser recompilados para cada DBMS e os binários resultantes funcionam apenas com um único DBMS. Embora isso seja aceitável para os aplicativos de baixo volume encontrados nos mundos minicomputador e mainframe, é inaceitável no mundo dos computadores pessoais. Em primeiro lugar, é um pesadelo logístico entregar múltiplas versões de software de alto volume e encolhido aos clientes; segundo, aplicativos de computador pessoais muitas vezes precisam acessar vários DBMSs simultaneamente.  
  
 Por outro lado, uma interface de nível de chamada pode ser implementada através de bibliotecas, ou drivers de banco de dados, que residem em cada máquina local; um driver diferente é necessário para cada DBMS. Como os sistemas operacionais modernos podem carregar tais bibliotecas (como bibliotecas de links dinâmicos no sistema operacional Microsoft® Windows®) em tempo de execução, um único aplicativo pode acessar dados de diferentes DBMSs sem recompilação e também pode acessar dados de vários bancos de dados simultaneamente. À medida que novos drivers de banco de dados se tornam disponíveis, os usuários podem simplesmente instalá-los em seus computadores sem ter que modificar, recompilar ou revincular seus aplicativos de banco de dados. Além disso, uma interface de nível de chamada era um bom candidato para o ODBC porque o Windows - a plataforma para a qual o ODBC foi originalmente desenvolvido - já fazia uso extensivo dessas bibliotecas.
