---
title: "Índices do dBASE | Microsoft Docs"
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
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f2725f312691d3cb644f9a096b5f469f1356c55
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="dbase-indexes"></a>Índices do dBASE
O driver ODBC para dBASE automaticamente abre e atualiza os arquivos de índice do dBASE IV. Você deve usar o **Selecionar índices** caixa de diálogo exibida por meio de administrador de fonte de dados do ODBC para associar os arquivos. ndx dBASE III arquivos dBASE.  
  
 As seguintes limitações se aplicam à criação de índices do dBASE:  
  
-   Todos os nomes de coluna devem ser válidos.  
  
-   Todas as colunas devem ser no mesmo crescente ou decrescente.  
  
-   O comprimento de uma coluna de texto deve ser inferior a 100 bytes.  
  
-   Se houver mais de uma coluna, todas as colunas devem ser colunas de texto e a soma do tamanho das colunas deve ser inferior a 100 bytes.  
  
-   Campos de memorando não podem ser indexados.  
  
-   Um índice não deve ser especificado para o conjunto atual de campos (ou seja, os índices duplicados não são permitidos).  
  
-   O nome do índice deve corresponder a convenção de nomenclatura de índice do dBASE. dBASE III requer que cada índice esteja em um arquivo separado, cada um tendo uma extensão. ndx. No dBASE IV, os índices são criados como nomes de marca são armazenados em um arquivo. MDX único. O arquivo. MDX tem o mesmo nome base do arquivo de banco de dados (por exemplo, Emp. MDX é o arquivo de índice para o banco de dados Emp).  
  
-   dBASE define um índice exclusivo como um em que apenas um registro de um conjunto de valores de chave idênticos é adicionado ao índice.

