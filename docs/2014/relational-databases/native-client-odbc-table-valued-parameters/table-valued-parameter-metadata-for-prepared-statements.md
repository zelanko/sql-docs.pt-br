---
title: Metadados de parâmetro com valor de tabela para instruções preparadas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1323c8e1fbc7c0b4a305ee2200dfbd457e98fe6f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411355"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>Metadados do parâmetro com valor de tabela para instruções preparadas
  Um aplicativo pode obter metadados para uma chamada de procedimento preparada por meio de SQLNumParams e SQLDescribeParam. Para parâmetros com valor de tabela, *DataTypePtr* é definido como SQL_SS_TABLE. Metadados adicionais estão disponíveis por meio de SQLGetDescField para SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME e SQL_CA_SS_SCHEMA_NAME.  
  
 SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME e SQL_CA_SS_SCHEMA_NAME podem ser usado com SQLColumns para obter metadados de coluna para tipos de tabela associados com parâmetros com valor de tabela. Nesse caso, SQL_SOPT_SS_NAME_SCOPE deve ser definido como SQL_SS_NAME_SCOPE_TABLE_TYPE antes de SQLColumns é chamado. SQL_SOPT_SS_NAME_SCOPE deve ser definido novamente com o valor padrão, SQL_SS_NAME_SCOPE_TABLE, quando o aplicativo concluir a recuperação de metadados da coluna do parâmetro com valor de tabela.  
  
 SQL_CA_SS_TYPE_NAME , SQL_CA_SS_CATALOG_NAME e SQL_CA_SS_SCHEMA_NAME também podem ser usados com parâmetros de tipo de dado CLR definido pelo usuário.  
  
 Você não pode obter metadados de parâmetro com valor de tabela para instruções preparadas que não são chamadas de procedimento armazenado. Se você tentar fazer isto, o aplicativo retornará SQL_ERROR com SQLSTATE 42000 e a mensagem "Erro de sintaxe ou violação de acesso".  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
