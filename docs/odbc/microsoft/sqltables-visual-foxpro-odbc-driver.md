---
title: SQLTables (visual FoxPro ODBC Driver) | Microsoft Docs
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
ms.openlocfilehash: 5467fc8c1717d5ceb548b3950a0894fd2a1b4499
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299276"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível 1  
  
 Retorna a lista de nomes de tabela especificados pelo parâmetro na declaração **SQLTables.** Se nenhum parâmetro for especificado, retorna os nomes de tabela armazenados na fonte de dados atual. O motorista retorna as informações como um conjunto de resultados.  
  
 As chamadas do tipo de enumeração não receberão uma entrada definida de resultado para visualizações remotas ou visualizações parametrizadas locais. No entanto, uma chamada para **SQLTables** com um especificador de nome de tabela exclusivo encontrará uma correspondência para tal exibição se estiver presente com esse nome; isso permite que a API seja usada para verificar conflitos de nome antes da criação de uma nova tabela.  
  
> [!NOTE]  
>  O driver Visual FoxPro ODBC diferencia entre [tabelas de banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) e [tabelas gratuitas,](../../odbc/microsoft/visual-foxpro-terminology.md)mesmo quando ambos os tipos de tabelas são armazenadas no mesmo diretório do seu sistema. Se sua fonte de dados for um diretório de tabelas gratuitas, o Visual FoxPro ODBC Driver não cataloga ou retorna os nomes de quaisquer tabelas que estejam associadas a um banco de dados.  
  
 Para obter mais informações, consulte [SQLTables](../../odbc/reference/syntax/sqltables-function.md) no *Programador ODBC*.
