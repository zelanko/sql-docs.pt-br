---
title: Metadados de TVP para declarações preparadas
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6928c24b1c06e75c8e20b318321eac4f4bd99985
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297744"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>Metadados do parâmetro com valor de tabela para instruções preparadas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Um aplicativo pode obter metadados para uma chamada de procedimento preparada através de SQLNumParams e SQLDescribeParam. Para parâmetros avaliados em tabela, *o DataTypePtr* está definido como SQL_SS_TABLE. Metadados adicionais estão disponíveis através do SQLGetDescField para SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME e SQL_CA_SS_SCHEMA_NAME.  
  
 SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME e SQL_CA_SS_SCHEMA_NAME podem ser usados com Colunas SQL para obter metadados de coluna para tipos de tabela associados a parâmetros de valor de tabela. Neste caso, SQL_SOPT_SS_NAME_SCOPE devem ser definidas para SQL_SS_NAME_SCOPE_TABLE_TYPE antes que as Colunas SQL sejam chamadas. SQL_SOPT_SS_NAME_SCOPE deve ser definido novamente com o valor padrão, SQL_SS_NAME_SCOPE_TABLE, quando o aplicativo concluir a recuperação de metadados da coluna do parâmetro com valor de tabela.  
  
 SQL_CA_SS_TYPE_NAME , SQL_CA_SS_CATALOG_NAME e SQL_CA_SS_SCHEMA_NAME também podem ser usados com parâmetros de tipo de dado CLR definido pelo usuário.  
  
 Você não pode obter metadados de parâmetro com valor de tabela para instruções preparadas que não são chamadas de procedimento armazenado. Se você tentar fazer isto, o aplicativo retornará SQL_ERROR com SQLSTATE 42000 e a mensagem "Erro de sintaxe ou violação de acesso".  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros avaliados em tabela &#40;&#41;o ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
