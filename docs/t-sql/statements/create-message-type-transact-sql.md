---
description: CREATE MESSAGE TYPE (Transact-SQL)
title: CREATE MESSAGE TYPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_MESSAGE_TSQL
- MESSAGE_TSQL
- MESSAGE
- CREATE MESSAGE
- CREATE_MESSAGE_TYPE_TSQL
- MESSAGE TYPE
- MESSAGE_TYPE_TSQL
- CREATE MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- XML [Service Broker]
- validation [Service Broker]
- message types [Service Broker], creating
- empty messages [SQL Server]
- binary [SQL Server], message types
- CREATE MESSAGE TYPE statement
ms.assetid: 98fe0fff-1a2e-4ca2-b37f-83a06fdf098e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4966690508bdc48b73471519595b3010443128b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444841"
---
# <a name="create-message-type-transact-sql"></a>CREATE MESSAGE TYPE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Cria um novo tipo de mensagem. Um tipo de mensagem define o nome de uma mensagem e a validação que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] executa nas mensagens com esse nome. Os dois lados de uma conversa devem definir os mesmos tipos de mensagem.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CREATE MESSAGE TYPE message_type_name  
    [ AUTHORIZATION owner_name ]  
    [ VALIDATION = {  NONE  
                    | EMPTY   
                    | WELL_FORMED_XML  
                    | VALID_XML WITH SCHEMA COLLECTION schema_collection_name  
                   } ]  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *message_type_name*  
 É o nome do tipo de mensagem a ser criado. Um novo tipo de mensagem é criado no banco de dados atual e é de propriedade do principal especificado na cláusula AUTHORIZATION. Os nomes de servidor, banco de dados e esquema não podem ser especificados. O *message_type_name* pode ter até 128 caracteres.  
  
 AUTHORIZATION *owner_name*  
 Define o proprietário do tipo de mensagem como o usuário ou a função do banco de dados especificado. Quando o usuário atual é **dbo** ou **sa**, *owner_name* pode ser o nome de qualquer usuário ou função válida. Caso contrário, *owner_name* deverá ser o nome do usuário atual, o nome de um usuário para o qual o usuário atual tenha a permissão IMPERSONATE ou o nome de uma função à qual o usuário atual pertença. Quando esta cláusula é omitida, o tipo de mensagem pertence ao usuário atual.  
  
 VALIDATION  
 Especifica como o [!INCLUDE[ssSB](../../includes/sssb-md.md)] valida o corpo da mensagem para mensagens desse tipo. Quando esta cláusula não é especificada, a validação assume NONE como padrão.  
  
 Nenhuma  
 Especifica que nenhuma validação é executada. O corpo da mensagem pode conter dados ou pode ser NULL.  
  
 EMPTY  
 Especifica que o corpo da mensagem deve ser NULL.  
  
 WELL_FORMED_XML  
 Especifica que o corpo da mensagem deve conter XML bem formado.  
  
 VALID_XML WITH SCHEMA COLLECTION *schema_collection_name*  
 Especifica que o corpo da mensagem deve conter um XML que obedeça a um esquema na coleção de esquemas especificada. O *schema_collection_name* deve ser o nome de uma coleção de esquemas XML existente.  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] valida mensagens de entrada. Quando uma mensagem contém um corpo de mensagem que não obedece ao tipo de validação especificado, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] descarta a mensagem inválida e retorna uma mensagem de erro ao serviço que enviou a mensagem.  
  
 Os dois lados de uma conversa devem definir o mesmo nome para um tipo de mensagem. Para ajudar a solucionar problemas, os dois lados de uma conversa normalmente especificam a mesma validação para o tipo de mensagem, embora o [!INCLUDE[ssSB](../../includes/sssb-md.md)] não exija que os dois lados da conversa usem a mesma validação.  
  
 Um tipo de mensagem não pode ser um objeto temporário. Nomes de tipo de mensagem que começam com **#** são permitidos, mas são objetos permanentes.  
  
## <a name="permissions"></a>Permissões  
 A permissão para criar um tipo de mensagem usa como padrão os membros das funções de banco de dados fixas **db_ddladmin** ou **db_owner** e da função de servidor fixa **sysadmin**.  
  
 A permissão REFERENCES para um tipo de mensagem usa como padrão o proprietário do tipo de mensagem, os membros da função de banco de dados fixa **db_owner** e os membros da função de servidor fixa **sysadmin**.  
  
 Quando a instrução CREATE MESSAGE TYPE especifica uma coleção de esquema, o usuário que executa a instrução deve ter a permissão REFERENCES na coleção de esquema especificada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-message-type-containing-well-formed-xml"></a>a. Criando um tipo de mensagem que contém XML bem formado  
 O exemplo a seguir cria um novo tipo de mensagem que contém XML bem formado.  
  
```  
CREATE MESSAGE TYPE  
  [//Adventure-Works.com/Expenses/SubmitExpense]  
  VALIDATION = WELL_FORMED_XML ;     
```  
  
### <a name="b-creating-a-message-type-containing-typed-xml"></a>B. Criando um tipo de mensagem que contém XML com tipo  
 O exemplo a seguir cria um tipo de mensagem para um relatório de despesas codificado em XML. Ele cria uma coleção de esquema XML que contém o esquema para um relatório de despesas simples. Ele também cria um novo tipo de mensagem que valida mensagens no esquema.  
  
```  
CREATE XML SCHEMA COLLECTION ExpenseReportSchema AS  
N'<?xml version="1.0" encoding="UTF-16" ?>  
  <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
     targetNamespace="https://Adventure-Works.com/schemas/expenseReport"  
     xmlns:expense="https://Adventure-Works.com/schemas/expenseReport"  
     elementFormDefault="qualified"  
   >   
    <xsd:complexType name="expenseReportType">  
       <xsd:sequence>  
         <xsd:element name="EmployeeName" type="xsd:string"/>  
         <xsd:element name="EmployeeID" type="xsd:string"/>  
         <xsd:element name="ItemDetail"  
           type="expense:ItemDetailType" maxOccurs="unbounded"/>  
      </xsd:sequence>  
    </xsd:complexType>  
  
    <xsd:complexType name="ItemDetailType">  
      <xsd:sequence>  
        <xsd:element name="Date" type="xsd:date"/>  
        <xsd:element name="CostCenter" type="xsd:string"/>  
        <xsd:element name="Total" type="xsd:decimal"/>  
        <xsd:element name="Currency" type="xsd:string"/>  
        <xsd:element name="Description" type="xsd:string"/>  
      </xsd:sequence>  
    </xsd:complexType>  
  
    <xsd:element name="ExpenseReport" type="expense:expenseReportType"/>  
  
  </xsd:schema>' ;  
  
  CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = VALID_XML WITH SCHEMA COLLECTION ExpenseReportSchema ;  
```  
  
### <a name="c-creating-a-message-type-for-an-empty-message"></a>C. Criando um tipo de mensagem para uma mensagem vazia  
 O exemplo a seguir cria um novo tipo de mensagem com codificação vazia.  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = EMPTY ;  
```  
  
### <a name="d-creating-a-message-type-containing-binary-data"></a>D. Criando um tipo de mensagem que contém dados binários  
 O exemplo a seguir cria um novo tipo de mensagem para conter dados binários. Como a mensagem terá dados que não são XML, o tipo de mensagem especifica um tipo de validação de `NONE`. Observe que, neste caso, o aplicativo que recebe uma mensagem desse tipo deve verificar se ela contém dados e se os dados são do tipo esperado.  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ReceiptImage]  
    VALIDATION = NONE ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [DROP MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
