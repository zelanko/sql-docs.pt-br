---
title: Preparar e executar uma instrução (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statement execution
- statement preparation
ms.assetid: 0adecc63-4da5-486c-bc48-09a004a2fae6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcc1f6d1542928d534d31c6d64ef6130c0c7e04b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63200395"
---
# <a name="prepare-and-execute-a-statement-odbc"></a>Preparar e executar uma instrução (ODBC)
    
### <a name="to-prepare-a-statement-once-and-then-execute-it-multiple-times"></a>Para preparar uma instrução uma vez e, depois, executá-la várias vezes  
  
1.  Chame a [Função SQL Prepare](https://go.microsoft.com/fwlink/?LinkId=59360) para preparar a instrução.  
  
2.  Opcionalmente, chame [SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) para determinar o número de parâmetros na instrução preparada.  
  
3.  Opcionalmente, para cada parâmetro na instrução preparada:  
  
    -   Chame [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md) para obter informações de parâmetro.  
  
    -   Associe cada parâmetro a uma variável de programa usando [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md). Configure qualquer parâmetro de dados em execução.  
  
4.  Para cada execução de uma instrução preparada:  
  
    -   Se a instrução tiver marcadores de parâmetro, coloque os valores de dados no buffer de parâmetros associado.  
  
    -   Chame [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) para executar a instrução preparada.  
  
    -   Se forem usados parâmetros de entrada de dados em execução, [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) retornará SQL_NEED_DATA. Envie os dados em partes useo [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=58405) e [SQLPutData](../../native-client-odbc-api/sqlputdata.md).  
  
### <a name="to-prepare-a-statement-with-column-wise-parameter-binding"></a>Para preparar uma instrução com associação de parâmetro de coluna  
  
1.  Chame [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) para definir os seguintes atributos:  
  
    -   Defina SQL_ATTR_PARAMSET_SIZE como o número de conjuntos (S) de parâmetros.  
  
    -   Defina SQL_ATTR_PARAM_BIND_TYPE como SQL_PARAMETER_BIND_BY_COLUMN.  
  
    -   Defina o atributo SQL_ATTR_PARAMS_PROCESSED_PTR de forma que aponte para uma variável SQLUINTEGER que contém o número de parâmetros processados.  
  
    -   Defina SQL_ATTR_PARAMS_STATUS_PTR de forma que aponte para uma matriz[S] de variáveis SQLUSSMALLINT que contém indicadores de status de parâmetro.  
  
2.  Chame SQLPrepare para preparar a instrução.  
  
3.  Opcionalmente, chame [SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) para determinar o número de parâmetros na instrução preparada.  
  
4.  Opcionalmente, para cada parâmetro na instrução preparada, chame SQLDescribeParam para obter informações de parâmetro.  
  
5.  Para cada marcador de parâmetro:  
  
    -   Aloque uma matriz de S buffers de parâmetro para armazenar valores de dados.  
  
    -   Aloque uma matriz de S buffers de parâmetro para armazenar comprimentos de dados.  
  
    -   Chame SQLBindParameter para associar as matrizes de comprimento de dados e de valor de dados de parâmetro ao parâmetro de instrução.  
  
    -   Se o parâmetro for um parâmetro de imagem ou de texto de dados em execução, configure-o.  
  
    -   Se qualquer parâmetro de dados em execução for usado, configure-o.  
  
6.  Para cada execução de uma instrução preparada:  
  
    -   Coloque os S valores de dados e os S comprimentos de dados nas matrizes de parâmetros associadas.  
  
    -   Chame SQLExecute para executar a instrução preparada.  
  
    -   Se forem usados parâmetros de entrada de dados em execução, SQLExecute retornará SQL_NEED_DATA. Envie os dados em partes useo SQLParamData e SQLPutData.  
  
### <a name="to-prepare-a-statement-with-row-wise-bound-parameters"></a>Para preparar uma instrução com parâmetros associados de linha  
  
1.  Aloque uma matriz[S] de estruturas, onde S é o número de conjuntos de parâmetros. A estrutura tem um elemento para cada parâmetro e cada elemento tem duas partes:  
  
    -   A primeira parte é uma variável do tipo de dados apropriado que contém os dados de parâmetro.  
  
    -   A segunda parte é uma variável SQLINTEGER que contém o indicador de status.  
  
2.  Chame [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) para definir os seguintes atributos:  
  
    -   Defina SQL_ATTR_PARAMSET_SIZE como o número de conjuntos (S) de parâmetros.  
  
    -   Defina SQL_ATTR_PARAM_BIND_TYPE como o tamanho da estrutura alocada na Etapa 1.  
  
    -   Defina o atributo SQL_ATTR_PARAMS_PROCESSED_PTR de forma que aponte para uma variável SQLUINTEGER que contém o número de parâmetros processados.  
  
    -   Defina SQL_ATTR_PARAMS_STATUS_PTR de forma que aponte para uma matriz[S] de variáveis SQLUSSMALLINT que contém indicadores de status de parâmetro.  
  
3.  Chame SQLPrepare para preparar a instrução.  
  
4.  Para cada marcador de parâmetro, chame SQLBindParameter para apontar o valor de dados de parâmetro e o ponteiro de comprimento de dados para suas variáveis no primeiro elemento da matriz de estruturas alocada na etapa 1. Se o parâmetro for um parâmetro de dados em execução, configure-o.  
  
5.  Para cada execução de uma instrução preparada:  
  
    -   Preencha a matriz de buffers de parâmetros associada com valores de dados.  
  
    -   Chame SQLExecute para executar a instrução preparada. O driver executa, com eficiência, a instrução SQL S vezes, uma vez para cada conjunto de parâmetros.  
  
    -   Se forem usados parâmetros de entrada de dados em execução, SQLExecute retornará SQL_NEED_DATA. Envie os dados em partes useo SQLParamData e SQLPutData.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre como executar consultas &#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
