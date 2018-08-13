---
title: Compatibilidade entre versões | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: c53ac418f6d394fbb6bdfeacccbe5244ecae62b4
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39562550"
---
# <a name="cross-version-compatibility"></a>Compatibilidade entre versões
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Podem ocorrer conflitos entre versões quando instâncias do cliente e do servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] são esperadas para processar parâmetros com valor de tabela.  
  
 Em geral, a funcionalidade de parâmetros com valor de tabela estão disponíveis apenas em clientes [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (que utilizam o SQL Server Native Client 10.0) ou posteriores que estão conectados a servidores [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posteriores). Colunas novas em conjuntos de resultados de funções de catálogo estarão presentes somente quando conectado a um [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior) server.  
  
 Se um aplicativo cliente compilado com uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client executar instruções que esperam parâmetros com valor de tabela, o servidor detectará essa condição por meio de um erro de conversão de dados, e o ODBC retornará com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados restrito".  
  
 Se um aplicativo cliente que foi compilado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10.0 ou posterior tentar usar parâmetros com valor de tabela quando conectado a uma instância de servidor anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client irá detectar isso e SQLBindCol, Chamadas SQLBindParameter, SQLSetDescFields e SQLSetDescRec falhará com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados (a versão do SQL Server para esta conexão não oferece suporte a parâmetros com valor de tabela) de Restricted".  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
