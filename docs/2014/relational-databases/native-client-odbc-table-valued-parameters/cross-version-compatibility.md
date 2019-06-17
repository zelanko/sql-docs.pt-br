---
title: Compatibilidade entre versões | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f23b0f43b32d737f03cb7c9b00368558e89e9288
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199998"
---
# <a name="cross-version-compatibility"></a>Compatibilidade entre versões
  Podem ocorrer conflitos entre versões quando instâncias do cliente e do servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] são esperadas para processar parâmetros com valor de tabela.  
  
 Em geral, a funcionalidade de parâmetros com valor de tabela estão disponíveis apenas em clientes [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (que utilizam o SQL Server Native Client 10.0) ou posteriores que estão conectados a servidores [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posteriores). Colunas novas em conjuntos de resultados de funções de catálogo estarão presentes somente quando conectado a um [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior) server.  
  
 Se um aplicativo cliente compilado com uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client executar instruções que esperam parâmetros com valor de tabela, o servidor detectará essa condição por meio de um erro de conversão de dados, e o ODBC retornará com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados restrito".  
  
 Se um aplicativo cliente que foi compilado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10.0 ou posterior tentar usar parâmetros com valor de tabela quando conectado a uma instância de servidor anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client irá detectar isso e SQLBindCol, Chamadas SQLBindParameter, SQLSetDescFields e SQLSetDescRec falhará com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados (a versão do SQL Server para esta conexão não oferece suporte a parâmetros com valor de tabela) de Restricted".  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
