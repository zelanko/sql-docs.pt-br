---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 808c63575b93f9e4fa3b6459d2111637021218c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472715"
---
# <a name="command-object-overview"></a>Visão geral do objeto Command
Com uma **comando** do objeto, você pode fazer o seguinte:  
  
-   Define o texto executável do comando (por exemplo, uma instrução SQL ou um procedimento armazenado) usando o **CommandText** propriedade.  
  
-   Definir argumentos de procedimento armazenado ou consultas parametrizadas usando **parâmetro** objetos e o **parâmetros** coleção.  
  
-   Executar um comando e retornar um **conjunto de registros** do objeto, se apropriado, usando o **Execute** método.  
  
-   Especifique o tipo de comando usando o **CommandType** propriedade antes da execução para otimizar o desempenho.  
  
-   Especificar informações específicas sobre o texto de comando usando o **dialeto** propriedade da **comando** objeto.  
  
-   Controlar se o provedor salva uma versão preparada (ou compilada) do comando antes da execução, usando o **preparado** propriedade.  
  
-   Definir o número de segundos que um provedor irá aguardar por um comando seja executado usando o **CommandTimeout** propriedade.  
  
-   Associar uma conexão aberta com um **comando** objeto definindo suas **ActiveConnection** propriedade.  
  
-   Defina as **nome** propriedade para identificar o **comando** objeto como um método em associado **Conexão** objeto.  
  
-   Passar um **comando** do objeto para o **fonte** propriedade de um **conjunto de registros** para obter dados.  
  
-   Passar uma **Stream** objeto que contém um comando (por exemplo, um comando XML) para um provedor que dá suporte a ele.
