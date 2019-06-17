---
title: Tarefas de gerenciamento de carga de trabalho - Analytics Platform System | Microsoft Docs
description: Tarefas de gerenciamento de carga de trabalho no Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8e538b96c482a6a16fffcfdac197e62885426b52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63243796"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Tarefas de gerenciamento de carga de trabalho no Analytics Platform System
Tarefas de gerenciamento de carga de trabalho no Analytics Platform System.

## <a name="view-login-members-of-each-resource-class"></a>Exibir membros de logon de cada classe de recurso
Descreve como exibir os membros de logon de cada função de servidor de classe de recurso no SQL Server PDW. Use esta consulta para descobrir a classe de recursos permitidos para as solicitações enviadas por cada logon.  
  
Para obter descrições de classe de recurso, consulte [gerenciamento de carga de trabalho](workload-management.md).  
  
Esta consulta exibe a lista de membros de cada classe de recurso. Há três classes de recursos, mediumrc, largerc e xlargerc.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  ( l.[type] = 'S' OR l.[type] = 'U' OR l.[type] = 'G' )  
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
```  
  
Se um logon não estiver nessa lista, suas solicitações receberá os recursos padrão. Se um logon for membro de mais de uma classe de recurso, a classe de maior tem precedência.  
  
Alocações de recursos são listadas na [gerenciamento de carga de trabalho](workload-management.md).  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>Os recursos do sistema alocados a uma solicitação de alteração
Descreve como descobrir quais recursos uma solicitação de PDW do SQL Server estiver em execução em classe e, em seguida, como alterar os recursos do sistema para a solicitação. Alterar os recursos para uma solicitação exige alterando os membros da classe de recurso de logon que está enviando a solicitação, usando o [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) instrução.  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>Etapa 1: Determine a classe de recurso para o logon executando a solicitação.  
Esta consulta exibe os logons que são membros de associações de função de servidor de classe de recurso. Há três classes de recursos, **mediumrc**, **largerc**, e **xlargerc**.  
  
> [!IMPORTANT]  
> Essa consulta deve ser executada por um logon que tenha **CONTROL SERVER** permissão. Se executada por um logon sem **CONTROL SERVER** permissão, essa consulta retorna apenas as associações de função para o logon atual.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  l.[type] = 'S'   
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
GO  
```  
  
Se não houver nenhum logon que são membros de uma função de servidor de classe de recurso, a tabela resultante estará vazia. Nesse caso, se a consulta retornar um logon denominado Ching, em seguida, quando a Ching envia uma solicitação, a solicitação receberá os recursos de sistema padrão, que são menores do que os recursos de sistema de classe de recurso. Se um logon for membro de mais de uma classe de recurso, a classe de maior tem precedência.  
  
Para obter uma lista de alocações de recursos para cada classe de recurso, consulte [gerenciamento de carga de trabalho](workload-management.md).  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>Etapa 2: Executar a solicitação em um logon com membros da classe de recursos diferente  
Há duas maneiras de executar uma solicitação com qualquer um dos recursos do sistema maiores ou menores:  
  
-   Execute a solicitação em um logon diferente que seja membro de uma classe de recurso maior ou menor.  
  
-   Adicione o logon necessário para uma das funções de classe de recurso. Escolha esta opção com cuidado; alterando a classe de recurso para o logon, você alterará o nível de recursos do sistema para todas as solicitações enviadas pelo logon.  
  
Suponha que a Ching é um membro da função de servidor largerc. O exemplo a seguir mostra como adicionar logon Ching à função de servidor xlargerc.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
A Ching agora é um membro do largerc e as funções de servidor xlargerc. Quando a Ching envia solicitações, as solicitações receberá os recursos do sistema xlargerc.  
  
O exemplo a seguir move a Ching de volta para a função de servidor mediumrc.  Para alterar para a nova função, o logon deve ser removido do funções de servidor largerc e xlargerc e adicionado à função de servidor mediumrc.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
A Ching agora é um membro da função de servidor mediumrc.  O exemplo a seguir altera a Ching tenha os recursos de sistema padrão para solicitações.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
Para obter mais informações sobre como alterar a associação de função de classe de recurso, consulte [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md).  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>Alterar um logon para os recursos de sistema padrão para suas solicitações
Descreve como alterar as alocações de recursos de sistema atribuídas a um logon do SQL Server PDW para os valores padrão. 
  
Para obter descrições de classe de recurso, consulte [gerenciamento de carga de trabalho](workload-management.md)  
  
Quando um logon não é um membro de qualquer função de servidor de classe de recurso, as solicitações enviadas pelo logon receberá a quantidade de recursos do sistema padrão.  
  
Suponha que o logon Matt atualmente é um membro de todas as funções de servidor de classe de recurso e deseja reverter para ter solicitações receber apenas os recursos padrão.  O exemplo a seguir atribui os recursos padrão para solicitações de Matt soltando sua associação a partir de todas as funções de servidor de classe de recurso de três.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>Exibir que o número de Slots de simultaneidade necessários para uma espera de solicitação
Descreve como descobrir o número de simultaneidade slots são necessários para uma solicitação que está esperando para ser executado no SQL Server PDW.  
  
Para obter mais informações, consulte [gerenciamento de carga de trabalho](workload-management.md).  
  
Uma solicitação pode estar aguardando muito tempo sem sendo executada. Uma das maneiras de solucionar problemas da solicitação é examinar o número de slots de simultaneidade, que a solicitação precisa.  O exemplo a seguir mostra o número de slots de simultaneidade necessária para cada solicitação de espera.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>Consulte também  
[Gerenciamento de carga de trabalho](workload-management.md)  
  
