---
title: Atributos personalizados para rotinas CLR | Microsoft Docs
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
ms.openlocfilehash: f1ff346abc41ee4589a8d0b2193b167fb2cf24e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70212379"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>Atributos personalizados da integração CLR para rotinas CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Os atributos listados podem ser aplicados a rotinas de Common Language Runtime (CLR), tipos definidos pelo usuário e agregações definidas pelo usuário que são registradas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se o atributo não for aplicado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] assumirá o valor padrão. Os atributos listados são definidos no namespace **Microsoft. SqlServer. Server** .  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>O atributo SqlUserDefinedAggregate  
 O atributo **SqlUserDefinedAggregate** indica que o método deve ser registrado como uma agregação definida pelo usuário. Todas as agregações definidas pelo usuário devem ser anotadas com esse atributo.  
  
 Para obter mais informações, consulte [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>O atributo SqlFunction  
 O atributo **SqlFunction** indica que o método deve ser registrado como uma função, com os atributos de função apropriados definidos.  
  
 Para obter mais informações, consulte [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>O atributo SqlFacet  
 O atributo **sqlfacial** é usado para retornar informações sobre o tipo de retorno de uma expressão UDT (tipo definido pelo usuário).  
  
 Para obter mais informações, consulte [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>O atributo SqlProcedure  
 O atributo **SqlProcedure** indica que o método deve ser registrado como um procedimento armazenado. Esse atributo só é usado pelo Visual Studio para registrar o método especificado como um procedimento armazenado automaticamente; não é usado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações, consulte [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>O atributo SqlTrigger  
 O atributo **SqlTrigger** indica que o método deve ser registrado como um gatilho.  
  
 Para obter mais informações, consulte [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022) e [SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>O SqlUserDefinedTypeAttribute  
 Você pode aplicar o SqlUserDefinedTypeAttribute a uma definição de classe no assembly. Ele faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crie um tipo definido pelo usuário que é associado à definição de classe que tem esse atributo personalizado.  
  
 Para obter mais informações, consulte [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>O atributo SqlMethod  
 O atributo **SqlMethod** é usado para indicar o determinante e as propriedades de acesso a dados de um método ou uma propriedade em um UDT.  
  
 Para obter mais informações, consulte [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Consulte Também  
 [Agregações CLR definidas pelo usuário](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Funções CLR definidas pelo usuário](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipos definidos pelo usuário de CLR](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Procedimentos armazenados CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Gatilhos CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
