---
description: Determinar os drivers e DBMSs de destino
title: Determinando os DBMSs e os drivers de destino | Microsoft Docs
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
ms.openlocfilehash: 8dfbc11e96577e9027d1cc6e17701a82b89061be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429318"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinar os drivers e DBMSs de destino
A próxima pergunta a ser considerada é, quais são os DBMS de destino do aplicativo e quais drivers estão disponíveis para dar suporte a esses DBMSs? Como os aplicativos genéricos tendem a ser altamente interoperáveis, a questão dos DBMS de destino é mais aplicável a aplicativos personalizados e verticais. No entanto, a questão dos drivers de destino se aplica a todos os aplicativos, pois os drivers variam muito em velocidade, qualidade, suporte a recursos e disponibilidade. Além disso, se os drivers forem redistribuídos com o aplicativo, o custo e a disponibilidade dos planos de licenciamento precisarão ser considerados.  
  
 Para muitos aplicativos personalizados, os DBMS de destino são óbvios: eles são DBMSs existentes que o aplicativo foi projetado para acessar. Os DBMSs para os quais a migração futura está planejada também devem ser considerados. No entanto, a principal pergunta para esses aplicativos é qual driver ou drivers usar com eles. Para outros aplicativos personalizados – aqueles que não foram projetados para acessar um DBMS existente-os DBMS de destino podem ser escolhidos com base no suporte a recursos, suporte simultâneo a usuários, disponibilidade de driver e acessível.  
  
 Para aplicativos verticais, os DBMS de destino geralmente são escolhidos com base no suporte a recursos, na disponibilidade do driver e no mercado. Por exemplo, um aplicativo vertical projetado para pequenas empresas deve ter como alvo DBMSs que são acessíveis para essas empresas; um aplicativo vertical projetado como um complemento a DBMSs existentes deve visar DBMSs amplamente usados.  
  
 Ao escolher DBMSs de destino, as diferenças entre bancos de dados de desktop e servidor devem ser consideradas. Bancos de dados de desktop como dBASE, Paradox e Btrieve são menos eficientes do que bancos de dados de servidor. Como eles são geralmente acessados por meio de mecanismos SQL menos poderosos encontrados na maioria dos drivers baseados em arquivo, eles geralmente não têm suporte total a transações, dão suporte a menos usuários simultâneos e têm SQL limitado. No entanto, eles são baratos e têm uma grande base instalada.  
  
 Bancos de dados de servidor como Oracle, DB2 e SQL Server fornecem suporte completo a transações, dão suporte a muitos usuários simultâneos e têm SQL avançado. Eles são muito mais caros e têm uma base instalada menor. Por outro lado, os preços de software tendem a ser maiores, o que é um pequeno mercado potencial.  
  
 Assim, os DBMS de destino às vezes podem ser escolhidos com base nos recursos exigidos pelo aplicativo e pelo mercado de destino do aplicativo. Por exemplo, um sistema de entrada de pedidos para grandes corporações pode não ter como destino bancos de dados de desktop porque eles não têm suporte adequado à transação. Um sistema semelhante projetado para pequenas empresas pode excluir a maioria dos bancos de dados de servidor com base no custo. E os desenvolvedores de aplicativos genéricos podem ter como destino ambos, mas evite usar os recursos avançados encontrados em bancos de dados de servidor.
