---
title: Alterações no comportamento de String-Length e substring | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18643dfc11d2b1b1d875a19c478f9ec8cbdd5be6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66428841"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>Alterações no comportamento de string-length e substring
  A [função de comprimento da cadeia de caracteres &#40;xquery&#41;](/sql/xquery/functions-on-string-values-string-length) e a [função substring &#40;funções do XQuery&#41;](/sql/xquery/functions-on-string-values-substring) podem retornar resultados diferentes quando usadas com bancos de dados XML que contêm caracteres substitutos.  
  
## <a name="description"></a>Descrição  
 Quando um banco de dados é definido para ser [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]compatível com, o comportamento da [função de comprimento da cadeia de caracteres &#40;XQuery&#41;](/sql/xquery/functions-on-string-values-string-length) e a [função substring &#40;XQuery&#41;](/sql/xquery/functions-on-string-values-substring) funções são alteradas ao lidar com caracteres suplementares Unicode. Cada caractere suplementar Unicode definido para ter um ponto de código maior que U+FFFF, é contado como um caractere por essas funções, em vez de dois, como era contado em versões anteriores.  
  
 Para obter mais informações sobre caracteres substitutos, consulte [Surrogates and Supplementary Characters](https://go.microsoft.com/fwlink/?LinkId=178317)(em inglês).  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
