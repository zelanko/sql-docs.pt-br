---
title: "Visão geral do objeto de comando | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f1f01c7ca7a378faaaabf11099b97b0dfa0c7a2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="command-object-overview"></a>Visão geral do objeto de comando
Com um **comando** do objeto, você pode fazer o seguinte:  
  
-   Definir o texto do executável do comando (por exemplo, uma instrução SQL ou um procedimento armazenado) usando o **CommandText** propriedade.  
  
-   Definir consultas com parâmetros ou argumentos de procedimento armazenado usando **parâmetro** objetos e o **parâmetros** coleção.  
  
-   Executar um comando e retornar um **registros** do objeto, se apropriado, usando o **Execute** método.  
  
-   Especifique o tipo de comando usando o **CommandType** propriedade antes da execução para otimizar o desempenho.  
  
-   Especificar informações específicas sobre o texto de comando usando o **dialeto** propriedade o **comando** objeto.  
  
-   Controlar se o provedor salva uma versão preparada (ou compilada) do comando antes da execução usando o **preparado** propriedade.  
  
-   Definir o número de segundos que um provedor irá aguardar um comando seja executado usando o **CommandTimeout** propriedade.  
  
-   Associar uma conexão aberta com um **comando** objeto definindo seu **ActiveConnection** propriedade.  
  
-   Definir o **nome** propriedade para identificar o **comando** objeto como um método em associado **Conexão** objeto.  
  
-   Passar um **comando** o objeto para o **fonte** propriedade de um **Recordset** para obter dados.  
  
-   Passar um **fluxo** objeto que contém um comando (por exemplo, um comando XML) para um provedor que dá suporte a ele.
