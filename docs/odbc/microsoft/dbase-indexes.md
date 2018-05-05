---
title: Índices do dBASE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9db4a41b3f5821fab27c0f779fd4c7cf4d691022
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
