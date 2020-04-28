---
title: Índices do dBASE | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307667"
---
# <a name="dbase-indexes"></a>Índices do dBASE
O driver do dBASE do ODBC abre e atualiza automaticamente os arquivos de índice do dBASE IV. Você deve usar a caixa de diálogo **selecionar índices** exibida por meio do administrador de fonte de dados ODBC para associar arquivos. ndx do dBASE III a arquivos do dBASE.  
  
 As seguintes limitações se aplicam à criação de índices do dBASE:  
  
-   Todos os nomes de coluna devem ser válidos.  
  
-   Todas as colunas devem estar na mesma ordem crescente ou decrescente.  
  
-   O comprimento de qualquer coluna de texto individual deve ser menor que 100 bytes.  
  
-   Se houver mais de uma coluna, todas as colunas deverão ser colunas de texto e a soma dos tamanhos das colunas deverá ser menor que 100 bytes.  
  
-   Os campos de memorando não podem ser indexados.  
  
-   Um índice não deve ser especificado para o conjunto atual de campos (ou seja, índices duplicados não são permitidos).  
  
-   O nome do índice deve corresponder à Convenção de nomenclatura do índice do dBASE. o dBASE III requer que cada índice esteja em um arquivo separado, cada um com uma extensão. ndx. No dBASE IV, os índices são criados como nomes de marca que são armazenados em um único arquivo. MDX. O arquivo. MDX tem o mesmo nome base do arquivo de banco de dados (por exemplo, EMP. MDX é o arquivo de índice para o banco de dados EMP. dbf).  
  
-   o dBASE define um índice exclusivo como um em que apenas um registro de um conjunto com valores de chave idênticos é adicionado ao índice.
