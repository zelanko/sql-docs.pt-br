---
title: Drivers baseados em arquivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 803da51c8507faa47f92b295d3749f00317bc413
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915381"
---
# <a name="file-based-drivers"></a>Drivers baseados em arquivo
Drivers baseados em arquivo são usadas com fontes de dados como dBASE que não fornecem um mecanismo de banco de dados autônomo para o driver a ser usado. Esses drivers acessam os dados físicos diretamente e devem implementar um mecanismo de banco de dados para as instruções SQL de processo. Como uma prática padrão, os mecanismos de banco de dados nos drivers baseados em arquivo implementam o subconjunto de ODBC SQL definido pelo nível de conformidade SQL mínimo; Para obter uma lista das instruções SQL nesse nível de compatibilidade, consulte [apêndice c: Gramática SQL](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Nos drivers baseados em DBMS e arquivo de comparação, drivers baseados em arquivo são menos avançados e mais difícil de escrever por causa do componente de mecanismo de banco de dados, menos complicado configurar porque não há nenhum partes da rede, porque algumas pessoas tenham o tempo de gravação de banco de dados mecanismos de tão poderosos quanto aqueles gerados por empresas de banco de dados.  
  
 A ilustração a seguir mostra duas configurações diferentes de drivers baseados em arquivo, uma na qual os dados residirem localmente e o outro no qual ele reside em um servidor de arquivos de rede.  
  
 ![Duas configurações do arquivo&#45;com base em drivers](../../odbc/reference/media/pr06.gif "pr06")
