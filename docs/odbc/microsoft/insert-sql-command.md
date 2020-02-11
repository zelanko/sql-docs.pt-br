---
title: INSERIR-comando SQL | Microsoft Docs
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
ms.openlocfilehash: 884a33339db10ee8e07d8b432d1765720d45734a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019456"
---
# <a name="insert---sql-command"></a>INSERT – comando SQL
Anexa um registro ao final de uma tabela que contém os valores de campo especificados.  
  
 O driver ODBC do Visual FoxPro dá suporte à sintaxe de linguagem nativa do Visual FoxPro para este comando. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>Argumentos  
 INSERIR em *dbf_name*  
 Especifica o nome da tabela para a qual o novo registro é acrescentado. *dbf_name* pode incluir um caminho e pode ser uma expressão de nome.  
  
 Se a tabela especificada não estiver aberta, ela será aberta exclusivamente em uma nova área de trabalho e o novo registro será anexado à tabela. A nova área de trabalho não está selecionada; a área de trabalho atual permanece selecionada.  
  
 Se a tabela que você especificar estiver aberta, INSERT acrescentará o novo registro à tabela. Se a tabela estiver aberta em uma área de trabalho diferente da área de trabalho atual, ela não será selecionada depois que o registro for anexado; a área de trabalho atual permanece selecionada.  
  
 [( *fname1*[, *fname2*[,...]])]  
 Especifica no novo registro os nomes dos campos nos quais os valores são inseridos.  
  
 VALORES ( *eExpression1*[, *eExpression2*[,...]])  
 Especifica os valores de campo inseridos no novo registro. Se você omitir os nomes de campo, deverá especificar os valores de campo na ordem definida pela estrutura de tabela.  
  
## <a name="remarks"></a>Comentários  
 O novo registro contém os dados listados na cláusula VALUEs.  
  
## <a name="driver-remarks"></a>Comentários do driver  
 Quando o aplicativo envia a instrução SQL ODBC INSERT para a fonte de dados, o driver ODBC do Visual FoxPro converte o comando no comando FoxProINSERT do Visual sem tradução.  
  
## <a name="see-also"></a>Consulte Também  
 [Comando CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT – comando SQL](../../odbc/microsoft/select-sql-command.md)
