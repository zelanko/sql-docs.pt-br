---
title: sp_syscollector_update_collector_type (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collector_type_TSQL
- sp_syscollector_update_collector_type
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 3c414dfd-d9ca-4320-81aa-949465b967bf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed8c11a7d5f333a086482d2882a6aef7a97370e3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830064"
---
# <a name="spsyscollectorupdatecollectortype-transact-sql"></a>sp_syscollector_update_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza um tipo de coletor para um item de coleta. Dado o nome e a GUID de um tipo de coletor, atualiza a configuração do tipo de coletor, inclusive a coleção e o pacote de carregamento, o esquema de parâmetros e o esquema do formatador de parâmetros.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_update_collector_type [ @collector_type_uid = ] 'collector_type_uid' OUTPUT  
          , [ @name = ] 'name'  
          , [ @parameter_schema = ] 'parameter_schema'  
          , [ @collection_package_id = ] collection_package_id  
          , [ @upload_package_id = ] upload_package_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@collector_type_uid =** ] **'***collector_type_uid***'**  
 É o GUID do tipo de coletor. *collector_type_uid* está **uniqueidentifier**, e se for NULL, ele será automaticamente criado e retornado como OUTPUT.  
  
 [  **@name =** ] **'***nome***'**  
 É o nome do tipo de coletor. *nome da* está **sysname** e deve ser especificado.  
  
 [  **@parameter_schema =** ] **'***parameter_schema***'**  
 É o esquema XML deste tipo de coletor. *parameter_schema* está **xml** e pode ser necessário para determinados tipos de coletor. Se não for necessário, esse argumento poderá ser NULL.  
  
 [  **@collection_package_id =** ] *collection_package_id*  
 É um identificador exclusivo local que aponta para o pacote de coleta do [!INCLUDE[ssIS](../../includes/ssis-md.md)] usado pelo conjunto de coleta. *collection_package_id* está **uniqueidentifer** e é necessária. Para obter o valor de *collection_package_id*, consulte a exibição de sistema syscollector_collector_types no banco de dados msdb.  
  
 [  **@upload_package_id =** ] *upload_package_id*  
 É um identificador exclusivo local que aponta para o pacote de carregamento do [!INCLUDE[ssIS](../../includes/ssis-md.md)] usado pelo conjunto de coleta. *upload_package_id* está **uniqueidentifier** e é necessária. Para obter o valor de *upload_package_id*, consulte a exibição de sistema syscollector_collector_types no banco de dados msdb.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **dc_admin** (com permissão EXECUTE) a função de banco de dados fixa.  
  
## <a name="example"></a>Exemplo  
 Esse exemplo atualiza o tipo de coletor de Consulta T-SQL Genérico. (No exemplo, o esquema padrão do tipo de coletor de Consulta T-SQL Genérico é usado.)  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collector_type  
@collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
@name = 'Generic T-SQL Query Collector Type',  
@parameter_schema = '<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="DataCollectorType">  
  <xs:element name="TSQLQueryCollector">  
<xs:complexType>  
  <xs:sequence>  
<xs:element name="Query" minOccurs="1" maxOccurs="unbounded">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Value" type="xs:string" />  
  <xs:element name="OutputTable" type="xs:string" />  
</xs:sequence>  
  </xs:complexType>  
</xs:element>  
<xs:element name="Databases" minOccurs="0" maxOccurs="1">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Database" minOccurs="0" maxOccurs="unbounded" type="xs:string" />  
</xs:sequence>  
<xs:attribute name="UseSystemDatabases" type="xs:boolean" use="optional" />  
<xs:attribute name="UseUserDatabases" type="xs:boolean" use="optional" />  
  </xs:complexType>  
</xs:element>  
  </xs:sequence>  
</xs:complexType>  
  </xs:element>  
</xs:schema>',  
@collection_package_id = '292B1476-0F46-4490-A9B7-6DB724DE3C0B',  
@upload_package_id = '6EB73801-39CF-489C-B682-497350C939F0';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
