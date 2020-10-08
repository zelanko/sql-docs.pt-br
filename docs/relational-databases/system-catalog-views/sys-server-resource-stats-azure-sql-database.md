---
description: sys.server_resource_stats (banco de dados SQL do Azure)
title: sys.server_resource_stats (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.service: sql-database
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
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 57d0a8e10eb79213de7eb29a2d18ea8837d7f908
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809312"
---
# <a name="sysserver_resource_stats-azure-sql-database"></a>sys.server_resource_stats (banco de dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

Retorna o uso da CPU, e/s e dados de armazenamento para o Azure SQL Instância Gerenciada. Os dados são coletados e agregados em intervalos de cinco minutos. Há uma linha para cada relatório de 15 segundos. Os dados retornados incluem uso de CPU, tamanho de armazenamento, utilização de e/s e SKU. Os dados históricos são retidos por aproximadamente 14 dias.

A exibição **Sys.server_resource_stats** tem definições diferentes, dependendo da versão do instância gerenciada do Azure SQL ao qual o banco de dados está associado. Considere essas diferenças e quaisquer modificações que seu aplicativo exige ao fazer a atualização para uma nova versão do servidor.
 
  
 A tabela a seguir descreve as colunas disponíveis em um servidor v12:  
  
|Colunas|Tipo de Dados|Descrição|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|Hora UTC indicando o início do intervalo de relatório de quinze segundos|  
|end_time|**datetime**|Hora UTC indicando o final do intervalo de relatórios de quinze segundos|
|resource_type|Nvarchar (128)|Tipo do recurso para o qual as métricas são fornecidas|
|resource_name|nvarchar(128)|Nome do recurso.|
|sku|nvarchar(128)|Instância Gerenciada camada de serviço da instância. O valores possíveis são os seguintes: <br><ul><li>Uso Geral</li></ul><ul><li>Comercialmente Crítico</li></ul>|
|hardware_generation|nvarchar(128)|Identificador de geração de hardware: como Gen 4 ou Gen 5|
|virtual_core_count|INT|Representa o número de núcleos virtuais por instância (8, 16 ou 24 em visualização pública)|
|avg_cpu_percent|decimal (5, 2)|Média de utilização de computação em porcentagem do limite do Instância Gerenciada camada de serviço utilizada pela instância. Ele é calculado como a soma do tempo de CPU de todos os pools de recursos para todos os bancos de dados na instância e dividido por tempo de CPU disponível para essa camada no intervalo especificado.|
|reserved_storage_mb|BIGINT|Armazenamento reservado por instância (quantidade de espaço de armazenamento que o cliente comprou para a instância gerenciada)|
|storage_space_used_mb|decimal (18, 2)|Armazenamento usado por todos os arquivos de banco de dados em uma instância gerenciada (incluindo bancos de dados do usuário e do sistema)|
|io_request|BIGINT|Número total de operações físicas de e/s dentro do intervalo|
|io_bytes_read|BIGINT|Número de bytes físicos lidos dentro do intervalo|
|io_bytes_written|BIGINT|Número de bytes físicos gravados no intervalo|

 
> [!TIP]  
>  Para obter mais contexto sobre esses limites e camadas de serviço, consulte os tópicos [instância gerenciada camadas de serviço](/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers).  
    
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao banco de dados **mestre** .  
  
## <a name="remarks"></a>Comentários  
 Os dados retornados por **Sys.server_resource_stats** são expressos como o total usado em bytes ou megabytes (declarados em nomes de coluna) que não seja avg_cpu, que é expresso como uma porcentagem do limite máximo permitido para a camada de serviço/nível de desempenho que você está executando.  
 
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
    
## <a name="see-also"></a>Consulte Também  
 [Instância Gerenciada camadas de serviço](/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)