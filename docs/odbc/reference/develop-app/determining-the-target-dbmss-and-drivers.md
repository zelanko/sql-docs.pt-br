---
title: Determinando os Drivers e DBMSs de destino | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7065aa88d60a508df9946d38d0dded220c4bb7a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106140"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinar os drivers e DBMSs de destino
A próxima questão a considerar é, quais são o DBMSs de destino para o aplicativo e quais drivers estão disponíveis que dão suporte a esses DBMSs? Como aplicativos genéricos tendem a ser altamente interoperável, a pergunta do DBMSs de destino é mais aplicável a aplicativos personalizados e verticais. No entanto, a questão dos drivers de destino se aplica a todos os aplicativos, porque os drivers variam enormemente em velocidade, qualidade, suporte ao recurso e disponibilidade. Além disso, se os drivers devem ser redistribuídos com o aplicativo, o custo e a disponibilidade dos planos de licenciamento precisam ser considerados.  
  
 Para muitos aplicativos personalizados, o destino DBMSs são óbvias: Eles são existentes DBMSs que o aplicativo foi projetado para acessar. Também devem ser considerados DBMSs ao qual a migração futura está planejada. No entanto, a questão principal para esses aplicativos é qual driver ou drivers a serem usados com elas. Para outros aplicativos personalizados – aquelas que não são projetados para acessar um DBMS existente - o DBMSs de destino pode ser escolhido com base no suporte ao recurso, suporte a usuários simultâneos, a disponibilidade de drivers e acessibilidade.  
  
 Para aplicativos verticais, o destino que DBMSs normalmente são escolhidos com base no mercado, a disponibilidade de drivers e suporte ao recurso. Por exemplo, um aplicativo vertical projetado para pequenas empresas deve ter como destino DBMSs são acessíveis a essas empresas; um aplicativo vertical projetado como um complemento para DBMSs existentes deve ter como destino amplamente usado DBMSs.  
  
 Ao escolher DBMSs de destino, as diferenças entre os bancos de dados da área de trabalho e servidor devem ser consideradas. Bancos de dados da área de trabalho, como, Paradox, dBASE e Btrieve são menos avançados que bancos de dados do servidor. Porque eles são geralmente acessados por meio de mecanismos de SQL menos potentes encontrados nos drivers mais baseados em arquivo, eles geralmente não têm suporte de transação completa, suportam o menor número de usuários simultâneo e limitaram SQL. No entanto, eles são baratos e tem uma grande base instalada.  
  
 Bancos de dados do servidor, como Oracle, DB2 e do SQL Server dão suporte a transações completo, dar suporte a muitos usuários simultâneos e tem o SQL avançada. Eles são muito mais caros e têm uma base instalada menor. Por outro lado, os preços de software tendem a ser mais alto, um pouco o deslocamento de um mercado potencial menor.  
  
 Assim, destino DBMSs, às vezes, pode ser escolhido com base nos recursos necessários pelo aplicativo e o mercado-alvo do aplicativo. Por exemplo, um sistema de entrada de pedidos para grandes corporações não pode direcionar bancos de dados da área de trabalho porque eles não têm suporte de transação adequado. Um sistema similar projetado para pequenas empresas pode excluir a maioria dos bancos de dados do servidor com base em custo. E os desenvolvedores de aplicativos genéricos podem direcionar a ambos, mas evite usar os recursos avançados encontrados em bancos de dados do servidor.
