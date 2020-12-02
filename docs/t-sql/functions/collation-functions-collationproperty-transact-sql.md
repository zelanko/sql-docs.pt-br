---
description: Funções de ordenação – COLLATIONPROPERTY (Transact-SQL)
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COLLATIONPROPERTY_TSQL
- COLLATIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], properties
- COLLATIONPROPERTY function
ms.assetid: f5029e74-a1db-4f69-b0f5-5ee920c3311d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7cd3bfc9b136dac41352d2be594e7d1e3099bd37
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96118935"
---
# <a name="collation-functions---collationproperty-transact-sql"></a>Funções de ordenação – COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Essa função retorna a propriedade solicitada de uma ordenação especificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
COLLATIONPROPERTY( collation_name , property )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*collation_name*  
O nome da ordenação. O argumento *collation_name* tem um tipo de dados **nvarchar (128)** sem nenhum valor padrão.
  
*property*  
A propriedade Collation. O argumento *property* tem um tipo de dados **varchar (128)** e pode ter qualquer um dos seguintes valores:
  
|Nome da propriedade|Descrição|  
|---|---|
|**CodePage**|Página de código de não Unicode da ordenação. É o conjunto de caracteres usado para dados **varchar**. Veja o [Apêndice G: Tabelas de mapeamento do DBCS/Unicode](/previous-versions/cc194886(v=msdn.10)) e o [Apêndice H: Páginas de código](/previous-versions/cc195051(v=msdn.10)) para converter esses valores e ver seus mapeamentos de caracteres.<br /><br />Tipo de dados base: **int**|  
|**LCID**|ID de localidade do Windows da ordenação. É a cultura usada para regras de classificação e comparação. Veja a [Estrutura de LCID](/openspecs/windows_protocols/ms-lcid/63d3d639-7fd2-4afb-abbe-0d5b5551eef8) para converter esses valores (você precisará converter **varbinary** primeiro).<br /><br />Tipo de dados base: **int**|  
|**ComparisonStyle**|Estilo de comparação da ordenação do Windows. Retorna 0 para ordenações primárias – (\_BIN) e (\_BIN2) – bem como quando todas as propriedades são confidenciais – (\_CS\_AS\_KS\_WS), (\_CS\_AS\_KS\_WS\_SC) e (\_CS\_AS\_KS\_WS\_VSS). Valores de bitmask:<br /><br /> Ignorar maiúsculas e minúsculas: 1<br /><br /> Ignorar acento: 2<br /><br /> Ignorar Kana: 65536<br /><br /> Ignorar largura: 131072<br /><br /> Observação: a opção \_VSS (seletor sensível à variação) não é representada nesse valor, embora afete o comportamento da comparação.<br /><br />Tipo de dados base: **int**|  
|**Versão**|A versão da ordenação. Retorna um valor entre 0 e 3.<br /><br /> Ordenações com "140" no nome retornam 3.<br /><br /> Ordenações com "100" no nome retornam 2.<br /><br /> Ordenações com "90" no nome retornam 1.<br /><br /> Todas as outras ordenações retornam 0.<br /><br />Tipo de dados base: **tinyint**|  
  
## <a name="return-types"></a>Tipos de retorno
**sql_variant**
  
## <a name="examples"></a>Exemplos  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
1252   
```  
  
## <a name="see-also"></a>Confira também
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
