---
title: Tratamento de erro | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cb3213b6a4c5711ccb8d6f9243047d8361a6e37
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925423"
---
# <a name="error-handling"></a>Tratamento de erros
O ADO usa vários métodos diferentes para notificar uma aplicação de erros que ocorrem. Esta seção aborda os tipos de erros que podem ocorrer quando você está usando o ADO e como seu aplicativo é notificado. Ele conclui fazendo sugestões sobre como lidar com esses erros.  
  
## <a name="how-does-ado-report-errors"></a>Como o ADO relata erros?  
 O ADO notifica sobre erros de várias maneiras:  
  
-   Os erros do ADO geram um erro em tempo de execução. Manipule um erro ADO da mesma maneira que faria com qualquer outro erro em tempo de execução, como o uso de uma instrução **On Error** no Visual Basic.  
  
-   Seu programa pode receber erros de OLE DB. Um erro OLE DB gera um erro de tempo de execução também.  
  
-   Se o erro for específico para seu provedor de dados, um ou mais objetos de **erro** serão colocados na coleção de **erros** do objeto de **conexão** que foi usado para acessar o armazenamento de dados quando o erro ocorreu.  
  
-   Se o processo que gerou um evento também produziu um erro, as informações de erro serão colocadas em um objeto de **erro** e transmitidas como um parâmetro para o evento. Consulte [manipulando eventos ADO](../../../ado/guide/data/handling-ado-events.md) para obter mais informações sobre eventos.  
  
-   Problemas que ocorrem durante o processamento de atualizações em lote ou outras operações em massa que envolvem um **conjunto de registros** podem ser indicados pela propriedade **status** do **conjunto de registros**. Por exemplo, violações de restrição de esquema ou permissões insuficientes podem ser especificadas por valores de **RecordStatusEnum** .  
  
-   Os problemas que ocorrem envolvendo um determinado **campo** no registro atual também são indicados pela propriedade **status** de cada **campo** na coleção **Fields** do **registro** ou **conjunto de registros**. Por exemplo, as atualizações que não puderam ser concluídas ou tipos de dados incompatíveis podem ser especificadas por valores de **FieldStatusEnum** .  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Erros ADO](../../../ado/guide/data/ado-errors.md)  
  
-   [Erros do provedor](../../../ado/guide/data/provider-errors.md)  
  
-   [Informações de erro relacionadas ao campo](../../../ado/guide/data/field-related-error-information.md)  
  
-   [Informações de erro relacionadas ao conjunto de registros](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [Tratamento de erro em outras linguagens](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [Antecipando erros](../../../ado/guide/data/anticipating-errors.md)
