---
title: DELETE - Comando SQL | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303547"
---
# <a name="delete---sql-command"></a>DELETE – comando SQL
Marca registros de exclusão.  
  
 O Visual FoxPro ODBC Driver suporta a sintaxe nativa visual foxpro para este comando. Para obter informações específicas do motorista, consulte as observações.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Argumentos  
 DE [ *Nome do banco de dados!*] *Nome da tabela*  
 Especifica a tabela em que os registros estão marcados para exclusão.  
  
 *Databasename!* especifica o nome de um banco de dados que contém a tabela se o banco de dados que contém não for o banco de dados especificado com a fonte de dados. Você deve incluir o nome de um banco de dados que contenha a tabela se o banco de dados não for o banco de dados especificado com a fonte de dados. Inclua o ponto de exclamação (!) delimitador após o nome do banco de dados e antes do nome da tabela.  
  
 ONDE *FilterCondition1*[E &#124; OU *FiltroCondição2*...]  
 Especifica que o Visual FoxPro marca apenas certos registros para exclusão.  
  
 *FilterCondition* especifica os critérios que os registros devem atender para serem marcados para exclusão. Você pode incluir quantas condições de filtro quiser, conectando-as com o operador E ou OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica, ou você pode usar **EMPTY**( ) para verificar se há um campo vazio.  
  
## <a name="remarks"></a>Comentários  
 Se SET DELETED for definido como ON, os registros marcados para exclusão serão ignorados por todos os comandos que incluem um escopo.  
  
 EXCLUSão - O SQL usa o bloqueio de registros ao marcar vários registros para exclusão em tabelas abertas para acesso compartilhado. Isso reduz a contenção de registros em situações de vários usuários, mas pode diminuir o desempenho. Para o máximo desempenho, abra a mesa para uso exclusivo.  
  
## <a name="driver-remarks"></a>Observações do motorista  
 Quando seu aplicativo envia a declaração ODBC SQL DELETE para a fonte de dados, o Driver Visual FoxPro ODBC converte o comando no comando Visual FoxPro DELETE sem tradução.  
  
## <a name="see-also"></a>Consulte Também  
 [Comando SET DELETED](../../odbc/microsoft/set-deleted-command.md)
