---
title: Execução direta | Microsoft Docs
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
ms.openlocfilehash: 73cd53e5b9c83fe77027b8260d46bc5b989e91a6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775940"
---
# <a name="direct-execution"></a>Execução direta
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  A execução direta é o modo mais básico de executar uma instrução. Um aplicativo cria uma cadeia de caracteres que contém uma [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução e a envia para execução usando a função **SQLExecDirect** . Quando a instrução alcança o servidor, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a compila em um plano de execução e executa esse plano imediatamente.  
  
 A execução direta normalmente é usada por aplicativos que compilam e executam instruções no tempo de execução e é o método mais eficiente para instruções que serão executadas de uma só vez. O problema com muitos bancos de dados é que a instrução SQL deve ser analisada e compilada sempre que é executada, o que adiciona sobrecarga se a instrução for executada várias vezes.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aprimora significativamente o desempenho da execução direta de instruções executadas comumente em ambientes de vários usuários, e o uso de SQLExecDirect com marcadores de parâmetro para instruções SQL usadas normalmente pode abordar a eficiência da execução preparada.  
  
 Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client usa [sp_executesql](../../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md) para transmitir a instrução SQL ou o lote especificado em **SQLExecDirect**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]tem a lógica para determinar rapidamente se uma instrução SQL ou um lote executado com **sp_executesql** corresponde à instrução ou ao lote que gerou um plano de execução que já existe na memória. Se houver correspondência, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] simplesmente reutilizará o plano existente, em vez de compilar um novo plano. Isso significa que as instruções SQL comumente executadas executadas com **SQLExecDirect** em um sistema com muitos usuários se beneficiarão de muitos benefícios de reutilização de plano que só estavam disponíveis para procedimentos armazenados em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Esse benefício de reutilizar planos de execução só funciona quando vários usuários estiverem executando a mesma instrução ou lote SQL. Siga estas convenções de codificação para aumentar a probabilidade de as instruções SQL executadas por clientes diferentes serem semelhantes a ponto de permitirem a reutilização de planos de execução:  
  
-   Não inclua constantes de dados nas instruções SQL; em vez disso, use marcadores de parâmetro associados para programar variáveis. Para obter mais informações, consulte [usando parâmetros de instrução](../../../relational-databases/native-client-odbc-queries/using-statement-parameters.md).  
  
-   Use nomes de objeto totalmente qualificados. Os planos de execução não serão reutilizados se os nomes de objeto não forem totalmente qualificados.  
  
-   Faça com que as conexões de aplicativo usem, na medida do possível, um conjunto comum de opções de conexão e instrução. Os planos de execução gerados para uma conexão com um conjunto de opções (como ANSI_NULLS) não são reutilizados para uma conexão que tenha outro conjunto de opções. O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client têm as mesmas configurações padrão para essas opções.  
  
 Se todas as instruções executadas com **SQLExecDirect** forem codificadas usando essas convenções, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] poderá reutilizar planos de execução quando a oportunidade surgir.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando instruções &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
