---
title: Mensagens de erro do Jet do ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec549f256caeab598f6e49632b2a50cfa5841710
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63244609"
---
# <a name="odbc-jet-error-messages"></a>Mensagens de erro do Jet do ODBC
Para erros que ocorrem na fonte de dados, o driver ODBC retorna uma mensagem de erro retornada a ele pela biblioteca de arquivo ODBC. Para erros que ocorrem no driver ODBC ou o Gerenciador de Driver, os retornos de driver, uma mensagem de erro com base no texto associado com o SQLSTATE.  
  
 Mensagens de erro têm o seguinte formato:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 Os prefixos de colchetes ([]) identificam o local do erro. Quando o erro ocorre no Gerenciador de Driver, *fonte de dados* não for fornecido. Quando o erro ocorre na fonte de dados, o [*fornecedor*] e [*componente ODBC*] prefixos de identificam o fornecedor e o nome do componente ODBC que recebeu o erro da fonte de dados.  
  
 A tabela a seguir mostra as mensagens de erro retornadas pelo Gerenciador de Driver e driver ISAM:  
  
|Mensagem de erro|Local do erro|  
|-------------------|--------------------|  
|[Microsoft] [Gerenciador de Driver ODBC] *texto da mensagem*|Gerenciador de driver (Odbc32. dll)|  
|[Microsoft][ODBC *driver-name*]*message-text*|O driver ISAM (consulte ISAMs Driver)|
