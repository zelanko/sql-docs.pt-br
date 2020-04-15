---
title: Drivers baseados em arquivos | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 223bd838754f1d656ac71ae37926389097af3ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306659"
---
# <a name="file-based-drivers"></a>Drivers baseados em arquivo
Drivers baseados em arquivos são usados com fontes de dados, como o dBASE, que não fornecem um mecanismo de banco de dados autônomo para o motorista usar. Esses drivers acessam os dados físicos diretamente e devem implementar um mecanismo de banco de dados para processar instruções SQL. Como prática padrão, os mecanismos de banco de dados em drivers baseados em arquivos implementam o subconjunto do ODBC SQL definido pelo nível mínimo de conformidade SQL; para obter uma lista das instruções SQL neste nível de conformidade, consulte [Apêndice C: Gramática SQL](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Ao comparar drivers baseados em arquivos e DBMS, drivers baseados em arquivos são mais difíceis de gravar por causa do componente do mecanismo de banco de dados, menos complicado de configurar porque não há peças de rede e menos poderosos porque poucas pessoas têm tempo para escrever mecanismos de banco de dados tão poderosos quanto os produzidos por empresas de banco de dados.  
  
 A ilustração a seguir mostra duas configurações diferentes de drivers baseados em arquivos, uma em que os dados residem localmente e a outra em que reside em um servidor de arquivos de rede.  
  
 ![Duas configurações de drivers baseados em&#45;de arquivos](../../odbc/reference/media/pr06.gif "pr06")
