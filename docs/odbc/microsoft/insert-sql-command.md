---
title: INSERT - Comando SQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ce00005fb1aa0ca9732fc5e9cfeacd6faf6ef9e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299997"
---
# <a name="insert---sql-command"></a>INSERT – comando SQL
Anexa um registro até o final de uma tabela que contém os valores de campo especificados.  
  
 O Visual FoxPro ODBC Driver suporta a sintaxe nativa visual foxpro para este comando. Para obter informações específicas do motorista, consulte as observações.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>Argumentos  
 INSIRA *EM DBF_NAME*  
 Especifica o nome da tabela à qual o novo registro é anexado. *dbf_name* pode incluir um caminho e pode ser uma expressão de nome.  
  
 Se a tabela especificada não estiver aberta, ela será aberta exclusivamente em uma nova área de trabalho e o novo registro será anexado à tabela. A nova área de trabalho não está selecionada; a área de trabalho atual permanece selecionada.  
  
 Se a tabela especificada estiver aberta, INSERT anexará o novo registro à tabela. Se a tabela estiver aberta em uma área de trabalho diferente da área de trabalho atual, ela não será selecionada após a anexação do registro; a área de trabalho atual permanece selecionada.  
  
 [( *fname1*[, *fname2*[, ...]]]  
 Especifica no novo registro os nomes dos campos nos quais os valores são inseridos.  
  
 VALORES ( *eExpression1*[, *eExpression2*[, ...]]  
 Especifica os valores de campo inseridos no novo registro. Se você omitir os nomes de campo, você deve especificar os valores de campo na ordem definida pela estrutura da tabela.  
  
## <a name="remarks"></a>Comentários  
 O novo registro contém os dados listados na cláusula VALORES.  
  
## <a name="driver-remarks"></a>Observações do motorista  
 Quando seu aplicativo envia a instrução ODBC SQL INSERT para a fonte de dados, o Driver Visual FoxPro ODBC converte o comando no comando Visual FoxProINSERT sem tradução.  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR TABELA - Comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT – comando SQL](../../odbc/microsoft/select-sql-command.md)
