---
title: sys.server_resource_stats (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.service: sql-database
ms.reviewer: carlrab, edmaca
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 2a0a1f82685cb107902c8065f2f696f615ad3930
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62744068"
---
# <a name="sysserverresourcestats-azure-sql-database"></a>sys.server_resource_stats (banco de dados SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Retorna os dados de armazenamento, de e/s e de utilização da CPU para uma instância gerenciada do SQL Azure. Os dados são coletados e agregados em intervalos de cinco minutos. Há uma linha para relatar a cada 15 segundos. Os dados retornados incluem o uso da CPU, tamanho de armazenamento, utilização de e/s e SKU de instância gerenciada. Os dados históricos são retidos por aproximadamente 14 dias.

O **sys.server_resource_stats** exibição tem definições diferentes dependendo da versão da instância gerenciada SQL do Azure que o banco de dados está associado. Considere essas diferenças e quaisquer modificações que seu aplicativo exige ao fazer a atualização para uma nova versão do servidor.
 
  
 A tabela a seguir descreve as colunas disponíveis em um servidor v12:  
  
|Colunas|Tipo de Dados|Descrição|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|Hora UTC que indica o início do intervalo de emissão de relatórios de 15 segundos|  
|end_time|**datetime**|Hora UTC que indica o final do intervalo de relatório de 15 segundos|
|resource_type|Nvarchar(128)|Tipo de recurso para o qual as métricas são fornecidas.|
|resource_name|nvarchar(128)|Nome do recurso.|
|sku|nvarchar(128)|Gerenciados de camada de serviço da instância da instância. O valores possíveis são os seguintes: <br><ul><li>Uso Geral</li></ul><ul><li>Comercialmente Crítica</li></ul>|
|hardware_generation|nvarchar(128)|Identificador de geração de hardware: como Gen 4 ou 5 Gen|
|virtual_core_count|INT|Representa o número de núcleos virtuais por instância (8, 16 ou 24 em visualização pública)|
|avg_cpu_percent|decimal(5,2)|Média de utilização em porcentagem do limite da camada de serviço de instância gerenciada utilizado pela instância de computação. Ele é calculado como a soma do tempo de CPU de todos os pools de recursos para todos os bancos de dados na instância e dividido pelo tempo de CPU disponível para essa camada em determinado intervalo.|
|reserved_storage_mb|BIGINT|Reservado armazenamento por instância (espaço de volume de armazenamento desse cliente adquirido para a instância gerenciada)|
|storage_space_used_mb|decimal(18,2)|Armazenamento usado pelos arquivos de todas as instância gerenciada dos bancos de dados (incluindo bancos de dados de usuário e sistema)|
|io_request|BIGINT|Número total de operações de e/s física dentro do intervalo|
|io_bytes_read|BIGINT|Número de bytes físicos dentro do intervalo de leitura|
|io_bytes_written|BIGINT|Número de bytes físicos escritos dentro do intervalo|

 
> [!TIP]  
>  Para obter mais contexto sobre esses limites e as camadas de serviço, consulte os tópicos [camadas de serviço da instância gerenciada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tier).  
    
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para conectar o **mestre** banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Os dados retornados pelo **sys.server_resource_stats** são expressas como o total usado em bytes ou em megabytes (mencionados em nomes de colunas) que não seja avg_cpu, que é expressa como uma porcentagem do máximo permitido de limites para o serviço nível de desempenho/camada que você está executando.  
 
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os bancos de dados que estão com média de pelo menos 80% de utilização de computação durante a última semana.  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT resource_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.server_resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY resource_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>Consulte também  
 [As camadas de serviço de instância de gerenciados](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tier)
