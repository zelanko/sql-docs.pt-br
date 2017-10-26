---
title: Usando fontes de dados | Microsoft Docs
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
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb3e6adb6f563e49429c2e04239ce3170d96b9a4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-data-sources"></a>Usando fontes de dados
Fontes de dados geralmente são criadas pelo usuário final ou um técnico com um programa chamado o *administrador ODBC*. O administrador ODBC solicita ao usuário para o driver para usar e, em seguida, chama esse driver. O driver exibe uma caixa de diálogo que solicita as informações necessárias para se conectar à fonte de dados. Depois que o usuário insere as informações, o driver armazena no sistema.  
  
 Posteriormente, o aplicativo chama o Gerenciador de Driver e passa o nome de uma fonte de dados do computador ou o caminho de um arquivo que contém uma fonte de dados de arquivo. Quando é passada a um nome de fonte de dados de máquina, o Gerenciador de Driver procura pelo sistema para localizar o driver usado pela fonte de dados. Em seguida, ele carrega o driver e passa o nome da fonte de dados a ele. O driver usa o nome da fonte de dados para localizar as informações necessárias para se conectar à fonte de dados. Finalmente, ele se conecta à fonte de dados, normalmente avisar o usuário para uma ID de usuário e senha, que geralmente não são armazenadas.  
  
 Quando passado a uma fonte de dados de arquivo, o Gerenciador de Driver abre o arquivo e carrega o driver especificado. Se o arquivo também contém uma cadeia de caracteres de conexão, ele passa a isso para o driver. Usando as informações na cadeia de conexão, o driver conecta-se à fonte de dados. Se nenhuma cadeia de caracteres de conexão foi passada, o driver geralmente solicita ao usuário as informações necessárias.

