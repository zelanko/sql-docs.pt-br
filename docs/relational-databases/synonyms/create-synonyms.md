---
title: Criar sinônimos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- sql13.swb.synonym.general.f1
helpviewer_keywords:
- creating synonyms
- synonyms [SQL Server], creating
ms.assetid: fedfa7a5-d0b6-4e2b-90f4-a08122958e33
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d65e6941d6db291130b1b0e991c5626277ce38b
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581618"
---
# <a name="create-synonyms"></a>Criar sinônimos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como criar um sinônimo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar um sinônimo, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para criar um sinônimo em um determinado esquema, o usuário deve ter a permissão CREATE SYNONYM e ou ser proprietário do esquema ou ter a permissão ALTER SCHEMA. A permissão CREATE SYNONYM pode ser concedida.  
  
####  <a name="Permissions"></a> Permissões  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-synonym"></a>Para criar um sinônimo  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados em que você deseja criar a nova exibição.  
  
2.  Clique com o botão direito do mouse na pasta **Sinônimos** e clique em **Novo Sinônimo...** .  
  
3.  Na caixa de diálogo **Adicionar Sinônimo** , insira as informações a seguir.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     **Synonym name**  
     Type the new name you will use for this object.  
  
     **Synonym schema**  
     Type the schema of the new name you will use for this object.  
  
     **Server name**  
     Type the server instance to connect to.  
  
     **Database name**  
     Type or select the database containing the object.  
  
     **Schema**  
     Type or select the schema that owns the object.  
  
     **Object type**  
     Select the type of object.  
  
     **Object name**  
     Type the name of the object to which the synonym refers.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-synonym"></a>Para criar um sinônimo  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole os exemplos a seguir na janela de consulta e clique em **Executar**.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir cria um sinônimo para uma tabela existente no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . O sinônimo é usado então em exemplos subsequentes.  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyAddressType  
FOR AdventureWorks2012.Person.AddressType;  
GO  
```  
  
 O exemplo a seguir insere uma linha na tabela base que é referida pelo sinônimo `MyAddressType` .  
  
```  
USE tempdb;  
GO  
INSERT INTO MyAddressType (Name)  
VALUES ('Test');  
GO  
```  
  
 O exemplo a seguir demonstra como um sinônimo pode ser referido no SQL dinâmico.  
  
```  
USE tempdb;  
GO  
EXECUTE ('SELECT Name FROM MyAddressType');  
GO  
```  
  
  
