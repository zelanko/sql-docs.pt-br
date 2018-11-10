---
title: Recursos e limitações do PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08d0b31d5ed0be4b3d9a5e766483f14e0653343e
ms.sourcegitcommit: 41979c9d511b3eeb45134d30ccb0dbc6bba70f1a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757961"
---
# <a name="polybase-features-and-limitations"></a>Recursos e limitações do PolyBase

[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

Este artigo é um resumo dos recursos do PolyBase disponíveis para produtos e serviços do SQL Server.  
  
## <a name="feature-summary-for-product-releases"></a>Resumo de recursos para versões do produto

Esta tabela lista os principais recursos para o PolyBase e os produtos nos quais estão disponíveis.  
  
||||||
|-|-|-|-|-|   
|**Recurso**|**SQL Server 2016**|**Banco de Dados SQL do Azure**|**Azure SQL Data Warehouse**|**Parallel Data Warehouse**| 
|Consultar dados do Hadoop com [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|não|não|Sim|
|Importar dados do Hadoop|Sim|não|não|Sim|
|Exportar dados para o Hadoop  |Sim|não|não| Sim|
|Consultar, importar e exportar para o Azure HDInsight |não|não|não|não
|Enviar cálculos de consulta por push ao Hadoop|Sim|não|não|Sim|  
|Importar dados do Armazenamento de Blobs do Azure|Sim|não|Sim|Sim| 
|Exportar dados para o Armazenamento de Blobs do Azure|Sim|não|Sim|Sim|  
|Importar dados do Azure Data Lake Store|não|não|Sim|não|    
|Exportar dados do Azure Data Lake Store|não|não|Sim|não|
|Executar consultas do PolyBase nas ferramentas do Microsoft BI|Sim|não|Sim|Sim|   

## <a name="pushdown-computation-supported-by-t-sql-operators"></a>Computação de aplicação com suporte para operadores do T-SQL

No SQL Server e no APS, nem todos os operadores do T-SQL podem ser aplicados ao cluster do Hadoop. A tabela a seguir lista todos os operadores com suporte e um subconjunto de operadores sem suporte. 

||||
|-|-|-| 
|**Tipo de operador**|**Pode ser enviado por push para Hadoop**|**Pode ser enviado por push para o Armazenamento de Blobs**|
|Projeções de coluna|Sim|não|
|Predicados|Sim|não|
|Agregações|Parcial|não|
|Junções entre tabelas externas|não|não|
|Junções entre tabelas externas e tabelas locais|não|não|
|Classificações|não|não|

A agregação parcial significa que uma agregação final deve ocorrer depois que os dados atingirem o SQL Server. Porém, uma parte da agregação ocorre no Hadoop. Esse método é comum nas agregações de computação em sistemas de processamento massivamente paralelos.  

## <a name="known-limitations"></a>Limitações conhecidas

O PolyBase apresenta as seguintes limitações:

- O tamanho máximo de linha possível, incluindo o comprimento total das colunas de comprimento variável, não pode exceder 32 KB no SQL Server ou 1 MB no SQL Data Warehouse do Azure.

- Quando os dados são exportados em um formato de arquivo ORC do SQL Server ou do SQL Data Warehouse, as colunas com muito texto podem ser limitadas. Podem ser limitados a apenas 50 colunas devido a mensagens de erro de falta de memória do Java. Para solucionar esse problema, exporte apenas um subconjunto das colunas.

- O PolyBase não poderá se conectar a uma instância do Hortonworks se o Knox estiver habilitado.

- Se estiver usando tabelas do Hive com transacional = true, o PolyBase não poderá acessar os dados no diretório da tabela do Hive.

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [O PolyBase não será instalado durante a adição de um nó a um cluster de failover do SQL Server 2016](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster).

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o PolyBase, consulte [What is PolyBase](polybase-guide.md) (O que é o PolyBase?).
