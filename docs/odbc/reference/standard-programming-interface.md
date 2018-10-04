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
manager: craigg
ms.openlocfilehash: b02b5a907fc134e04a4c78cda2448c128178585a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622554"
---
# <a name="standard-programming-interface"></a>Interface de programação padrão
A interface de programação é talvez o candidato mais óbvio para padronização. Na verdade, quando estava sendo desenvolvido ODBC, ANSI e ISO já fornecidos padrões para embedded SQL e SQL módulos. Embora nenhum padrões existiam para um banco de dados da CLI, SQL Access Group — um consórcio do setor de fornecedores de banco de dados — foi considerar a possibilidade de criar um; partes do ODBC posteriormente tornou-se a base para o seu trabalho.  
  
 Um dos requisitos para o ODBC foi que um único aplicativo binário precisava funcionar com vários DBMSs. É por esse motivo que o ODBC não usar idiomas SQL ou o módulo incorporados. Embora a linguagem em linguagens SQL e o módulo inseridas é padronizada, cada um está vinculada ao precompilers específicos de DBMS. Assim, aplicativos devem ser recompilados para cada DBMS e os binários resultantes só funcionam com um único DBMS. Embora isso seja aceitável para os aplicativos de baixo volume encontrados nos mundos minicomputador e de mainframe, é inaceitável no mundo do computador pessoal. Primeiro, é um pesadelo de logístico para fornecer várias versões de software de alto volume, a configuração inicial pelo usuário para os clientes; em segundo lugar, os aplicativos de computador pessoal geralmente precisam acessar vários DBMSs simultaneamente.  
  
 Por outro lado, uma interface de nível de chamada pode ser implementada por meio de bibliotecas ou drivers de banco de dados, que residem em cada computador local; um driver diferente é necessário para cada DBMS. Como os sistemas operacionais modernos pode carregar essas bibliotecas (como bibliotecas de vínculo dinâmico no sistema operacional Microsoft® Windows®) em tempo de execução, um único aplicativo pode acessar dados de diferentes DBMSs sem recompilação e também pode acessar dados de vários bancos de dados simultaneamente. Conforme novos drivers de banco de dados se tornam disponíveis, os usuários apenas podem instalá-los em seus computadores sem a necessidade de modificar, recompilar ou vincular novamente seus aplicativos de banco de dados. Além disso, uma interface de nível de chamada foi um bom candidato para ODBC, porque o Windows — a plataforma para a qual o ODBC foi originalmente desenvolvido — já faz uso extensivo dessas bibliotecas.
