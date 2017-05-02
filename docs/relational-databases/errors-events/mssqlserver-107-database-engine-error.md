---
title: MSSQLSERVER_107 | Microsoft Docs
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
- 107 (Database Engine error)
ms.assetid: f33f514c-56aa-42e2-841b-e91244da90e2
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8cc991f218748f0f6c4d35e915656847378c46cd
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver107"></a>MSSQLSERVER_107
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|107|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|P_NOCORRMATCH|  
|Texto da mensagem|O prefixo de coluna '%.*ls' não coincide com um nome de tabela ou nome de alias usado na consulta.|  
  
## <a name="explanation"></a>Explicação  
A lista de seleção da consulta contém um asterisco (*) que é qualificado incorretamente com um prefixo de coluna. Esse erro pode ser retornado nas seguintes condições:  
  
-   O prefixo de coluna não corresponde a nenhum nome de tabela ou de alias usado na consulta. Por exemplo, a instrução a seguir utiliza um nome de alias (`T1`) como prefixo de coluna, mas o alias não está definido na cláusula FROM.  
  
    ```  
    SELECT T1.* FROM dbo.ErrorLog;  
    ```  
  
-   Um nome de tabela é especificado como prefixo de coluna quando um nome de alias da tabela é informado na cláusula FROM. Por exemplo, a instrução a seguir usa o nome de tabela `ErrorLog` como prefixo de coluna; entretanto, a tabela tem um alias (`T1`) definido na cláusula FROM.  
  
    ```  
    SELECT ErrorLog.* FROM dbo.ErrorLog AS T1;  
    ```  
  
    Se um nome de alias tiver sido especificado para um nome de tabela na cláusula FROM, você só poderá usar o alias para prefixar colunas da tabela.  
  
## <a name="user-action"></a>Ação do usuário  
Compare os prefixos de coluna com os nomes de tabela ou de alias especificados na cláusula FROM da consulta. Por exemplo, as instruções acima podem ser corrigidas da seguinte maneira:  
  
```  
SELECT T1.* FROM dbo.ErrorLog AS T1;  
```  
  
ou  
  
```  
SELECT ErrorLog.* FROM dbo.ErrorLog;  
```  
  
## <a name="see-also"></a>Consulte também  
[MSSQLSERVER_4104](~/relational-databases/errors-events/mssqlserver-4104-database-engine-error.md)  
  

