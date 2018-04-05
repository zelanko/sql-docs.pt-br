---
title: Comando de tabela DROP | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c6b38eeeba42f1a24520c176fb2f49caac1712e2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="drop-table-command"></a>Remova o comando de tabela
Remove uma tabela de banco de dados especificado com a fonte de dados e o exclui do disco.  
  
 O Driver de ODBC do Visual FoxPro oferece suporte a sintaxe de linguagem do Visual FoxPro nativo para este comando. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>Configurações  
 *Nome de tabela*  
 Especifica a tabela para remover o banco de dados especificado com a fonte de dados e excluir do disco.  
  
 *FileName*  
 Especifica uma tabela livre para excluir do disco.  
  
 ?  
 Exibe a caixa de diálogo Remover do qual você pode escolher uma tabela para remover o banco de dados especificado com a fonte de dados e excluir do disco.  
  
## <a name="remarks"></a>Remarks  
 Quando DROP TABLE é emitido, todos os índices primários, valores padrão e as regras de validação associadas à tabela também são removidas. DROP TABLE também afeta outras tabelas no banco de dados especificado com a fonte de dados se as tabelas têm regras ou relações associadas à tabela que está sendo removida. As regras e as relações não são mais válidas quando a tabela é removida do banco de dados.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Quando o aplicativo envia a instrução SQL ODBC DROP TABLE para a fonte de dados, o Driver de ODBC do Visual FoxPro converte o comando para o comando de tabela FoxProDROP Visual usando a sintaxe mostrada na tabela a seguir.  
  
|Sintaxe ODBC|Fonte de dados|Sintaxe do Visual FoxPro|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE *nome da tabela de base*|Banco de dados (arquivo. dbc)|Remover tabela *TableName* excluir|  
||Diretório de tabelas livres (arquivos. dbf)|APAGAR *dbfName*<br /><br /> APAGAR *cdxName*<br /><br /> APAGAR *fptName*|
