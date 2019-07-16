---
title: Comando de tabela DROP | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 278950bac7589b8a6b02d894c8133a699c3bd1ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071800"
---
# <a name="drop-table-command"></a>Comando DROP TABLE
Remove uma tabela de banco de dados especificado com a fonte de dados e a exclui do disco.  
  
 O Driver de ODBC do Visual FoxPro dá suporte à sintaxe de linguagem do Visual FoxPro nativo para esse comando. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>Configurações  
 *TableName*  
 Especifica a tabela a ser removido do banco de dados especificado com a fonte de dados e excluir do disco.  
  
 *FileName*  
 Especifica uma tabela livre para excluir do disco.  
  
 ?  
 Exibe a caixa de diálogo Remover do qual você pode escolher uma tabela para remover do banco de dados especificado com a fonte de dados e excluir do disco.  
  
## <a name="remarks"></a>Comentários  
 Quando DROP TABLE é emitido, todos os índices primários, valores padrão e as regras de validação associadas com a tabela também são removidas. DROP TABLE também afeta outras tabelas no banco de dados especificado com a fonte de dados se essas tabelas tem regras ou relações associadas à tabela que está sendo removida. As regras e as relações não são mais válidas quando a tabela é removida do banco de dados.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Quando seu aplicativo envia a instrução ODBC SQL DROP TABLE para a fonte de dados, o Driver de ODBC do Visual FoxPro converte o comando para o comando de tabela de FoxProDROP Visual usando a sintaxe mostrada na tabela a seguir.  
  
|Sintaxe de ODBC|Fonte de dados|Sintaxe do Visual FoxPro|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE *nome da tabela de base*|Banco de dados (arquivo. dbc)|Remover tabela *TableName* excluir|  
||Diretório de tabelas livres (arquivos. dbf)|ERASE *dbfName*<br /><br /> APAGAR *cdxName*<br /><br /> APAGAR *fptName*|
