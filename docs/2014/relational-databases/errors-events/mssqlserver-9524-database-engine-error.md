---
title: MSSQLSERVER_9524 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16f5876211a987dff593721310ee31667d428b81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761661"
---
# <a name="mssqlserver_9524"></a>MSSQLSERVER_9524
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|9254|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|XMLERR_INVALID_COLUMNSET_XML|  
|Texto da mensagem|O conteúdo XML fornecido não se adapta ao formato XML exigido para conjuntos de colunas esparsos.|  
  
## <a name="explanation"></a>Explicação  
 Uma tentativa foi feita para modificar um conjunto de colunas. É necessário que o conteúdo em XML de um conjunto de colunas esteja de acordo com as restrições de formato de um conjunto de colunas. O formato geral de um conjunto de colunas é o seguinte:  
  
 `<column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...`  
  
 Para obter mais informações sobre conjuntos de colunas, consulte o tópico "Usando conjuntos de colunas" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Ação do usuário  
 Corrija o formato do XML para o conjunto de colunas na instrução.  
  
  
