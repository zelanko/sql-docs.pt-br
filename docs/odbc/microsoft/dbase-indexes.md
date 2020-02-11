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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9a0a57c3dce920c6d5fbc2510932066cb5a2659
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096365"
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
