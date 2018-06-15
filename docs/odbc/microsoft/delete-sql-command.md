---
title: Exclua - o comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e00f1d819f792f88ffb4495385be5abd754af21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32902541"
---
# <a name="delete---sql-command"></a>Exclua - o comando SQL
Marca registros para exclusão.  
  
 O Driver de ODBC do Visual FoxPro oferece suporte a sintaxe de linguagem do Visual FoxPro nativo para este comando. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Argumentos  
 DE [ *DatabaseName!*] *TableName*  
 Especifica a tabela na qual os registros são marcados para exclusão.  
  
 *DatabaseName!* Especifica o nome de um banco de dados que contém a tabela se o banco de dados de conteúdo não é o banco de dados especificado com a fonte de dados. Você deve incluir o nome de um banco de dados que contém a tabela se o banco de dados não é o banco de dados especificado com a fonte de dados. Inclua o delimitador de ponto de exclamação (!) depois do nome do banco de dados e antes do nome da tabela.  
  
 ONDE *FilterCondition1*[AND &#124; ou *FilterCondition2*...]  
 Especifica que o Visual FoxPro marcar apenas determinados registros para exclusão.  
  
 *FilterCondition* Especifica os critérios que os registros devem atender para ser marcado para exclusão. Você pode incluir muitas condições de filtragem você deseja conectar-se com AND ou operador OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica, ou você pode usar **vazio**() para verificar se há um campo vazio.  
  
## <a name="remarks"></a>Remarks  
 Se definir excluído está definido como ON, registros marcados para exclusão são ignorados por todos os comandos que incluem um escopo.  
  
 Exclua - usa SQL bloqueio de registro quando a marcação de vários registros para exclusão em tabelas aberto para acesso compartilhado. Isso reduz a contenção de registro em situações de multiusuários, mas pode diminuir o desempenho. Para obter desempenho máximo, abra a tabela para uso exclusivo.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Quando o aplicativo envia a instrução DELETE do ODBC SQL para a fonte de dados, o Driver de ODBC do Visual FoxPro converte o comando para o comando Excluir do Visual FoxPro sem conversão.  
  
## <a name="see-also"></a>Consulte também  
 [Comando SET DELETED](../../odbc/microsoft/set-deleted-command.md)
