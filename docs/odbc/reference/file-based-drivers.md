---
title: Drivers baseados em arquivo | Microsoft Docs
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
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ab8cb4066a8c5c7ab2e31401dd1e80d003d5b38
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="file-based-drivers"></a>Drivers baseados em arquivo
Drivers baseados em arquivo são usadas com fontes de dados como dBASE que não fornecem um mecanismo de banco de dados independente para usar o driver. Esses drivers acessam os dados físicos diretamente e devem implementar um mecanismo de banco de dados para instruções SQL de processo. Como prática padrão, os mecanismos de banco de dados de drivers baseados em arquivo implementam o subconjunto de ODBC SQL definido pelo nível de conformidade SQL mínimo; Para obter uma lista das instruções SQL neste nível de conformidade, consulte [gramática de SQL do apêndice c:](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Em drivers baseados em DBMS e arquivo de comparação, drivers baseados em arquivo são menos avançados e mais difícil de escrever devido o componente do mecanismo de banco de dados, menos complicado configurar porque não há nenhum partes da rede, pois poucas pessoas têm tempo para gravar no banco de dados mecanismos tão poderoso quanto os que foram produzidos por empresas de banco de dados.  
  
 A ilustração a seguir mostra duas configurações diferentes de drivers baseados em arquivo, um no qual os dados residem localmente e o outro no qual ele reside em um servidor de arquivos de rede.  
  
 ![Duas configurações de arquivo &#45; drivers com base](../../odbc/reference/media/pr06.gif "pr06")
