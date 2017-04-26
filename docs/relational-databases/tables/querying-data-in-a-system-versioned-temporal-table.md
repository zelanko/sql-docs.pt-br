---
title: "Consultando dados em uma tabela temporal com controle de versão do sistema | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d358c2e-ebd8-4eb3-9bff-cfa598a39125
caps.latest.revision: 7
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9cc4156eccf9dd642e53ec2aeea967d9dcf016af
ms.lasthandoff: 04/11/2017

---
# <a name="querying-data-in-a-system-versioned-temporal-table"></a>Consultando dados em uma tabela temporal com controle da versão do sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Quando quiser obter o estado mais recente (real) dos dados em uma tabela temporal, você pode fazer uma consulta exatamente da mesma maneira que consulta uma tabela não temporal. Se as colunas PERIOD não estiverem ocultas, seus valores aparecerão em uma consulta SELECT \* . Se você especificou as colunas **PERIOD** como ocultas, seus valores não aparecerão na consulta SELECT \* . Quando as colunas **PERIOD** estiverem ocultas, faça referência às colunas **PERIOD** especificamente na cláusula SELECT para retornar os valores para essas colunas.  
  
 Para executar qualquer tipo de análise baseada em tempo, use a nova cláusula  **FOR SYSTEM_TIME** com quatro subcláusulas específicas temporais para consultar dados entre as tabelas atuais e de histórico. Para obter mais informações sobre essas cláusulas, consulte [Tabelas temporais](../../relational-databases/tables/temporal-tables.md) e [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
-   AS OF <data_hora>  
  
-   FROM <data_hora_inicial> TO <data_hora_final>  
  
-   BETWEEN <data_hora_inicial> AND <data_hora_final>  
  
-   CONTAINED IN (<sdata_hora_inicial> , <data_hora_final>)  
  
-   ALL  
  
 **FOR SYSTEM_TIME** pode ser especificada independentemente para cada tabela em uma consulta. Ela pode ser usada dentro de expressões de tabela comuns, funções com valor de tabela e procedimentos armazenados.  
  
## <a name="query-for-a-specific-time-using-the-as-of-sub-clause"></a>Consultar um horário específico usando a subcláusula AS OF  
 Use a subcláusula**AS OF** quando você precisar reconstruir o estado dos dados como eram em qualquer momento específico no passado.  Você pode reconstruir os dados com a precisão do tipo datetime2 que foi especificado nas definições da coluna **PERIOD** .    
A cláusula da subcláusula**AS OF** pode ser usada com literais constantes ou com variáveis, que permitem especificar dinamicamente a condição de tempo. Os valores fornecidos são interpretados como hora UTC.  
  
 Este primeiro exemplo retorna o estado da tabela dbo.Department A PARTIR de uma data específica no passado.  
  
```  
/*State of entire table AS OF specific date in the past*/   
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]   
FROM [dbo].[Department]   
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;  
  
```  
  
 Este segundo exemplo compara os valores entre dois pontos no tempo para um subconjunto de linhas.  
  
```  
DECLARE @ADayAgo datetime2   
SET @ADayAgo = DATEADD (day, -1, sysutcdatetime())   
/*Comparison between two points in time for subset of rows*/   
SELECT D_1_Ago.[DeptID], D.[DeptID],   
D_1_Ago.[DeptName], D.[DeptName],   
D_1_Ago.[SysStartTime], D.[SysStartTime],   
D_1_Ago.[SysEndTime], D.[SysEndTime]   
FROM [dbo].[Department] FOR SYSTEM_TIME AS OF @ADayAgo AS D_1_Ago   
JOIN [Department] AS D ON  D_1_Ago.[DeptID] = [D].[DeptID]    
AND D_1_Ago.[DeptID] BETWEEN 1 and 5 ;  
```  
  
### <a name="using-views-with-as-of-sub-clause-in-temporal-queries"></a>Usando exibições com a subcláusula AS OF em consultas temporais  
 Usar exibições é muito útil em cenários quando há necessidade de análise pontual complexa.   
Um exemplo comum é gerar um relatório de negócios hoje com os valores do mês anterior.   
Geralmente, os clientes têm um modelo de banco de dados normalizado que envolve muitas tabelas com relações de chave estrangeira. Responder à pergunta de como eram os dados desse modelo normalizado em um ponto no passado pode ser bastante desafiador, uma vez que todas as tabelas são alteradas de modo independente, em seu próprio ritmo.   
Nesse caso, a melhor opção é criar uma exibição e aplicar a subcláusula **AS OF** em toda a exibição. Usar essa abordagem permite a você separar a modelagem da camada de acesso a dados da análise pontual, pois o SQL Server aplicará a cláusula **AS OF** de modo transparente em todas as tabelas temporais que participam da definição da exibição. Além disso, você pode combinar tabelas temporais com não temporais na mesma exibição e **AS OF** será aplicada apenas às temporais. Se a exibição não fizer referência a pelo menos uma tabela temporal, a aplicação de cláusulas de consulta temporais a ela falhará com um erro.  
  
```  
/* Create view that joins three temporal tables: Department, CompanyLocation, LocationDepartments */   
CREATE VIEW [dbo].[vw_GetOrgChart]   
AS   
SELECT   
     [CompanyLocation].LocID  
   , [CompanyLocation].LocName  
   , [CompanyLocation].City  
   , [Department].DeptID  
   , [Department].DeptName    
FROM [dbo].[CompanyLocation]   
LEFT JOIN [dbo].[LocationDepartments]    
   ON [CompanyLocation].LocID = LocationDepartments.LocID   
LEFT JOIN [dbo].[Department]    
   ON LocationDepartments.DeptID = [Department].DeptID ;  
GO   
/* Querying view AS OF */   
SELECT * FROM [vw_GetOrgChart]   
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;  
  
```  
  
## <a name="query-for-changes-to-specific-rows-over-time"></a>Consultar alterações em linhas específicas ao longo do tempo  
 As subcláusulas temporais **FROM...TO**, **BETWEEN...AND** e **CONTAINED IN** são úteis quando você quer realizar uma auditoria de dados, ou seja, quando você precisar obter todas as alterações de histórico de uma linha específica na tabela atual.   
As duas primeiras subcláusulas retornam versões de linha que sobrepõem um período específico (isto é, aquelas que começaram antes de determinado período e foram encerradas depois dele), enquanto CONTAINED IN retorna apenas aquelas que existiram dentro de limites de período específicos.  
  
> [!IMPORTANT]  
>  Se você pesquisar somente versões de linha não atuais, é recomendável usar **CONTAINED IN** , pois ela funciona somente com a tabela de histórico e vai gerar o melhor desempenho de consulta. Use **ALL** quando precisar consultar dados do histórico e atuais sem nenhuma restrição.  
  
```  
/* Query using BETWEEN...AND sub-clause*/  
SELECT   
     [DeptID]  
   , [DeptName]  
   , [SysStartTime]  
   , [SysEndTime]  
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual   
FROM [dbo].[Department]   
FOR SYSTEM_TIME BETWEEN  '2015-01-01' AND '2015-12-31'   
WHERE DeptId = 1   
ORDER BY SysStartTime DESC;   
  
/*  Query using CONTAINED IN sub-clause */  
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]   
FROM [dbo].[Department]   
FOR SYSTEM_TIME CONTAINED IN ('2015-04-01', '2015-09-25')   
WHERE DeptId = 1   
ORDER BY SysStartTime DESC ;  
  
/*  Query using ALL sub-clause */   
SELECT    
     [DeptID]   
   , [DeptName]   
   , [SysStartTime]   
   , [SysEndTime]   
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual    
FROM [dbo].[Department] FOR SYSTEM_TIME ALL   
ORDER BY [DeptID], [SysStartTime] Desc  
  
```  
  
## <a name="did-this-article-help-you-were-listening"></a>Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Queryinging%20a%20System-Versioned%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Como criar uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Modificando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Alterando o esquema de uma tabela temporal com versão do sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [Parando o controle de versão do sistema de uma tabela temporal com versão do sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  

