---
title: sys. database_connection_stats (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_connection_stats
- database_connection_stats
- database_connection_stats_TSQL
- sys.database_connection_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_connection_stats
- database_connection_stats
ms.assetid: 5c8cece0-63b0-4dee-8db7-6b43d94027ec
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 86e8c5af0a2b992a1167e23497a419e0f90abe56
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55421103"
---
# <a name="sysdatabaseconnectionstats-azure-sql-database"></a>sys.database_connection_stats (Banco de Dados SQL do Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contém estatísticas para [!INCLUDE[ssSDS](../../includes/sssds-md.md)] banco de dados **conectividade** eventos, fornecendo uma visão geral de falhas e êxitos de conexão de banco de dados. Para obter mais informações sobre eventos de conectividade, consulte tipos de evento em [sys. event_log &#40;banco de dados SQL&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md).  
  
|Estatística|Tipo|Descrição|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|Nome do banco de dados.|  
|**start_time**|**datetime2**|Data e hora UTC do início do intervalo de agregação. A hora é sempre um múltiplo de 5 minutos. Por exemplo:<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|Data e hora UTC do término do intervalo de agregação. **End_time** é sempre exatamente 5 minutos mais tarde do que o correspondente **start_time** na mesma linha.|  
|**success_count**|**int**|Número de conexões bem-sucedidas.|  
|**total_failure_count**|**int**|Número total de conexões com falha. Essa é a soma das **connection_failure_count**, **terminated_connection_count**, e **throttled_connection_count**e não inclui eventos de deadlock.|  
|**connection_failure_count**|**int**|Número de falhas de logon.|  
|**terminated_connection_count**|**int**|**_Aplicável somente para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11._**<br /><br /> Número de conexões encerradas.|  
|**throttled_connection_count**|**int**|**_Aplicável somente para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11._**<br /><br /> Número de conexões aceleradas.|  
  
## <a name="remarks"></a>Comentários  
  
### <a name="event-aggregation"></a>Agregação de eventos

 As informações de evento para esta exibição são coletadas e agregadas em intervalos de 5 minutos. As colunas de contagem representam o número de vezes que um evento de conectividade determinado ocorreu para um banco de dados específico dentro de um intervalo de tempo.  
  
 Por exemplo, se um usuário não puder se conectar ao banco de dados Database1 sete vezes entre 11:00 e 11:05 em 5/2/2012 (UTC), essas informações estarão disponíveis em uma única linha nesta exibição:  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
### <a name="interval-starttime-and-endtime"></a>start_time e end_time do intervalo

 Um evento é incluído em um intervalo de agregação quando ocorre o evento *na* ou _depois_**start_time** e _antes_  **end_time** para esse intervalo. Por exemplo, um evento que ocorre exatamente em `2012-10-30 19:25:00.0000000` seria incluído somente no segundo intervalo mostrado abaixo:  
  
```  
  
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```  
  
### <a name="data-updates"></a>Atualizações de dados

 Os dados nessa exibição são acumulados com o passar do tempo. Normalmente, os dados são acumulados em uma hora de início do intervalo de agregação, mas pode levar até um máximo de 24 horas para que todos os dados apareçam na exibição. Durante esse período, as informações em uma única linha podem ser atualizadas periodicamente.  
  
### <a name="data-retention"></a>Retenção de Dados

 Os dados nessa exibição são retidos por um máximo de 30 dias, ou possivelmente menor dependendo do número de bancos de dados e o número de eventos exclusivos que cada banco de dados gera. Para reter essas informações por um período mais longo, copie os dados em um banco de dados separado. Depois que você faz uma cópia inicial da exibição, as linhas na exibição podem ser atualizadas à medida que os dados são acumulados. Para manter sua cópia de dados atualizada, periodicamente faça uma verificação da tabela das linhas para procurar um aumento na contagem de eventos de linhas existentes e identificar novas linhas (você pode identificar linhas exclusivas usando a hora de início e de término) e, em seguida, atualize sua cópia dos dados com essas alterações.  
  
### <a name="errors-not-included"></a>Erros não incluídos

 Essa exibição não pode incluir todas as informações de conexão e erro:  
  
- Essa exibição não inclui todos os [!INCLUDE[ssSDS](../../includes/sssds-md.md)] erros que podem ocorrer, somente os especificados em tipos de evento no banco de dados [sys. event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md).  
  
- Se não houver uma falha do computador dentro do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] datacenter, uma pequena quantidade de dados pode estar falta na tabela de evento.  
  
- Se um endereço IP tiver sido bloqueado com DoSGuard, os eventos da tentativa de conexão desse endereço IP não poderão ser coletados e não aparecerão nessa exibição.  
  
## <a name="permissions"></a>Permissões

 Os usuários com permissão para acessar o **mestre** banco de dados têm acesso somente leitura a essa exibição.  
  
## <a name="example"></a>Exemplo

 O exemplo a seguir mostra uma consulta de **sys. database_connection_stats** para retornar um resumo das conexões de banco de dados que ocorreram entre meio-dia em 9/25/2011 e meio-dia em 9/28/2011 (UTC). Por padrão, os resultados da consulta são classificados por **start_time** (ordem crescente).  
  
```sql
SELECT *  
FROM sys.database_connection_stats
WHERE start_time>='2011-09-25:12:00:00' and end_time<='2011-09-28 12:00:00';  
```  

## <a name="see-also"></a>Consulte também

 [Solução de problemas do Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee730906.aspx)  
  
  
