---
title: DELETE – comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dac94d8bfb0e2bc0ab91f6a18e6f18606481b112
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198581"
---
# <a name="delete---sql-command"></a>DELETE – comando SQL
Registros de marcas para exclusão.  
  
 O Driver de ODBC do Visual FoxPro dá suporte à sintaxe de linguagem do Visual FoxPro nativo para esse comando. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Argumentos  
 FROM [ *DatabaseName!*] *TableName*  
 Especifica a tabela na qual os registros são marcados para exclusão.  
  
 *DatabaseName!* Especifica o nome de um banco de dados que contém a tabela se o banco de dados que contém não for o banco de dados especificado com a fonte de dados. Você deve incluir o nome de um banco de dados que contém a tabela se o banco de dados não for o banco de dados especificado com a fonte de dados. Inclua o delimitador de ponto de exclamação (!) após o nome do banco de dados e antes do nome da tabela.  
  
 Em que *FilterCondition1*[AND &#124; ou *FilterCondition2*...]  
 Especifica que o Visual FoxPro marcar apenas determinados registros para exclusão.  
  
 *FilterCondition* Especifica os critérios que os registros devem atender para ser marcado para exclusão. Você pode incluir quantos condições de filtragem, como você deseja conectar-se com o operador e ou operador OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica, ou você pode usar **vazio**() para verificar se há um campo vazio.  
  
## <a name="remarks"></a>Comentários  
 Se definir excluído é definido como ON, registros marcados para exclusão são ignorados por todos os comandos que incluem um escopo.  
  
 Exclua - usa SQL bloqueio de registro quando a marcação de vários registros para exclusão em tabelas aberto para acesso compartilhado. Isso reduz a contenção de registros em situações de multiusuários, mas pode diminuir o desempenho. Para obter máximo desempenho, abra a tabela para uso exclusivo.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Quando seu aplicativo envia a instrução DELETE do ODBC SQL para a fonte de dados, o Driver de ODBC do Visual FoxPro converte o comando para o comando Excluir do Visual FoxPro sem tradução.  
  
## <a name="see-also"></a>Consulte também  
 [Comando SET DELETED](../../odbc/microsoft/set-deleted-command.md)
