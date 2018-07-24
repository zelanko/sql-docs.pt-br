---
title: Resumo de recursos com controle de versão do PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.technology: polybase
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: df01d5e4503aeb4004f06ec0310ac613a6318d8b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993967"
---
# <a name="polybase-versioned-feature-summary"></a>Resumo de recursos com controle de versão do PolyBase
[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]
Resumo dos recursos do PolyBase disponíveis para produtos e serviços do SQL Server.  
  
## <a name="feature-summary-for-product-releases"></a>Resumo de recursos para versões do produto  
 Esta tabela resume os principais recursos para o PolyBase e os produtos nos quais eles estão disponíveis.  
  
||||||
|-|-|-|-|-|   
|**Recurso**|**SQL Server 2016**|**Banco de Dados SQL do Azure**|**Azure SQL Data Warehouse**|**Parallel Data Warehouse**| 
|Consultar dados do Hadoop com [!INCLUDE[tsql](../../includes/tsql-md.md)]|sim|não|não|sim|
|Importar dados do Hadoop|sim|não|não|sim|
|Exportar dados para o Hadoop  |sim|não|não| sim|
|Consultar, importar e exportar para o HDInsights |não|não|não|não
|Enviar cálculos de consulta por push ao Hadoop|sim|não|não|sim|  
|Importar dados do armazenamento de blobs do Azure|sim|não|sim|sim| 
|Exportar dados para o armazenamento de blobs do Azure|sim|não|sim|sim|  
|Importar dados do Azure Data Lake Store|não|não|sim|não|    
|Exportar dados do Azure Data Lake Store|não|não|sim|não|
|Executar consultas do PolyBase nas ferramentas de BI da Microsoft|sim|não|sim|sim|   


## <a name="pushdown-computation-supported-t-sql-operators"></a>Operadores T-SQL com suporte para computação de aplicação
No SQL Server e no APS, nem todos os operadores T-SQL podem ser aplicados ao cluster hadoop. A tabela a seguir lista todos com suporte e um subconjunto dos operadores sem suporte. 

||||
|-|-|-| 
|**Tipo de operador**|**Pode ser enviado por push para Hadoop**|**Pode ser enviado por push para Armazenamento de Blobs**|
|Projeções de coluna|sim|não|
|Predicados|sim|não|
|Agregações|parcial|não|
|Junções entre tabelas externas|não|não|
|Junções entre tabelas externas e tabelas locais|não|não|
|Classificações|não|não|

Agregação parcial significa que uma agregação final deve ocorrer depois que os dados atingirem o SQL Server, mas uma parte da agregação ocorre no Hadoop. Este é uma agregação de computação de método comum em sistemas de Processamento Paralelo Maciço.  
## <a name="see-also"></a>Consulte Também  
 [Guia do PolyBase](../../relational-databases/polybase/polybase-guide.md)  
  
  
