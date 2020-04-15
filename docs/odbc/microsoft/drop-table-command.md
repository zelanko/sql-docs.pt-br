---
title: Comando DROP TABLE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 779c519f720027aea3a6f6cf2587d3c6e0b59b52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303417"
---
# <a name="drop-table-command"></a>Comando DROP TABLE
Remove uma tabela do banco de dados especificada com a fonte de dados e a exclui do disco.  
  
 O Visual FoxPro ODBC Driver suporta a sintaxe nativa visual foxpro para este comando. Para obter informações específicas do motorista, consulte as observações.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>Configurações  
 *Tablename*  
 Especifica a tabela para remover do banco de dados especificado com a fonte de dados e para excluir do disco.  
  
 *Filename*  
 Especifica uma tabela gratuita para excluir do disco.  
  
 ?  
 Exibe a caixa de diálogo Remover da qual você pode escolher uma tabela para remover do banco de dados especificado com a fonte de dados e para excluir do disco.  
  
## <a name="remarks"></a>Comentários  
 Quando a TABELA DROP é emitida, todos os índices primários, valores padrão e regras de validação associados à tabela também são removidos. Tabela DROP também afeta outras tabelas no banco de dados especificadas com a fonte de dados se essas tabelas tiverem regras ou relações associadas à tabela a ser removida. As regras e relações não são mais válidas quando a tabela é removida do banco de dados.  
  
## <a name="driver-remarks"></a>Observações do motorista  
 Quando seu aplicativo envia a tabela de gota da declaração SQL ODBC para a fonte de dados, o Driver Visual FoxPro ODBC converte o comando no comando Visual FoxProDROP TABLE usando a sintaxe mostrada na tabela a seguir.  
  
|Sintaxe ODBC|Fonte de dados|Sintaxe Visual FoxPro|  
|-----------------|-----------------|--------------------------|  
|NOME *da tabela de base* DROP TABLE|Banco de dados (arquivo.dbc)|REMOVER *TABELA Nome de* TABELA EXCLUSão|  
||Diretório de tabelas gratuitas (arquivos.dbf)|ERASE *dbfName*<br /><br /> ERASE *cdxName*<br /><br /> ERASE *fptName*|
