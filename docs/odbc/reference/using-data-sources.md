---
title: Usando fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c898cb5cd8c9998d9126ec468a2b43587e2e279a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714114"
---
# <a name="using-data-sources"></a>Usar fontes de dados
Fontes de dados geralmente são criadas pelo usuário final ou um técnico com um programa de chamada a *administrador de ODBC*. O administrador de ODBC solicita ao usuário para o driver para usar e, em seguida, chama esse driver. O driver exibe uma caixa de diálogo que solicita as informações necessárias para se conectar à fonte de dados. Depois que o usuário insere as informações, o driver armazena no sistema.  
  
 Posteriormente, o aplicativo chama o Gerenciador de Driver e passa o nome de uma fonte de dados de máquina ou o caminho de um arquivo que contém uma fonte de dados de arquivo. Quando passado um nome de fonte de dados de máquina, o Gerenciador de Driver pesquisa pelo sistema para localizar o driver usado pela fonte de dados. Em seguida, ele carrega o driver e passa o nome da fonte de dados para ele. O driver usa o nome da fonte de dados para localizar as informações necessárias para se conectar à fonte de dados. Por fim, ele se conecta à fonte de dados, geralmente solicitando que o usuário para uma ID de usuário e uma senha, que geralmente não são armazenados.  
  
 Quando passado a uma fonte de dados de arquivo, o Gerenciador de Driver abre o arquivo e carrega o driver especificado. Se o arquivo também contém uma cadeia de caracteres de conexão, ele passa isso para o driver. Usando as informações na cadeia de conexão, o driver conecta-se à fonte de dados. Se nenhuma cadeia de conexão foi passada, o driver geralmente solicita ao usuário as informações necessárias.
