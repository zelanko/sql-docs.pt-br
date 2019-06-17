---
title: SQLTables (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e134b2870c4506e725f2900b83d1118e42b55d15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63219115"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível 1  
  
 Retorna a lista de nomes de tabela especificado pelo parâmetro na **SQLTables** instrução. Se nenhum parâmetro for especificado, retorna os nomes de tabela, armazenados na fonte de dados atual. O driver retorna as informações como um conjunto de resultados.  
  
 Chamadas de tipo de enumeração não receberão uma entrada de conjunto de resultados para modos de exibição remotos ou locais exibições com parâmetros. No entanto, uma chamada para **SQLTables** com uma tabela exclusiva especificador de nome encontrará uma correspondência para um modo de exibição se estiver presente com esse nome; Isso permite que a API a ser usado para verificar se há conflitos de nome antes da criação de uma nova tabela.  
  
> [!NOTE]  
>  O driver ODBC do Visual FoxPro diferencia [tabelas de banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) e [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md), mesmo quando ambos os tipos de tabelas são armazenados no mesmo diretório em seu sistema. Se sua fonte de dados é um diretório de tabelas livres, o Driver de ODBC do Visual FoxPro do catálogo não ou retornar os nomes de todas as tabelas que estão associados um banco de dados.  
  
 Para obter mais informações, consulte [SQLTables](../../odbc/reference/syntax/sqltables-function.md) na *referência do programador de ODBC*.
