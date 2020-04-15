---
title: Execução Direta | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a89888ac055e83ab38588646f2f9b38ecd6444d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297968"
---
# <a name="direct-execution"></a>Execução direta
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A execução direta é o modo mais básico de executar uma instrução. Um aplicativo cria uma seqüência de caracteres contendo uma [!INCLUDE[tsql](../../../includes/tsql-md.md)] declaração e a envia para execução usando a função **SQLExecDirect.** Quando a instrução alcança o servidor, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a compila em um plano de execução e executa esse plano imediatamente.  
  
 A execução direta normalmente é usada por aplicativos que compilam e executam instruções no tempo de execução e é o método mais eficiente para instruções que serão executadas de uma só vez. O problema com muitos bancos de dados é que a instrução SQL deve ser analisada e compilada sempre que é executada, o que adiciona sobrecarga se a instrução for executada várias vezes.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aprimora significativamente o desempenho da execução direta de instruções executadas comumente em ambientes de vários usuários, e o uso de SQLExecDirect com marcadores de parâmetro para instruções SQL usadas normalmente pode abordar a eficiência da execução preparada.  
  
 Quando conectado a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância de , o driver Cliente Nativo ODBC usa [sp_executesql](../../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md) para transmitir a declaração SQL ou o lote especificado no **SQLExecDirect**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]tem lógica para determinar rapidamente se uma declaração SQL ou lote executado com **sp_executesql** corresponde à declaração ou lote que gerou um plano de execução que já existe na memória. Se houver correspondência, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] simplesmente reutilizará o plano existente, em vez de compilar um novo plano. Isso significa que as declarações SQL comumente executadas executadas com **O SQLExecDirect** em um sistema com muitos usuários se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]beneficiarão de muitos dos benefícios de reutilização do plano que só estavam disponíveis para procedimentos armazenados em versões anteriores de .  
  
 Esse benefício de reutilizar planos de execução só funciona quando vários usuários estiverem executando a mesma instrução ou lote SQL. Siga estas convenções de codificação para aumentar a probabilidade de as instruções SQL executadas por clientes diferentes serem semelhantes a ponto de permitirem a reutilização de planos de execução:  
  
-   Não inclua constantes de dados nas instruções SQL; em vez disso, use marcadores de parâmetro associados para programar variáveis. Para obter mais informações, consulte [Usando parâmetros de declaração](../../../relational-databases/native-client-odbc-queries/using-statement-parameters.md).  
  
-   Use nomes de objeto totalmente qualificados. Os planos de execução não serão reutilizados se os nomes de objeto não forem totalmente qualificados.  
  
-   Faça com que as conexões de aplicativo usem, na medida do possível, um conjunto comum de opções de conexão e instrução. Os planos de execução gerados para uma conexão com um conjunto de opções (como ANSI_NULLS) não são reutilizados para uma conexão que tenha outro conjunto de opções. O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client têm as mesmas configurações padrão para essas opções.  
  
 Se todas as declarações executadas com **o SQLExecDirect** forem codificadas usando essas convenções, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] poderão reutilizar planos de execução quando a oportunidade surgir.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de Declarações &#40;&#41;Da ODBC](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
