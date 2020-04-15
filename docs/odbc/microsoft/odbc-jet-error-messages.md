---
title: Mensagens de erro do jato ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8fa6e672b69c7791e66dc3919e6fcd22b7c3de7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293106"
---
# <a name="odbc-jet-error-messages"></a>Mensagens de erro do Jet do ODBC
Para erros que ocorrem na fonte de dados, o driver ODBC retorna uma mensagem de erro devolvida a ela pela Biblioteca de Arquivos ODBC. Para erros que ocorrem no driver ODBC ou no Gerenciador de driver, o driver retorna uma mensagem de erro com base no texto associado ao SQLSTATE.  
  
 As mensagens de erro têm o seguinte formato:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 Os prefixos entre parênteses ([]) identificam a localização do erro. Quando o erro ocorre no Gerenciador de driver, a *fonte de dados* não é dada. Quando o erro ocorre na fonte de dados, os prefixos *[fornecedor]* e [*componente ODBC]* identificam o fornecedor e o nome do componente ODBC que recebeu o erro da fonte de dados.  
  
 A tabela a seguir mostra as mensagens de erro retornadas pelo Driver Manager e pelo driver ISAM:  
  
|Mensagem de erro|Localização de erro|  
|-------------------|--------------------|  
|[Microsoft] [Gerente de Driver ODBC] *mensagem de texto*|Driver Manager (Odbc32.dll)|  
|[Microsoft] [Nome *do driver*ODBC ] *mensagem de texto*|Driver ISAM (ver DRIVER ISAMs)|
