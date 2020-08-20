---
description: Visão geral do objeto Command
title: Visão geral do objeto de comando | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
author: rothja
ms.author: jroth
ms.openlocfilehash: d44c727a69dc74bf243bc2f2c0204cb41cd9f585
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453678"
---
# <a name="command-object-overview"></a>Visão geral do objeto Command
Com um objeto de **comando** , você pode fazer o seguinte:  
  
-   Defina o texto executável do comando (por exemplo, uma instrução SQL ou um procedimento armazenado) usando a propriedade **CommandText** .  
  
-   Defina consultas parametrizadas ou argumentos de procedimento armazenado usando objetos de **parâmetro** e a coleção de **parâmetros** .  
  
-   Execute um comando e retorne um objeto **Recordset** , se apropriado, usando o método **Execute** .  
  
-   Especifique o tipo de comando usando a propriedade **CommandType** antes da execução para otimizar o desempenho.  
  
-   Especifique informações específicas sobre o texto do comando usando a propriedade **dialeto** do objeto **Command** .  
  
-   Controle se o provedor salva uma versão preparada (ou compilada) do comando antes da execução usando a propriedade **preparada** .  
  
-   Defina o número de segundos que um provedor aguardará até que um comando seja executado usando a propriedade **CommandTimeout** .  
  
-   Associe uma conexão aberta a um objeto de **comando** definindo sua propriedade **ActiveConnection** .  
  
-   Defina a propriedade **Name** para identificar o objeto de **comando** como um método no objeto de **conexão** associado.  
  
-   Passe um objeto de **comando** para a propriedade **Source** de um **conjunto de registros** a fim de obter dados.  
  
-   Passe um objeto **Stream** contendo um comando (por exemplo, um comando XML) para um provedor que ofereça suporte a ele.
