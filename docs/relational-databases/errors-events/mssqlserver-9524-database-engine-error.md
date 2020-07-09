---
title: MSSQLSERVER_9524 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c5513126899b4ad2790ecd252e54e40b769e3184
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85636216"
---
# <a name="mssqlserver_9524"></a>MSSQLSERVER_9524
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
  
