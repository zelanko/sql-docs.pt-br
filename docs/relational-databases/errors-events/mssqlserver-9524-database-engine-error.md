---
title: MSSQLSERVER_9524 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5896357fde2c8930544bd435884701a7a406ee34
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9524"></a>MSSQLSERVER_9524
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9254|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|XMLERR_INVALID_COLUMNSET_XML|  
|Texto da mensagem|O conteúdo XML fornecido não se adapta ao formato XML exigido para conjuntos de colunas esparsos.|  
  
## <a name="explanation"></a>Explicação  
Uma tentativa foi feita para modificar um conjunto de colunas. É necessário que o conteúdo em XML de um conjunto de colunas esteja de acordo com as restrições de formato de um conjunto de colunas. O formato geral de um conjunto de colunas é o seguinte:  
  
`<column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...`  
  
Para obter mais informações sobre conjuntos de colunas, consulte o tópico "Usando conjuntos de colunas" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Ação do usuário  
Corrija o formato do XML para o conjunto de colunas na instrução.  
  

