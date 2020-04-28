---
title: DELETE-comando SQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9757fd57d999815964266c035963de1129eaf5e8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303547"
---
# <a name="delete---sql-command"></a>DELETE – comando SQL
Marca os registros para exclusão.  
  
 O driver ODBC do Visual FoxPro dá suporte à sintaxe de linguagem nativa do Visual FoxPro para este comando. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Argumentos  
 DE [ *DatabaseName!*] *TableName*  
 Especifica a tabela na qual os registros são marcados para exclusão.  
  
 *NomeDoBancoDeDados!* Especifica o nome de um banco de dados que contém a tabela, se o banco de dado que o contém não for o especificado com a fonte. Você deve incluir o nome de um banco de dados que contenha a tabela se o banco de dado não for o banco especificado com a fonte. Inclua o delimitador de ponto de exclamação (!) após o nome do banco de dados e antes do nome da tabela.  
  
 EM que *FilterCondition1*[e &#124; ou *FilterCondition2*...]  
 Especifica que o Visual FoxPro marca apenas determinados registros para exclusão.  
  
 *FilterCondition* especifica os critérios que os registros devem atender para serem marcados para exclusão. Você pode incluir quantas condições de filtro desejar, conectando-as com o operador AND ou OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica ou pode usar **Empty**() para verificar se há um campo vazio.  
  
## <a name="remarks"></a>Comentários  
 Se SET DELETED for definido como ON, os registros marcados para exclusão serão ignorados por todos os comandos que incluem um escopo.  
  
 DELETE-SQL usa o bloqueio de registro ao marcar vários registros para exclusão em tabelas abertas para acesso compartilhado. Isso reduz a contenção de registros em situações multiusuários, mas pode diminuir o desempenho. Para obter o máximo de desempenho, abra a tabela para uso exclusivo.  
  
## <a name="driver-remarks"></a>Comentários do driver  
 Quando o aplicativo envia a instrução SQL ODBC DELETE para a fonte de dados, o driver ODBC do Visual FoxPro converte o comando no comando DELETE do Visual FoxPro sem tradução.  
  
## <a name="see-also"></a>Consulte Também  
 [Comando SET DELETED](../../odbc/microsoft/set-deleted-command.md)
