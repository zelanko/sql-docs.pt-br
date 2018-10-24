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
ms.openlocfilehash: 8f7520a4e9bdc346113e4777bd6899f5ccc0e01c
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460311"
---
# <a name="polybase-features-and-limitations"></a>Recursos e limitações do PolyBase

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

## <a name="known-limitations"></a>Limitações conhecidas

O PolyBase apresenta as seguintes limitações:

- O tamanho máximo de linha possível, incluindo o comprimento total das colunas de comprimento variável, não pode exceder 32 KB no SQL Server ou 1 MB no SQL Data Warehouse do Azure.

- O PolyBase não dá suporte aos tipos de dados de Hive 0,12 + (ou seja, Char(), VarChar())

- Durante a exportação de dados em um Formato de Arquivo ORC do SQL Server ou do Azure SQL Data Warehouse, as colunas com excesso de texto podem ser limitadas a até 50 colunas, devido a erros de memória insuficiente do Java. Para solucionar esse problema, exporte apenas um subconjunto das colunas.

- Não é possível ler ou gravar dados criptografados em repouso no Hadoop. Isso inclui a Criptografia Transparente ou as Zonas Criptografadas do HDFS.

- O PolyBase não poderá se conectar a uma instância de Hortonworks se o KNOX estiver habilitado.

- Se você estiver usando tabelas do Hive com transacional = true, o PolyBase não poderá acessar os dados no diretório da tabela do Hive.

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [O PolyBase não é instalado durante a adição de um nó a um Cluster de Failover do SQL Server 2016](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)

::: moniker-end

- A autenticação de integração não é compatível. Somente o nome de usuário e a senha são compatíveis por enquanto.  

- A criptografia é habilitada por padrão.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, confira [O que é o PolyBase?](polybase-guide.md).
