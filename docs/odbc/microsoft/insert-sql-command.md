---
title: INSERT – comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa2211ddef09e127b66430968792007d29dd5eb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840094"
---
# <a name="insert---sql-command"></a>INSERT – comando SQL
Acrescenta um registro ao final de uma tabela que contém os valores de campo especificado.  
  
 O Driver de ODBC do Visual FoxPro dá suporte à sintaxe de linguagem do Visual FoxPro nativo para esse comando. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>Argumentos  
 INSERT INTO *dbf_name*  
 Especifica o nome da tabela à qual o novo registro é acrescentado. *dbf_name* pode incluir um caminho e pode ser uma expressão de nome.  
  
 Se a tabela que você especificar não estiver aberta, ele será aberto exclusivamente em uma nova área de trabalho e o novo registro é acrescentado à tabela. A nova área de trabalho não estiver selecionada; a área de trabalho atual permanece selecionada.  
  
 Se a tabela que você especificar for aberta, INSERT acrescenta o novo registro na tabela. Se a tabela é aberta em uma área de trabalho, além de área de trabalho atual, ele não é selecionado depois que o registro for acrescentado; a área de trabalho atual permanece selecionada.  
  
 [( *fname1*[, *fname2*[,...]])]  
 Especifica no novo registro, os nomes dos campos em que os valores são inseridos.  
  
 VALORES ( *eExpression1*[, *eExpression2*[,...]])  
 Especifica os valores de campo inseridos no novo registro. Se você omitir os nomes de campo, você deve especificar os valores de campo na ordem definida pela estrutura de tabela.  
  
## <a name="remarks"></a>Comentários  
 O novo registro contém os dados listados na cláusula VALUES.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Quando seu aplicativo envia a instrução INSERT do ODBC SQL para a fonte de dados, o Driver de ODBC do Visual FoxPro converte o comando para o comando FoxProINSERT Visual sem tradução.  
  
## <a name="see-also"></a>Consulte também  
 [CREATE TABLE – comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT – comando SQL](../../odbc/microsoft/select-sql-command.md)
