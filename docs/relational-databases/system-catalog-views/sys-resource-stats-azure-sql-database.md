---
title: sys. resource_stats (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.service: sql-database
ms.reviewer: ''
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
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f151d62a03cebf931c58f37b1e126a7331cefae9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68418873"
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna os dados de armazenamento e de utilização da CPU para um Banco de Dados SQL do Azure. Os dados são coletados e agregados em intervalos de cinco minutos. Para cada banco de dados de usuário, há uma linha para cada janela de relatório de cinco minutos, na qual há uma alteração no consumo de recursos. Os dados retornados incluem uso de CPU, alteração de tamanho de armazenamento e modificação de SKU de banco de dados. Bancos de dados ociosos sem alterações podem não ter linhas para cada intervalo de cinco minutos. Os dados históricos são retidos por aproximadamente 14 dias.  
  
 A exibição **Sys. resource_stats** tem definições diferentes, dependendo da versão do servidor de banco de dados SQL do Azure ao qual o banco de dados está associado. Considere essas diferenças e quaisquer modificações que seu aplicativo exige ao fazer a atualização para uma nova versão do servidor.  
  
 A tabela a seguir descreve as colunas disponíveis em um servidor v12:  
  
|Colunas|Tipo de dados|Descrição|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|Hora UTC indicando o início do intervalo de relatórios de cinco minutos.|  
|end_time|**datetime**|Hora UTC indicando o final do intervalo de relatórios de cinco minutos.|  
|database_name|**nvarchar(128)**|Nome do banco de dados do usuário.|  
|sku|**nvarchar(128)**|Camada de serviço do banco de dados. O valores possíveis são os seguintes:<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br />Uso Geral<br /><br />Comercialmente Crítica|  
|storage_in_megabytes|**float**|O tamanho máximo de armazenamento em megabytes para o período de tempo, incluindo dados do banco de dados, índices, procedimentos armazenados e metadados.|  
|avg_cpu_percent|**decimal(5,2)**|Utilização média de computação, em porcentagem, do limite da camada de serviço.|  
|avg_data_io_percent|**decimal(5,2)**|Utilização média de E/S em percentagem com base no limite da camada de serviço.|  
|avg_log_write_percent|**decimal(5,2)**|Utilização média do recurso de gravação, em porcentagem, do limite da camada de serviço.|  
|max_worker_percent|**decimal(5,2)**|Máximo de trabalhos simultâneos (solicitações) em porcentagem com base no limite da camada de serviço do banco de dados.<br /><br /> No momento, o máximo é calculado para o intervalo de cinco minutos com base nas amostras de 15 segundos de contagens de trabalho simultâneas.|  
|max_session_percent|**decimal(5,2)**|Máximo de sessões simultâneas em porcentagem com base no limite da camada de serviço do banco de dados.<br /><br /> No momento, o máximo é calculado para o intervalo de cinco minutos com base nas amostras de 15 segundos de contagens de sessão simultâneas.|  
|dtu_limit|**int**|Configuração de DTU máxima do banco de dados atual para este banco de dados durante esse intervalo. |   
|allocated_storage_in_megabytes|**float**|A quantidade de espaço de arquivo formatado em MB disponibilizada para armazenar dados de banco de dados. O espaço de arquivo formatado também é conhecido como espaço de dados alocado.  Para obter mais informações, consulte: [Gerenciamento de espaço de arquivo no banco de BD SQL](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|
  
> [!TIP]  
>  Para obter mais contexto sobre esses limites e camadas de serviço, consulte as [camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)de tópicos.  
    
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao banco de dados **mestre** virtual.  
  
## <a name="remarks"></a>Comentários  
 Os dados retornados por **Sys. resource_stats** são expressos como uma porcentagem dos limites máximos permitidos para a camada de serviço/nível de desempenho que você está executando.  
  
 Quando um banco de dados é membro de um pool elástico, as estatísticas de recursos apresentadas como valores percentuais são expressas como a porcentagem do limite máximo para os bancos de dados, conforme definido na configuração do pool elástico.  
  
 Para obter uma exibição mais granular desses dados, use a exibição de gerenciamento dinâmico **Sys. dm _db_resource_stats** em um banco de dados de usuário. Essa visualização captura dados a cada 15 segundos e mantém dados históricos por 1 hora.  Para obter mais informações, consulte [Sys. dm &#40;_Db_resource_stats banco de&#41;dados SQL do Azure](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os bancos de dados que estão com média de pelo menos 80% de utilização de computação durante a última semana.  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>Consulte também  
 [Camadas de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Limites e capacidades da camada de serviço](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
