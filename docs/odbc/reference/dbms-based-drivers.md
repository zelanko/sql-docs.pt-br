---
title: Drivers baseados em DBMS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e7b7b153d0b0cb0a3e6a3d738908b0039b95679
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306482"
---
# <a name="dbms-based-drivers"></a>Drivers baseados em DBMS
Os drivers baseados em DBMS são usados com fontes de dados, como Oracle ou SQL Server, que fornecem um mecanismo de banco de dados autônomo para o motorista usar. Esses drivers acessam os dados físicos através do motor autônomo; ou seja, eles enviam instruções SQL para e recuperam resultados do motor.  
  
 Como os drivers baseados em DBMS usam um mecanismo de banco de dados existente, eles geralmente são mais fáceis de escrever do que drivers baseados em arquivos. Embora um driver baseado em DBMS possa ser facilmente implementado traduzindo chamadas ODBC para chamadas de API nativas, isso resulta em um driver mais lento. Uma maneira melhor de implementar um driver baseado em DBMS é usar o protocolo de fluxo de dados subjacente, que geralmente é o que a API nativa faz. Por exemplo, um driver sql server deve usar TDS (o protocolo de fluxo de dados para SQL Server) em vez de BIBLIOTECA DB (a API nativa para SQL Server). Uma exceção a esta regra é quando o ODBC é a API nativa. Por exemplo, watcom SQL é um motor autônomo que reside na mesma máquina que o aplicativo e é carregado diretamente como o driver.  
  
 Os drivers baseados em DBMS atuam como cliente em uma configuração cliente/servidor onde a fonte de dados atua como servidor. Na maioria dos casos, o cliente (driver) e o servidor (fonte de dados) residem em máquinas diferentes, embora ambos possam residir na mesma máquina executando um sistema operacional multitarefa. Uma terceira possibilidade é um *gateway,* que fica entre o driver e a fonte de dados. Um gateway é um software que faz com que um DBMS se pareça com outro. Por exemplo, aplicativos escritos para usar o SQL Server também podem acessar dados DB2 através do Gateway DB2 do Micro Decisionware; este produto faz com que o DB2 se pareça com o SQL Server.  
  
 A ilustração a seguir mostra três configurações diferentes de drivers baseados em DBMS. Na primeira configuração, o driver e a fonte de dados residem na mesma máquina. No segundo, o driver e a fonte de dados residem em diferentes máquinas. No terceiro, o driver e a fonte de dados residem em diferentes máquinas e um gateway fica entre eles, residindo em outra máquina.  
  
 ![Três configurações para drivers baseados em&#45;DBMS](../../odbc/reference/media/pr07.gif "pr07")
