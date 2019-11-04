---
title: CREATE CONTRACT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONTRACT_TSQL
- CREATE_CONTRACT_TSQL
- CREATE CONTRACT
- CONTRACT
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE CONTRACT statement
- contracts [Service Broker], creating
- message types [Service Broker], contracts
ms.assetid: 494cbfa6-8e93-4161-a64d-90d681915211
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2e7dbdb8ea5a422b91f290478eeca4dfc9b21cbc
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064644"
---
# <a name="create-contract-transact-sql"></a>CREATE CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um novo contrato. Um contrato define os tipos de mensagem que são usados em uma conversa do [!INCLUDE[ssSB](../../includes/sssb-md.md)] e também determina qual lado da conversa pode enviar mensagens daquele tipo. Cada conversa segue um contrato. O serviço iniciador especifica o contrato para a conversa quando esta inicia. O serviço de destino especifica os contratos para os quais o serviço de destino aceita conversas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE CONTRACT contract_name  
   [ AUTHORIZATION owner_name ]  
      (  {   { message_type_name | [ DEFAULT ] }  
          SENT BY { INITIATOR | TARGET | ANY }   
       } [ ,...n] )   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *contract_name*  
 É o nome do contrato a ser criado. Um novo contrato é criado no banco de dados atual e é de propriedade da entidade especificada na cláusula AUTHORIZATION. Os nomes de servidor, banco de dados e esquema não podem ser especificados. O *contract_name* pode ter até 128 caracteres.  
  
> [!NOTE]  
>  Não crie um contrato que usa a palavra-chave ANY para o *contract_name*. Quando você especifica ANY para um nome de serviço em CREATE BROKER PRIORITY, a prioridade é considerada para todos os contratos. Ela não fica limitada a um contrato cujo nome é ANY.  
  
 AUTHORIZATION *owner_name*  
 Define o proprietário do contrato para o usuário ou a função de banco de dados especificada. Quando o usuário atual é **dbo** ou **sa**, *owner_name* pode ser o nome de qualquer usuário ou função válida. Caso contrário, *owner_name* deverá ser o nome do usuário atual, o nome de um usuário para o qual o usuário atual tem permissões de representação ou o nome de uma função à qual o usuário atual pertence. Quando esta cláusula é omitida, o contrato pertence ao usuário atual.  
  
 *message_type_name*  
 É o nome de um tipo de mensagem a ser incluído como parte do contrato.  
  
 SENT BY  
 Especifica qual ponto de extremidade pode enviar uma mensagem do tipo indicado. Os contratos documentam as mensagens que os serviços podem usar para ter conversas específicas. Cada conversa contém dois pontos de extremidade: o ponto do *iniciador*, o serviço que iniciou a conversa, e o ponto de *destino*, o serviço que o iniciador está contatando.  
  
 INITIATOR  
 Indica que somente o iniciador da conversa pode enviar mensagens do tipo especificado. Um serviço que inicia uma conversa é chamado de *iniciador* da conversa.  
  
 TARGET  
 Indica que somente o destino da conversa pode enviar mensagens do tipo especificado. Um serviço que aceita uma conversa iniciada por outro serviço é chamado de *destino* da conversa.  
  
 ANY  
 Indica que as mensagens deste tipo podem ser enviadas pelo iniciador e pelo destino.  
  
 [ DEFAULT ]  
 Indica que este contrato dá suporte a mensagens do tipo padrão. Por padrão, todos os bancos de dados contêm um tipo de mensagem denominado DEFAULT. Esse tipo de mensagem usa uma validação de NONE. No contexto desta cláusula, DEFAULT não é uma palavra-chave e deve ser delimitado como um identificador. O Microsoft SQL Server também fornece um contrato DEFAULT que especifica o tipo de mensagem DEFAULT.  
  
## <a name="remarks"></a>Remarks  
 A ordem de tipos de mensagem no contrato não é significativa. Depois que o destino recebe a primeira mensagem, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] permite que cada lado da conversa envie qualquer mensagem permitida para aquele lado a qualquer hora. Por exemplo, se o iniciador da conversa puder enviar o tipo de mensagem **//Adventure-Works.com/Expenses/SubmitExpense**, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] permitirá que o iniciador envie qualquer quantidade de mensagens **SubmitExpense** durante a conversa.  
  
 Os tipos e as direções de mensagens não podem ser alterados em um contrato. Para alterar a AUTHORIZATION para um contrato, use a instrução ALTER AUTHORIZATION.  
  
 Um contrato deve permitir que o iniciador envie uma mensagem. A instrução CREATE CONTRACT falha quando o contrato não contém pelo menos um tipo de mensagem que seja SENT BY ANY ou SENT BY INITIATOR.  
  
 Independentemente do contrato, um serviço pode sempre receber os tipos de mensagem `https://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`, `https://schemas.microsoft.com/SQL/ServiceBroker/Error` e `https://schemas.microsoft.com/SQL/ServiceBroker/EndDialog`. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa esses tipos de mensagem para mensagens de sistema enviadas ao aplicativo.  
  
 Um contrato não pode ser um objeto temporário. Os nomes de contrato que começam com # são permitidos, mas são objetos permanentes.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros das funções de banco de dados fixas **db_ddladmin** ou **db_owner** ou da função de servidor fixa **sysadmin** podem criar contratos.  
  
 Por padrão, o proprietário do contrato, os membros das funções de banco de dados fixas **db_ddladmin** ou **db_owner** e os membros da função de servidor fixa **sysadmin** têm a permissão REFERENCES em um contrato.  
  
 O usuário que executa a instrução CREATE CONTRACT deve ter a permissão REFERENCES em todos os tipos de mensagem especificados.  
  
## <a name="examples"></a>Exemplos  
 **A. Criando um contrato**  
  
 O exemplo a seguir cria um contrato de reembolso de despesas com base em três tipos de mensagem.  
  
```sql  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE           
    [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
    VALIDATION= WELL_FORMED_XML ;           
  
CREATE CONTRACT            
    [//Adventure-Works.com/Expenses/ExpenseSubmission]           
    ( [//Adventure-Works.com/Expenses/SubmitExpense]           
          SENT BY INITIATOR,           
      [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
          SENT BY TARGET,           
      [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
          SENT BY TARGET           
    ) ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DROP CONTRACT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-contract-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
