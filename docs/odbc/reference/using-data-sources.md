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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df9b09e4c5519e0fff44902bd83b8e3d92a67ca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286536"
---
# <a name="using-data-sources"></a>Usar fontes de dados
As fontes de dados geralmente são criadas pelo usuário final ou por um técnico com um programa chamado *Administrador ODBC*. O administrador do ODBC solicita ao usuário que o driver use e, em seguida, chama o driver. O driver exibe uma caixa de diálogo que solicita as informações de que precisa para se conectar à fonte de dados. Depois que o usuário insere as informações, o motorista armazena-as no sistema.  
  
 Mais tarde, o aplicativo liga para o Gerenciador de driver e passa-o o nome de uma fonte de dados de máquina ou o caminho de um arquivo contendo uma fonte de dados de arquivo. Quando passa um nome de origem de dados da máquina, o Driver Manager pesquisa o sistema para encontrar o driver usado pela fonte de dados. Em seguida, ele carrega o driver e passa o nome da fonte de dados para ele. O driver usa o nome de origem dos dados para encontrar as informações que precisa para se conectar à fonte de dados. Finalmente, ele se conecta à fonte de dados, normalmente solicitando ao usuário um ID de usuário e senha, que geralmente não são armazenados.  
  
 Quando passa uma fonte de dados de arquivo, o Gerenciador de driver abre o arquivo e carrega o driver especificado. Se o arquivo também contiver uma seqüência de conexão, ele passa isso para o driver. Usando as informações na seqüência de conexão, o driver se conecta à fonte de dados. Se nenhuma seqüência de conexão foi aprovada, o driver geralmente solicita ao usuário as informações necessárias.
