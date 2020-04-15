---
title: SQLExtendedFetch (driver Visual FoxPro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ecff538198a2b517f980cc63acfc97d29a9f162
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298646"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível 2  
  
 Semelhante ao [SQLFetch,](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) mas retorna várias linhas usando uma matriz para cada coluna. O conjunto de resultados é rolável para a frente e pode ser feito para trás se o cursor for definido como estático, não apenas para frente.  
  
 Por padrão, o Driver Visual FoxPro ODBC não retorna linhas marcadas como excluídas em uma tabela FoxPro. As linhas marcadas para exclusão, mas ainda não removidas de uma tabela, não estão incluídas no cursor do conjunto de resultados. Você pode alterar esse comportamento usando o comando [SET DELETED.](../../odbc/microsoft/set-deleted-command.md)  
  
 Para obter mais informações, consulte [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) na *referência do programador ODBC*.
