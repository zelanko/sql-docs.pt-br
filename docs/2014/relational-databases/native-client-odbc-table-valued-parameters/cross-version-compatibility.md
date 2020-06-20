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
author: rothja
ms.author: jroth
ms.openlocfilehash: af434713946f5c568ee71644a7403f9496a8c16f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049709"
---
# <a name="cross-version-compatibility"></a>Compatibilidade entre versões
  Podem ocorrer conflitos entre versões quando instâncias do cliente e do servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] são esperadas para processar parâmetros com valor de tabela.  
  
 Em geral, a funcionalidade de parâmetros com valor de tabela estão disponíveis apenas em clientes [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (que utilizam o SQL Server Native Client 10.0) ou posteriores que estão conectados a servidores [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posteriores). As novas colunas nos conjuntos de resultados da função de catálogo só estarão presentes quando conectadas a um [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] servidor (ou posterior).  
  
 Se um aplicativo cliente compilado com uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client executar instruções que esperam parâmetros com valor de tabela, o servidor detectará essa condição por meio de um erro de conversão de dados, e o ODBC retornará com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados restrito".  
  
 Se um aplicativo cliente que foi compilado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Native client 10,0 ou posterior tentar usar parâmetros com valor de tabela quando conectado a uma instância de servidor anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Native Client detectará isso, e as chamadas SQLBindCol, SQLBindParameter, SQLSetDescFields e SQLSetDescRec falharão com SQLSTATE 07006 e a mensagem "violação de atributo de tipo de dados restritos (a versão do SQL Server para essa conexão não oferece suporte a parâmetros com  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;&#41;ODBC](table-valued-parameters-odbc.md)  
  
  
