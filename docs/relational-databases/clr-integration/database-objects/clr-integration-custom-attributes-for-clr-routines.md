---
title: Atributos personalizados para rotinas CLR | Microsoft Docs
description: Atributos personalizados podem ser aplicados a rotinas CLR, tipos definidos pelo usuário e agregações definidas pelo usuário que são registradas no Microsoft SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
ms.openlocfilehash: bad209c4ddb516167b8048ae73680bc9ea59cc05
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810800"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>Atributos personalizados da integração CLR para rotinas CLR
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Os atributos listados podem ser aplicados a rotinas de Common Language Runtime (CLR), tipos definidos pelo usuário e agregações definidas pelo usuário que são registradas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se o atributo não for aplicado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] assumirá o valor padrão. Os atributos listados são definidos no namespace **Microsoft. SqlServer. Server** .  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>O atributo SqlUserDefinedAggregate  
 O atributo **SqlUserDefinedAggregate** indica que o método deve ser registrado como uma agregação definida pelo usuário. Todas as agregações definidas pelo usuário devem ser anotadas com esse atributo.  
  
 Para obter mais informações, consulte [SqlUserDefinedAggregateAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedaggregateattribute).  
  
## <a name="the-sqlfunction-attribute"></a>O atributo SqlFunction  
 O atributo **SqlFunction** indica que o método deve ser registrado como uma função, com os atributos de função apropriados definidos.  
  
 Para obter mais informações, consulte [SqlFunctionAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfunctionattribute).  
  
## <a name="the-sqlfacet-attribute"></a>O atributo SqlFacet  
 O atributo **sqlfacial** é usado para retornar informações sobre o tipo de retorno de uma expressão UDT (tipo definido pelo usuário).  
  
 Para obter mais informações, consulte [SqlFacetAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfacetattribute).  
  
## <a name="the-sqlprocedure-attribute"></a>O atributo SqlProcedure  
 O atributo **SqlProcedure** indica que o método deve ser registrado como um procedimento armazenado. Esse atributo só é usado pelo Visual Studio para registrar o método especificado como um procedimento armazenado automaticamente; não é usado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações, consulte [SqlProcedureAttribute](/dotnet/api/microsoft.sqlserver.server.sqlprocedureattribute).  
  
## <a name="the-sqltrigger-attribute"></a>O atributo SqlTrigger  
 O atributo **SqlTrigger** indica que o método deve ser registrado como um gatilho.  
  
 Para obter mais informações, consulte [SqlTriggerContext](/dotnet/api/microsoft.sqlserver.server.sqltriggercontext) e [SqlTriggerAttribute](/dotnet/api/microsoft.sqlserver.server.sqltriggerattribute).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>O SqlUserDefinedTypeAttribute  
 Você pode aplicar o SqlUserDefinedTypeAttribute a uma definição de classe no assembly. Ele faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crie um tipo definido pelo usuário que é associado à definição de classe que tem esse atributo personalizado.  
  
 Para obter mais informações, consulte [SqlUserDefinedTypeAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedtypeattribute).  
  
## <a name="the-sqlmethod-attribute"></a>O atributo SqlMethod  
 O atributo **SqlMethod** é usado para indicar o determinante e as propriedades de acesso a dados de um método ou uma propriedade em um UDT.  
  
 Para obter mais informações, consulte [SqlMethodAttribute](/dotnet/api/microsoft.sqlserver.server.sqlmethodattribute).  
  
## <a name="see-also"></a>Consulte Também  
 [Agregações CLR definidas pelo usuário](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Funções CLR definidas pelo usuário](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipos definidos pelo usuário de CLR](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Procedimentos armazenados CLR](/dotnet/framework/data/adonet/sql/clr-stored-procedures)   
 [Gatilhos de CLR](/dotnet/framework/data/adonet/sql/clr-triggers)  
  
