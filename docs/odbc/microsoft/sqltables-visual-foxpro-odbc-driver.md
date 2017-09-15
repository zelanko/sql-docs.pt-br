---
title: SQLTables (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd3e59437eae02a94353a6205e567fde208f4b97
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade de API de ODBC: Nível 1  
  
 Retorna a lista de nomes de tabela especificado pelo parâmetro no **SQLTables** instrução. Se nenhum parâmetro for especificado, retorna os nomes de tabela armazenados na fonte de dados atual. O driver retorna as informações como um conjunto de resultados.  
  
 Chamadas de tipo de enumeração não receberão uma entrada de conjunto de resultados para modos de exibição remotos ou locais exibições com parâmetros. No entanto, uma chamada para **SQLTables** com uma tabela exclusiva especificador de nome encontrará uma correspondência para um modo de exibição se estiver presente com esse nome; Isso permite que a API a ser usado para verificar se há conflitos de nome antes da criação de uma nova tabela.  
  
> [!NOTE]  
>  O driver ODBC do Visual FoxPro diferencia [tabelas de banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) e [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md), mesmo quando os dois tipos de tabelas são armazenados no mesmo diretório em seu sistema. Se sua fonte de dados é um diretório de tabelas livres, o Driver de ODBC do Visual FoxPro não catálogo ou retornar os nomes de todas as tabelas que estão associados um banco de dados.  
  
 Para obter mais informações, consulte [SQLTables](../../odbc/reference/syntax/sqltables-function.md) no *referência do programador de ODBC*.
