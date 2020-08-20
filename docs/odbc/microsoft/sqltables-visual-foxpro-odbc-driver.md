---
description: SQLTables (Driver ODBC do Visual FoxPro)
title: Sqltablenames (driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 089208ab612984283e3f87c4ad03aca0ccfa2b38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471548"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 1  
  
 Retorna a lista de nomes de tabela especificada pelo parâmetro na instrução **SQLTables** . Se nenhum parâmetro for especificado, retornará os nomes de tabela armazenados na fonte de dados atual. O driver retorna as informações como um conjunto de resultados.  
  
 Chamadas de tipo de enumeração não receberão uma entrada de conjunto de resultados para exibições remotas ou exibições com parâmetros locais. No entanto, uma chamada para **SQLTables** com um especificador de nome de tabela exclusivo encontrará uma correspondência para tal exibição, se estiver presente com esse nome; Isso permite que a API seja usada para verificar se há conflitos de nome antes da criação de uma nova tabela.  
  
> [!NOTE]  
>  O driver ODBC do Visual FoxPro diferencia entre [tabelas de banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) e [tabelas gratuitas](../../odbc/microsoft/visual-foxpro-terminology.md), mesmo quando ambos os tipos de tabelas são armazenados no mesmo diretório em seu sistema. Se sua fonte de dados for um diretório de tabelas livres, o driver ODBC do Visual FoxPro não catalogará nem retornará os nomes de todas as tabelas associadas a um banco de dados.  
  
 Para obter mais informações, consulte [SQLTables](../../odbc/reference/syntax/sqltables-function.md) na *referência do programador de ODBC*.
