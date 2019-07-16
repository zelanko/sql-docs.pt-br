---
title: 'Alternativas: Usando instruções SQL | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f41ef7f0641877056a6e2f3d85fd6a40ff7826db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925999"
---
# <a name="alternatives-using-sql-statements"></a>Alternativas: Usando instruções SQL
ADO também permite usar comandos como alternativas para suas propriedades internas e métodos para a edição de dados. Dependendo do seu provedor, todas as operações mencionadas nesta seção também podem ser feitas passando comandos para sua fonte de dados. Por exemplo, instruções de atualização do SQL podem ser usadas para modificar os dados sem usar o **valor** propriedade de uma **campo**. Instruções SQL INSERT podem ser usadas para adicionar novos registros para uma fonte de dados, em vez do método ADO **AddNew**. Para obter mais informações sobre o SQL ou a linguagem de manipulação de dados do seu provedor, consulte a documentação da fonte de dados.  
  
 Por exemplo, você pode passar uma cadeia de caracteres SQL que contém uma instrução DELETE para um banco de dados, conforme mostrado no código a seguir:  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
