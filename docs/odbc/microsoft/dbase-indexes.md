---
title: DBASE Indexes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9300a38a0e36da771a238f73b77d3dda527334ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307667"
---
# <a name="dbase-indexes"></a>Índices do dBASE
O driver oDBC dBASE abre e atualiza automaticamente os arquivos de índice dBASE IV. Você deve usar a caixa de diálogo **Select Indexes** exibida através do Administrador de Origem de Dados oDBC para associar arquivos dBASE III .ndx com arquivos dBASE.  
  
 As seguintes limitações se aplicam à criação de índices dBASE:  
  
-   Todos os nomes das colunas devem ser válidos.  
  
-   Todas as colunas devem estar na mesma ordem ascendente ou descendente.  
  
-   O comprimento de qualquer coluna de texto deve ser inferior a 100 bytes.  
  
-   Se existir mais de uma coluna, todas as colunas devem ser colunas de texto e a soma dos tamanhos das colunas deve ser inferior a 100 bytes.  
  
-   Os campos de memorando não podem ser indexados.  
  
-   Um índice não deve ser especificado para o conjunto atual de campos (ou seja, índices duplicados não são permitidos).  
  
-   O nome do índice deve corresponder à convenção de nomeação do índice dBASE. dBASE III requer que cada índice esteja em um arquivo separado, cada um com uma extensão .ndx. No dBASE IV, os índices são criados como nomes de marca que são armazenados em um único arquivo .mdx. O arquivo .mdx tem o mesmo nome base do arquivo de banco de dados (por exemplo, Emp.mdx é o arquivo de índice para o banco de dados Emp.dbf).  
  
-   o dBASE define um índice único como aquele em que apenas um registro de um conjunto com valores-chave idênticos é adicionado ao índice.
