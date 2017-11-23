---
title: "Criar serviço (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SERVICE_TSQL
- SERVICE
- CREATE SERVICE
- SERVICE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- services [Service Broker], creating
- CREATE SERVICE statement
- contracts [Service Broker], service creation
ms.assetid: fb804fa2-48eb-4878-a12f-4e0d5f4bc9e3
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5298494b6c3be0685df771f6d86e11c7b788d002
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="create-service-transact-sql"></a>CREATE SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um serviço novo. Um serviço [!INCLUDE[ssSB](../../includes/sssb-md.md)] é um nome de uma tarefa específica ou conjunto de tarefas. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa o nome do serviço para rotear mensagens, entregar mensagens para a fila correta dentro de um banco de dados e impor o contrato para uma conversa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE SERVICE service_name  
   [ AUTHORIZATION owner_name ]  
   ON QUEUE [ schema_name. ]queue_name  
   [ ( contract_name | [DEFAULT][ ,...n ] ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SERVICE_NAME*  
 É o nome do serviço a ser criado. Um novo serviço é criado no banco de dados atual e é de propriedade do principal especificado na cláusula AUTHORIZATION. Os nomes de servidor, banco de dados e esquema não podem ser especificados. O *service_name* deve ser um válido **sysname**.  
  
> [!NOTE]  
>  Não crie um serviço que usa a palavra-chave ANY para o *service_name*. Quando você especifica ANY para um nome de serviço em CREATE BROLER PRIORITY, a prioridade é considerada para todos os serviços. Não fica limitada a um serviço cujo nome é ANY.  
  
 AUTORIZAÇÃO *owner_name*  
 Define o proprietário do serviço para o usuário ou função de banco de dados especificados. Quando o usuário atual é **dbo** ou **sa**, *owner_name* pode ser o nome de qualquer usuário ou função válida. Caso contrário, *owner_name* deve ser o nome do usuário atual, o nome de um usuário que o usuário atual tenha a permissão IMPERSONATE ou o nome de uma função ao qual pertence o usuário atual.  
  
 FILA de ON [ *schema_name***.** ] *nome_da_fila*  
 Especifica a fila que recebe as mensagens para o serviço. A fila deve existir no mesmo banco de dados assim como o serviço. Se nenhum *schema_name* for fornecido, o esquema é o esquema padrão para o usuário que executa a instrução.  
  
 *contract_name*  
 Especifica um contrato para o qual este serviço pode ser um destino. Os programas de serviço iniciam conversas para este serviço usando os contratos especificados. Se nenhum contrato for especificado, o serviço só poderá iniciar conversas.  
  
 **[**PADRÃO**]**  
 Especifica que o serviço pode ser um destino para as conversas que seguem o contrato DEFAULT. No contexto desta cláusula, DEFAULT não é uma palavra-chave e deve ser delimitado como um identificador. O contrato DEFAULT permite que ambos os lados da conversa enviem mensagens de tipo de mensagem DEFAULT. Mensagem tipo DEFAULT usa validação NONE.  
  
## <a name="remarks"></a>Comentários  
 Um serviço expõe a funcionalidade fornecida pelos contratos com os quais está associado, de forma que eles possam ser usados por outros serviços. A instrução CREATE SERVICE especifica os contratos para os quais este serviço é o destino. Um serviço só pode ser um destino para conversas que usam os contratos especificados pelo serviço. Um serviço que não especifica nenhum contrato, não expõe nenhuma funcionalidade a outros serviços.  
  
 As conversas iniciadas deste serviço podem usar qualquer contrato. Você criará um serviço sem especificar contratos quando o serviço só for iniciar conversas.  
  
 Quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] aceita uma nova conversa de um serviço remoto, o nome do serviço de destino determina a fila em que o broker coloca as mensagens na conversa.  
  
## <a name="permissions"></a>Permissões  
 Padrões de permissão para criar um serviço aos membros do **db_ddladmin** ou **db_owner** funções de banco de dados fixas e **sysadmin** função de servidor fixa. O usuário que executa a instrução CREATE SERVICE deve ter permissão de REFERENCES na fila e todos os contratos especificados.  
  
 Permissão REFERENCES para um serviço padrão é o proprietário do serviço, os membros do **db_ddladmin** ou **db_owner** fixa de funções de banco de dados e os membros do **sysadmin** função de servidor fixa. Permissões de envio para um padrão de serviço para o proprietário do serviço, os membros do **db_owner** fixo de função de banco de dados e membros do **sysadmin** função de servidor fixa.  
  
 Um serviço pode não ser um objeto temporário. Serviço de nomes que começam com  **#**  são permitidos, mas são objetos permanentes.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-service-with-one-contract"></a>A. Criando um serviço com um contrato  
 O exemplo seguinte cria o serviço `//Adventure-Works.com/Expenses` na fila `ExpenseQueue` no esquema `dbo`. Diálogos que tenham esse serviço como destino devem seguir o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`.  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE [dbo].[ExpenseQueue]  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="b-creating-a-service-with-multiple-contracts"></a>B. Criando um serviço com vários contratos  
 O exemplo a seguir cria o serviço `//Adventure-Works.com/Expenses` na fila `ExpenseQueue`. Diálogos que tenham esse serviço como destino devem seguir o contrato `//Adventure-Works.com/Expenses/ExpenseSubmission` ou o contrato `//Adventure-Works.com/Expenses/ExpenseProcessing`.  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission],  
     [//Adventure-Works.com/Expenses/ExpenseProcessing]) ;  
```  
  
### <a name="c-creating-a-service-with-no-contracts"></a>C. Criando um serviço sem contratos  
 O exemplo a seguir cria o serviço `//Adventure-Works.com/Expenses on the ExpenseQueue` fila. Esse serviço não tem nenhuma informação de contrato. Portanto, o serviço só poderá ser o iniciador de um diálogo.  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER SERVICE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [Remover serviço &#40; Transact-SQL &#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
