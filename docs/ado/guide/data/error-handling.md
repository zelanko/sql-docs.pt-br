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
manager: craigg
ms.openlocfilehash: 5d8f96b28a15258df4b7d093ce14f227f28ad9b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161740"
---
# <a name="error-handling"></a>Tratamento de erros
ADO usa vários métodos diferentes para notificar um aplicativo de erros que ocorrem. Esta seção discute os tipos de erros que podem ocorrer quando você estiver usando o ADO e como seu aplicativo é notificado. Ele conclui fazendo sugestões sobre como lidar com esses erros.  
  
## <a name="how-does-ado-report-errors"></a>Como o ADO relatar erros?  
 ADO notifica você sobre erros de várias maneiras:  
  
-   Erros ADO geram um erro de tempo de execução. Manipular um erro de ADO da mesma maneira que faria com qualquer outro erro de tempo de execução, como o uso de um **On Error** instrução no Visual Basic.  
  
-   Seu programa pode receber erros de OLE DB. Um erro OLE DB gera um erro de tempo de execução também.  
  
-   Se o erro é específico para seu provedor de dados, um ou mais **erro** objetos são colocados na **erros** coleção dos **Conexão** objeto que foi usado para acessar os dados Armazene quando ocorreu o erro.  
  
-   Se o processo que disparou um evento também produziu um erro, informações de erro são colocadas em uma **erro** do objeto e passado como um parâmetro para o evento. Ver [manipulação de eventos ADO](../../../ado/guide/data/handling-ado-events.md) para obter mais informações sobre os eventos.  
  
-   Problemas que ocorrem durante o processamento em lote de atualizações ou outras operações em massa que envolvem uma **conjunto de registros** podem ser indicados pela **Status** propriedade do **conjunto de registros**. Por exemplo, permissões insuficientes ou violações de restrição de esquema podem ser especificadas por **RecordStatusEnum** valores.  
  
-   Problemas que ocorrem que envolvem uma determinada **campo** no registro atual também são indicados pela **Status** propriedade de cada **campo** no **campos**  coleção do **registro** ou **conjunto de registros**. Por exemplo, as atualizações que não pôde ser concluídas ou tipos de dados incompatíveis podem ser especificados por **FieldStatusEnum** valores.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Erros ADO](../../../ado/guide/data/ado-errors.md)  
  
-   [Erros do provedor](../../../ado/guide/data/provider-errors.md)  
  
-   [Informações de erro relacionadas ao campo](../../../ado/guide/data/field-related-error-information.md)  
  
-   [Informações de erro relacionadas ao conjunto de registros](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [Tratamento de erro em outras linguagens](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [Antecipando erros](../../../ado/guide/data/anticipating-errors.md)
