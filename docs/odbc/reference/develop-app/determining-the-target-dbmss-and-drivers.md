---
title: Determinando os DBMSs de destino e os Drivers | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6be642b6c64da8193ba97de9df8b21ecb9e5a27c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinando os DBMSs de destino e os Drivers
A próxima questão a considerar é, o que são o alvo DBMSs para o aplicativo e quais drivers estão disponíveis que dão suporte a esses DBMSs? Como aplicativos genéricos tendem a ser altamente interoperável, a questão de destino DBMSs é mais aplicável para aplicativos personalizados e verticais. No entanto, a questão de drivers de destino se aplica a todos os aplicativos, como drivers variam amplamente velocidade, qualidade, suporte a recursos e disponibilidade. Além disso, se os drivers devem ser redistribuídos com o aplicativo, o custo e a disponibilidade dos planos de licenciamento precisam ser considerado.  
  
 Para muitos aplicativos personalizados, o destino DBMSs é óbvio: existentes DBMSs que o aplicativo foi projetado para acessar. Também devem ser consideradas DBMSs ao qual a migração futura está planejada. No entanto, a pergunta principal para esses aplicativos é qual driver ou drivers a serem usados com eles. Para outros aplicativos personalizados — aqueles que não são projetados para acessar um DBMS existente — o destino DBMSs pode ser escolhido com base no suporte ao recurso, suporte a usuários simultâneos, disponibilidade do driver e acessíveis.  
  
 Para aplicativos verticais, o destino que DBMSs normalmente são escolhidos com base no mercado, disponibilidade do driver e suporte ao recurso. Por exemplo, um aplicativo vertical projetado para pequenas empresas deve ter como destino os que são acessíveis para essas empresas; um aplicativo vertical projetado como um complemento para DBMSs existentes deve ter como destino amplamente usado DBMSs.  
  
 Ao escolher DBMSs de destino, as diferenças entre bancos de dados de área de trabalho e servidor devem ser consideradas. Bancos de dados de área de trabalho, como dBASE, Paradox e Btrieve são menos eficientes do que bancos de dados do servidor. Porque elas geralmente são acessadas por meio de mecanismos SQL menos avançados nos drivers mais baseada em arquivo, eles geralmente não têm suporte de transação completa, dar suporte a menos de usuários simultâneos e limitaram SQL. No entanto, eles são mais baratos e tem uma grande base instalada.  
  
 Bancos de dados do servidor, como Oracle, DB2 e do SQL Server fornecem suporte de transação completa, o suportam a muitos usuários simultâneos e tem SQL Avançado. Eles são muito mais caros e tem uma base instalada menor. Por outro lado, os preços de software tendem a ser mais alto, um pouco a compensação de um mercado potencial menor.  
  
 Assim, destino DBMSs às vezes pode ser escolhido com base nos recursos necessários pelo aplicativo e o mercado-alvo do aplicativo. Por exemplo, um sistema de entrada de ordem de grandes empresas pode não ter como destino bancos de dados de área de trabalho porque eles não têm suporte de transação adequado. Um sistema semelhante desenvolvido para pequenas empresas pode excluir a maioria dos bancos de dados do servidor com base em custo. E os desenvolvedores de aplicativos genéricos podem direcionar ambos mas evite usar os recursos avançados encontrados em bancos de dados do servidor.

