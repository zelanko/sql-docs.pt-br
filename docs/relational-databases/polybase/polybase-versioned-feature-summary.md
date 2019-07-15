---
title: Recursos e limitações do PolyBase | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: aboke
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e4a267e98b38ff294366ce198518ffdb3062d460
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67731955"
---
# <a name="polybase-features-and-limitations"></a>Recursos e limitações do PolyBase

[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

Este artigo é um resumo dos recursos do PolyBase disponíveis para produtos e serviços do SQL Server.  
  
## <a name="feature-summary-for-product-releases"></a>Resumo de recursos para versões do produto

Esta tabela lista os principais recursos para o PolyBase e os produtos nos quais estão disponíveis.  
  
||||||
|-|-|-|-|-|   
|**Recurso**|**SQL Server 2016**|**Banco de Dados SQL do Azure**|**Azure SQL Data Warehouse**|**Parallel Data Warehouse**| 
|Consultar dados do Hadoop com [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|Não|Não|Sim|
|Importar dados do Hadoop|Sim|Não|Não|Sim|
|Exportar dados para o Hadoop  |Sim|Não|Não| Sim|
|Consultar, importar e exportar para o Azure HDInsight |Não|Não|Não|Não
|Enviar cálculos de consulta por push ao Hadoop|Sim|Não|Não|Sim|  
|Importar dados do Armazenamento de Blobs do Azure|Sim|Não|Sim|Sim| 
|Exportar dados para o Armazenamento de Blobs do Azure|Sim|Não|Sim|Sim|  
|Importar dados do Azure Data Lake Store|Não|Não|Sim|Não|    
|Exportar dados do Azure Data Lake Store|Não|Não|Sim|Não|
|Executar consultas do PolyBase nas ferramentas do Microsoft BI|Sim|Não|Sim|Sim|   

## <a name="pushdown-computation-supported-by-t-sql-operators"></a>Computação de aplicação com suporte para operadores do T-SQL

No SQL Server e no APS, nem todos os operadores do T-SQL podem ser aplicados ao cluster do Hadoop. A tabela a seguir lista todos os operadores com suporte e um subconjunto de operadores sem suporte. 

||||
|-|-|-| 
|**Tipo de operador**|**Pode ser enviado por push para Hadoop**|**Pode ser enviado por push para o Armazenamento de Blobs**|
|Projeções de coluna|Sim|Não|
|Predicados|Sim|Não|
|Agregações|Parcial|Não|
|Junções entre tabelas externas|Não|Não|
|Junções entre tabelas externas e tabelas locais|Não|Não|
|Classificações|Não|Não|

A agregação parcial significa que uma agregação final deve ocorrer depois que os dados atingirem o SQL Server. Porém, uma parte da agregação ocorre no Hadoop. Esse método é comum nas agregações de computação em sistemas de processamento massivamente paralelos.  

## <a name="known-limitations"></a>Limitações conhecidas

O PolyBase apresenta as seguintes limitações:

- Para usar o PolyBase, você deve permissões no nível de sysadmin ou SERVER CONTROL no banco de dados.

- O tamanho máximo de linha possível, incluindo o comprimento total das colunas de comprimento variável, não pode exceder 32 KB no SQL Server ou 1 MB no SQL Data Warehouse do Azure.

- Quando os dados são exportados em um formato de arquivo ORC do SQL Server ou do SQL Data Warehouse, as colunas com muito texto podem ser limitadas. Podem ser limitados a apenas 50 colunas devido a mensagens de erro de falta de memória do Java. Para solucionar esse problema, exporte apenas um subconjunto das colunas.

- O PolyBase não poderá se conectar a uma instância do Hortonworks se o Knox estiver habilitado.

- Se estiver usando tabelas do Hive com transacional = true, o PolyBase não poderá acessar os dados no diretório da tabela do Hive.

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [O PolyBase não será instalado durante a adição de um nó a um cluster de failover do SQL Server 2016](https://support.microsoft.com/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster).

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o PolyBase, consulte [What is PolyBase](polybase-guide.md) (O que é o PolyBase?).
