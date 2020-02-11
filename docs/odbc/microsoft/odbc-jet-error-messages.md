---
title: Mensagens de erro ODBC Jet | Microsoft Docs
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
ms.openlocfilehash: 85e0f9a8bc7015a0ad5b12ce46a6c94ab31ca43c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915809"
---
# <a name="odbc-jet-error-messages"></a>Mensagens de erro do Jet do ODBC
Para erros que ocorrem na fonte de dados, o driver ODBC retorna uma mensagem de erro retornada a ele pela biblioteca de arquivos ODBC. Para erros que ocorrem no driver ODBC ou no Gerenciador de driver, o driver retorna uma mensagem de erro com base no texto associado ao SQLSTATE.  
  
 As mensagens de erro têm o seguinte formato:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 Os prefixos entre colchetes ([]) identificam o local do erro. Quando o erro ocorre no Gerenciador de driver, a *fonte de dados* não é fornecida. Quando o erro ocorre na fonte de dados, os prefixos [*fornecedor*] e [*ODBC-Component*] identificam o fornecedor e o nome do componente ODBC que recebeu o erro da fonte de dados.  
  
 A tabela a seguir mostra as mensagens de erro retornadas pelo Gerenciador de driver e driver ISAM:  
  
|Mensagem de erro|Localização do erro|  
|-------------------|--------------------|  
|O [Gerenciador de driver ODBC] *texto da mensagem*|Gerenciador de driver (Odbc32. dll)|  
|O [ *Nome do driver*ODBC] *texto da mensagem*|Driver ISAM (consulte ISAM de driver)|
