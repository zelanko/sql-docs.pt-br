---
title: Tratamento de erro | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d22a7f0b1472fd5f55535bf6ffb9295729a0087
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="error-handling"></a>Tratamento de erros
ADO usa vários métodos diferentes para notificar um aplicativo de erros que ocorrem. Esta seção aborda os tipos de erros que podem ocorrer quando você estiver usando o ADO e como o aplicativo é notificado. Ele conclui fazendo sugestões sobre como lidar com esses erros.  
  
## <a name="how-does-ado-report-errors"></a>Como o ADO relatar erros?  
 ADO notifica sobre erros de várias maneiras:  
  
-   Erros de ADO geram um erro de tempo de execução. Lidar com um erro de ADO da mesma maneira que faria com qualquer outro erro de tempo de execução, como o uso de um **On Error** instrução no Visual Basic.  
  
-   Seu programa pode receber erros de OLE DB. Um erro de OLE DB gera um erro de tempo de execução também.  
  
-   Se o erro é específico ao provedor de dados, um ou mais **erro** objetos são colocados no **erros** coleção do **Conexão** objeto que foi usado para acessar os dados Armazene quando ocorreu o erro.  
  
-   Se o processo que disparou um evento também produziu um erro, informações de erro são colocadas em uma **erro** de objeto e passada como um parâmetro para o evento. Consulte [manipulando eventos de ADO](../../../ado/guide/data/handling-ado-events.md) para obter mais informações sobre os eventos.  
  
-   Problemas que ocorrem durante o processamento em lote de atualizações ou outras operações em massa que envolvem um **registros** pode ser indicado pelo **Status** propriedade do **registros**. Por exemplo, permissões insuficientes ou violações de restrição de esquema podem ser especificadas por **RecordStatusEnum** valores.  
  
-   Problemas que ocorrem que envolvem uma determinada **campo** no registro atual também são indicadas pelo **Status** propriedade de cada **campo** no **campos**  coleção do **registro** ou **registros**. Por exemplo, as atualizações que não podem ser concluídas ou tipos de dados incompatíveis podem ser especificados por **FieldStatusEnum** valores.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Erros ADO](../../../ado/guide/data/ado-errors.md)  
  
-   [Erros do provedor](../../../ado/guide/data/provider-errors.md)  
  
-   [Informações de erro relacionadas ao campo](../../../ado/guide/data/field-related-error-information.md)  
  
-   [Informações de erro relacionadas ao conjunto de registros](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [Tratamento de erro em outras linguagens](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [Antecipando erros](../../../ado/guide/data/anticipating-errors.md)
