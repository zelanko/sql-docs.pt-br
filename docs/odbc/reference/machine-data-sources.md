---
title: Fontes de dados da máquina | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- machine data sources [ODBC]
- data sources [ODBC], machine
ms.assetid: 371bb5b5-1258-4657-acb5-d2b688b2ab4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8b0dca3a9d850cca3eb514ff65e8cb83971340c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295557"
---
# <a name="machine-data-sources"></a>Fontes de dados do computador
*As fontes de dados* da máquina são armazenadas no sistema com um nome definido pelo usuário. Associado ao nome de origem dos dados está todas as informações que o Driver Manager e o driver precisam para se conectar à fonte de dados. Para uma fonte de dados Xbase, este pode ser o nome do driver Xbase, o caminho completo do diretório contendo os arquivos Xbase e algumas opções que dizem ao driver como usar esses arquivos, como modo de usuário único ou somente leitura. Para uma fonte de dados Oracle, este pode ser o nome do driver Oracle, o servidor onde o Oracle DBMS reside, a seqüência de conexão SQL*Net que identifica o driver SQL\*Net a ser usado e o ID do sistema do banco de dados no servidor.
