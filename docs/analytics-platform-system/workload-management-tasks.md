---
title: Tarefas de gerenciamento de carga de trabalho
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/12/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.openlocfilehash: 0a9c3ffd4768d78a4063ad40f7903dfe00b647e5
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="workload-management-tasks"></a>Tarefas de gerenciamento de carga de trabalho

## <a name="view-login-members-of-each-resource-class"></a>Exibir membros do logon de cada classe de recurso
Descreve como exibir os membros de logon de cada função de servidor de classe do recurso SQL Server PDW. Use esta consulta para descobrir a classe de recursos permitido para solicitações enviadas por cada logon.  
  
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
  
Se um logon não estiver nesta lista, suas solicitações receberá os recursos padrão. Se um logon for membro de mais de uma classe de recurso, a classe maior tem precedência.  
  
As alocações de recurso são listadas no [gerenciamento de carga de trabalho](workload-management.md) tópico.  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>Os recursos do sistema alocados a uma solicitação de alteração
Descreve como descobrir quais recursos classe uma solicitação de PDW do SQL Server está sendo executado e, em seguida, como alterar os recursos do sistema para essa solicitação. Alterar os recursos de uma solicitação exige a alteração na associação de classe de recursos de logon enviando a solicitação, usando o [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) instrução.  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>Etapa 1: Determine a classe de recurso para o logon que está executando a solicitação.  
Esta consulta exibe os logons que são membros de associações de função de servidor de classe de recurso. Há três classes de recursos, **mediumrc**, **largerc**, e **xlargerc**.  
  
> [!IMPORTANT]  
> Essa consulta deve ser executada por um logon que tenha **CONTROL SERVER** permissão. Se executado por um logon sem **CONTROL SERVER** permissão, essa consulta retorna apenas as associações de função para o logon atual.  
  
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
  
Se não existem logons que são membros de uma função de servidor de classe de recurso, a tabela resultante estará vazia. Nesse caso, se a consulta retornar um logon denominado Ching, em seguida, quando Ching envia uma solicitação, a solicitação receberá os recursos de sistema padrão, menor do que os recursos de sistema de classe de recurso. Se um logon for membro de mais de uma classe de recurso, a classe maior tem precedência.  
  
Para obter uma lista de alocações de recursos para cada classe de recurso, consulte [gerenciamento de carga de trabalho](workload-management.md) tópico.  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>Etapa 2: Executar a solicitação em um logon com membros da classe de recurso diferente  
Há duas maneiras de executar uma solicitação com qualquer um dos recursos do sistema maior ou menor:  
  
-   Execute a solicitação em um logon diferente que seja membro de uma classe de recurso maior ou menor.  
  
-   Adicione o logon necessário para uma das funções de classe do recurso. Escolha esta opção com cuidado; alterar a classe de recurso para o logon alterará o nível de recursos de sistema para todas as solicitações enviadas pelo logon.  
  
Suponha que Ching é um membro da função de servidor largerc. O exemplo a seguir mostra como adicionar logon Ching à função de servidor xlargerc.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching agora é membro do largerc e as funções de servidor xlargerc. Quando Ching envia solicitações, as solicitações recebem os recursos do sistema xlargerc.  
  
O exemplo a seguir move Ching de volta à função de servidor mediumrc.  Para fazer isso, ela deve ser removida do xlargerc e largerc funções de servidor e adicionada à função de servidor mediumrc.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching agora é um membro da função de servidor mediumrc.  O exemplo a seguir altera Ching com os recursos de sistema padrão para suas solicitações.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
Para obter mais informações sobre como alterar a associação de função de classe de recurso, consulte [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md).  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>Alterar um logon para os recursos de sistema padrão para suas solicitações
Descreve como alterar as alocações de recursos de sistema atribuídas a um logon do SQL Server PDW para os valores padrão. Isso afeta os recursos de sistema do SQL Server PDW atribui a solicitações enviadas pelo logon.  
  
Para obter descrições de classe de recurso, consulte [gerenciamento de carga de trabalho](workload-management.md)  
  
Quando um logon não é um membro da função de servidor de classe qualquer recurso, solicitações enviadas pelo logon receberá o valor padrão de recursos do sistema.  
  
Suponha que o logon Matt atualmente é um membro de todas as funções de servidor de classe de recurso e deseja reverter para ter suas solicitações de receber apenas os recursos padrão.  O exemplo a seguir atribui os recursos padrão para solicitações de Matt cancelando sua associação de todas as funções de servidor de classe de recurso de três.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>Exibir que o número de Slots de simultaneidade necessária uma espera de solicitação
Descreve como descobrir o número de slots necessárias por uma solicitação que está aguardando para serem executados no SQL Server PDW de simultaneidade.  
  
Para obter mais informações, consulte [gerenciamento de carga de trabalho](workload-management.md).  
  
Uma solicitação pode estar esperando muito tempo sem sendo executada. Uma das maneiras de solucionar esse problema é examinar o número de slots de simultaneidade que precisa a solicitação.  O exemplo a seguir mostra o número de slots de simultaneidade necessária para cada solicitação de espera.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>Consulte também  
[Gerenciamento de carga de trabalho](workload-management.md)  
  
