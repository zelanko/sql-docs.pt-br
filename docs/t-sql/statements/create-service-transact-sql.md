---
title: CREATE SERVICE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_SERVICE_TSQL
- SERVICE
- CREATE SERVICE
- SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- services [Service Broker], creating
- CREATE SERVICE statement
- contracts [Service Broker], service creation
ms.assetid: fb804fa2-48eb-4878-a12f-4e0d5f4bc9e3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 761a04baca38ee1301c8f51d8b69564f409fac1e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70745394"
---
# <a name="create-service-transact-sql"></a>CREATE SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Cria um serviço novo. Um serviço [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um nome de uma tarefa específica ou conjunto de tarefas. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa o nome do serviço para rotear mensagens, entregar mensagens para a fila correta dentro de um banco de dados e impor o contrato para uma conversa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE SERVICE service_name  
   [ AUTHORIZATION owner_name ]  
   ON QUEUE [ schema_name. ]queue_name  
   [ ( contract_name | [DEFAULT][ ,...n ] ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *service_name*  
 É o nome do serviço a ser criado. Um novo serviço é criado no banco de dados atual e é de propriedade do principal especificado na cláusula AUTHORIZATION. Os nomes de servidor, banco de dados e esquema não podem ser especificados. O *service_name* deve ser um **sysname** válido.  
  
> [!NOTE]  
> Não crie um serviço que usa a palavra-chave ANY para o *contract_name*. Quando você especifica `ANY` para um nome de serviço em `CREATE BROKER PRIORITY`, a prioridade é considerada para todos os serviços. Não fica limitada a um serviço cujo nome é ANY.  
  
 AUTHORIZATION *owner_name*  
 Define o proprietário do serviço para o usuário ou função de banco de dados especificados. Quando o usuário atual é **dbo** ou **sa**, *owner_name* pode ser o nome de qualquer usuário ou função válida. Caso contrário, *owner_name* deve ser o nome do usuário atual, o nome de um usuário para o qual o usuário atual tenha a permissão IMPERSONATE ou o nome de uma função à qual o usuário atual pertença.  
  
 ON QUEUE [ _schema_name_ **.** ] *queue_name*  
 Especifica a fila que recebe as mensagens para o serviço. A fila deve existir no mesmo banco de dados assim como o serviço. Se nenhum *schema_name* for fornecido, o esquema será o esquema padrão para o usuário que executa a instrução.  
  
 *contract_name*  
 Especifica um contrato para o qual este serviço pode ser um destino. Os programas de serviço iniciam conversas para este serviço usando os contratos especificados. Se nenhum contrato for especificado, o serviço só poderá iniciar conversas.  
  
 **[** DEFAULT **]**  
 Especifica que o serviço pode ser um destino para as conversas que seguem o contrato DEFAULT. No contexto desta cláusula, DEFAULT não é uma palavra-chave e deve ser delimitado como um identificador. O contrato DEFAULT permite que ambos os lados da conversa enviem mensagens de tipo de mensagem DEFAULT. Mensagem tipo DEFAULT usa validação NONE.  
  
## <a name="remarks"></a>Comentários  
 Um serviço expõe a funcionalidade fornecida pelos contratos com os quais está associado, de forma que eles possam ser usados por outros serviços. A instrução `CREATE SERVICE` especifica os contratos para os quais este serviço é o destino. Um serviço só pode ser um destino para conversas que usam os contratos especificados pelo serviço. Um serviço que não especifica nenhum contrato, não expõe nenhuma funcionalidade a outros serviços.  
  
 As conversas iniciadas deste serviço podem usar qualquer contrato. Você criará um serviço sem especificar contratos quando o serviço só for iniciar conversas.  
  
 Quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] aceita uma nova conversa de um serviço remoto, o nome do serviço de destino determina a fila em que o broker coloca as mensagens na conversa.  
  
## <a name="permissions"></a>Permissões  
 A permissão para criar um serviço tem como padrão os membros das funções de banco de dados fixa `db_ddladmin` ou `db_owner`, ou a função de servidor fixa `sysadmin`. O usuário que executa a instrução `CREATE SERVICE` deve ter permissão `REFERENCES` na fila e todos os contratos especificados.  
  
 A permissão `REFERENCES` para um serviço assume como padrão o proprietário do serviço, os membros das funções de banco de dados fixas `db_ddladmin` ou `db_owner`, ou os membros da função de servidor fixa `sysadmin`. As permissões `SEND` para um serviço assumem como padrão o proprietário do serviço, os membros da função de banco de dados fixa `db_owner` ou os membros da função de servidor fixa `sysadmin`.  
  
 Um serviço pode não ser um objeto temporário. Nomes de serviços que começam com **#** são permitidos, mas são objetos permanentes.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-service-with-one-contract"></a>a. Criando um serviço com um contrato  
 O exemplo seguinte cria o serviço `//Adventure-Works.com/Expenses` na fila `ExpenseQueue` no esquema `dbo`. Diálogos que tenham esse serviço como destino devem seguir o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`.  
  
```sql  
CREATE SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE [dbo].[ExpenseQueue]  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="b-creating-a-service-with-multiple-contracts"></a>B. Criando um serviço com vários contratos  
 O exemplo a seguir cria o serviço `//Adventure-Works.com/Expenses` na fila `ExpenseQueue`. Diálogos que tenham esse serviço como destino devem seguir o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission` ou o contrato `//Adventure-Works.com/Expenses/ExpenseProcessing`.  
  
```sql  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission],  
     [//Adventure-Works.com/Expenses/ExpenseProcessing]) ;  
```  
  
### <a name="c-creating-a-service-with-no-contracts"></a>C. Criando um serviço sem contratos  
 O exemplo a seguir cria a fila `//Adventure-Works.com/Expenses on the ExpenseQueue` do serviço. Esse serviço não tem nenhuma informação de contrato. Portanto, o serviço só poderá ser o iniciador de um diálogo.  
  
```sql  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
