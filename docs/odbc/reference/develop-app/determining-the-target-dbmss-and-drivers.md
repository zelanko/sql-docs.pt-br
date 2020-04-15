---
title: Determinando os DBMSs e Drivers alvo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8811e4d289a8fc89c2c3773aab973df523025f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305867"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinar os drivers e DBMSs de destino
A próxima pergunta a considerar é: quais são os DBMSs de destino e quais drivers estão disponíveis que suportam esses DBMSs? Como as aplicações genéricas tendem a ser altamente interoperáveis, a questão do DBMSs de destino é mais aplicável a aplicações personalizadas e verticais. No entanto, a questão dos drivers-alvo se aplica a todos os aplicativos, pois os drivers variam amplamente em velocidade, qualidade, suporte de recursos e disponibilidade. Além disso, se os motoristas forem redistribuídos com o aplicativo, o custo e a disponibilidade dos planos de licenciamento precisam ser considerados.  
  
 Para muitos aplicativos personalizados, os DBMSs de destino são óbvios: são DBMSs existentes que o aplicativo foi projetado para acessar. Também devem ser consideradas DBMSs para as quais a migração futura está prevista. No entanto, a grande questão para esses aplicativos é qual motorista ou motorista usar com eles. Para outros aplicativos personalizados - aqueles que não foram projetados para acessar um DBMS existente - os DBMSs de destino podem ser escolhidos com base no suporte a recursos, suporte ao usuário simultâneo, disponibilidade do driver e acessibilidade.  
  
 Para aplicações verticais, os DBMSs de destino geralmente são escolhidos com base no suporte a recursos, disponibilidade de driver e mercado. Por exemplo, um aplicativo vertical projetado para pequenas empresas deve ter como alvo DBMSs que sejam acessíveis a essas empresas; uma aplicação vertical projetada como um complemento aos DBMSs existentes deve ter como alvo DBMSs amplamente utilizados.  
  
 Ao escolher DBMSs de destino, as diferenças entre bancos de dados de desktop e servidor devem ser consideradas. Bancos de dados de desktop como dBASE, Paradox e Btrieve são menos poderosos que os bancos de dados de servidores. Como eles geralmente são acessados através dos mecanismos SQL menos poderosos encontrados na maioria dos drivers baseados em arquivos, eles geralmente não têm suporte total à transação, suportam menos usuários simultâneos e têm SQL limitado. No entanto, eles são baratos e têm uma grande base instalada.  
  
 Bancos de dados de servidores como Oracle, DB2 e SQL Server fornecem suporte total a transações, suportam muitos usuários simultâneos e têm SQL rico. Eles são muito mais caros e têm uma base instalada menor. Por outro lado, os preços dos softwares tendem a ser mais altos, compensando um pouco um mercado potencial menor.  
  
 Assim, os DBMSs de destino às vezes podem ser escolhidos com base nos recursos exigidos pelo aplicativo e no mercado-alvo do aplicativo. Por exemplo, um sistema de entrada de pedidos para grandes corporações pode não ter como alvo bancos de dados de desktop porque eles não têm suporte adequado para transações. Um sistema semelhante projetado para pequenas empresas pode excluir a maioria dos bancos de dados de servidores com base no custo. E os desenvolvedores de aplicativos genéricos podem ter como alvo ambos, mas evitam usar os recursos avançados encontrados nos bancos de dados dos servidores.
