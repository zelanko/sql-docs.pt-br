---
title: Tarefas de gerenciamento de carga de trabalho
description: Tarefas de gerenciamento de carga de trabalho no Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 88d95eb0a2e0805930cb5f01f5af05b8fc6b3f2e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399411"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Tarefas de gerenciamento de carga de trabalho no Analytics Platform System
Tarefas de gerenciamento de carga de trabalho no Analytics Platform System.

## <a name="view-login-members-of-each-resource-class"></a>Exibir membros de logon de cada classe de recurso
Descreve como exibir os membros de logon de cada função de servidor da classe de recurso no SQL Server PDW. Use essa consulta para descobrir a classe de recursos permitidos para solicitações enviadas por cada logon.  
  
Para obter descrições de classe de recurso, consulte [Gerenciamento de carga de trabalho](workload-management.md).  
  
Essa consulta exibe a lista de associação para cada classe de recurso. Há três classes de recursos, mediumrc, largerc e xlargerc.  
  
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
  
Se um logon não estiver nessa lista, suas solicitações receberão os recursos padrão. Se um logon for membro de mais de uma classe de recurso, a maior classe terá precedência.  
  
As alocações de recursos são listadas no [Gerenciamento de carga de trabalho](workload-management.md).  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>Alterar os recursos do sistema alocados para uma solicitação
Descreve como descobrir em qual classe de recurso uma SQL Server PDW solicitação está sendo executada e como alterar os recursos do sistema para essa solicitação. A alteração dos recursos de uma solicitação requer a alteração da Associação de classe de recurso do logon que envia a solicitação, usando a instrução [ALTER Server Role](../t-sql/statements/alter-server-role-transact-sql.md) .  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>Etapa 1: determinar a classe de recurso para o logon que está executando a solicitação.  
Essa consulta exibe os logons que são membros das associações de função de servidor classe de recurso. Há três classes de recursos, **mediumrc**, **largerc**e **xlargerc**.  
  
> [!IMPORTANT]  
> Essa consulta deve ser executada por um logon com a permissão **Control Server** . Se executado por um logon sem permissão **Control Server** , essa consulta retornará apenas as associações de função para o logon atual.  
  
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
  
Se não houver logons que sejam membros de uma função de servidor de classe de recurso, a tabela resultante estará vazia. Nesse caso, se a consulta retornar um logon chamado Ching, quando o Ching enviar uma solicitação, a solicitação receberá os recursos padrão do sistema, que são menores do que os recursos do sistema da classe de recurso. Se um logon for membro de mais de uma classe de recurso, a maior classe terá precedência.  
  
Para obter uma lista de alocações de recursos para cada classe de recurso, consulte [Gerenciamento de carga de trabalho](workload-management.md).  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>Etapa 2: executar a solicitação em um logon com associação de classe de recurso diferente  
Há duas maneiras de executar uma solicitação com recursos maiores ou menores do sistema:  
  
-   Execute a solicitação em um logon diferente que seja membro de uma classe de recursos maior ou menor.  
  
-   Adicione o logon necessário a uma das funções de classe de recurso. Escolha essa opção com cuidado; alterar a classe de recurso para o logon alterará o nível de recurso do sistema para todas as solicitações enviadas pelo logon.  
  
Suponha que Ching seja membro da função de servidor largerc. O exemplo a seguir mostra como adicionar Ching de logon à função de servidor xlargerc.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching agora é um membro das funções de servidor largerc e xlargerc. Quando o Ching envia solicitações, as solicitações receberão os recursos do sistema xlargerc.  
  
O exemplo a seguir move Ching de volta para a função de servidor mediumrc.  Para alterar para a nova função, o logon deve ser removido das funções de servidor xlargerc e largerc e adicionado à função de servidor mediumrc.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching agora é um membro da função de servidor mediumrc.  O exemplo a seguir altera Ching para ter os recursos de sistema padrão para solicitações.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
Para obter mais informações sobre como alterar a associação de função de classe de recurso, consulte [ALTER Server Role](../t-sql/statements/alter-server-role-transact-sql.md).  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>Alterar um logon para os recursos padrão do sistema para suas solicitações
Descreve como alterar as alocações de recursos do sistema atribuídas a um SQL Server PDW logon para as quantidades padrão. 
  
Para obter descrições de classe de recurso, consulte [Gerenciamento de carga de trabalho](workload-management.md)  
  
Quando um logon não for um membro de qualquer função de servidor da classe de recurso, as solicitações enviadas pelo logon receberão a quantidade padrão de recursos do sistema.  
  
Suponha que o logon Matt seja atualmente um membro de todas as funções de servidor da classe de recurso e queira reverter para que as solicitações recebam apenas os recursos padrão.  O exemplo a seguir atribui os recursos padrão às solicitações de Matt removendo sua associação de todas as três funções de servidor da classe de recurso.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>Exibir o número de Slots de simultaneidade necessários para uma solicitação em espera
Descreve como descobrir o número de Slots de simultaneidade necessários para uma solicitação que está aguardando para ser executada em SQL Server PDW.  
  
Para obter mais informações, consulte [Gerenciamento de carga de trabalho](workload-management.md).  
  
Uma solicitação pode estar aguardando muito tempo sem ser executada. Uma das maneiras de solucionar problemas da solicitação é examinar o número de Slots de simultaneidade necessários para a solicitação.  O exemplo a seguir mostra o número de Slots de simultaneidade necessários para cada solicitação em espera.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciamento da Carga de Trabalho](workload-management.md)  
  
