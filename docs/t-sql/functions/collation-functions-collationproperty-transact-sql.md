---
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 842c70125c5d311f36df50afa72feae47c47bd55
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68064709"
---
# <a name="collation-functions---collationproperty-transact-sql"></a>Funções de ordenação – COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Essa função retorna a propriedade solicitada de uma ordenação especificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>Argumentos  
*collation_name*  
O nome da ordenação. O argumento *collation_name* tem um tipo de dados **nvarchar (128)** sem nenhum valor padrão.
  
*property*  
A propriedade Collation. O argumento *property* tem um tipo de dados **varchar (128)** e pode ter qualquer um dos seguintes valores:
  
|Nome da propriedade|DESCRIÇÃO|  
|---|---|
|**CodePage**|Página de código de não Unicode da ordenação. É o conjunto de caracteres usado para dados **varchar**. Veja o [Apêndice G: Tabelas de mapeamento do DBCS/Unicode](https://msdn.microsoft.com/library/cc194886.aspx) e o [Apêndice H: Páginas de código](https://msdn.microsoft.com/library/cc195051.aspx) para converter esses valores e ver seus mapeamentos de caracteres.<br /><br />Tipo de dados base: **int**|  
|**LCID**|ID de localidade do Windows da ordenação. É a cultura usada para regras de classificação e comparação. Veja a [Estrutura de LCID](https://msdn.microsoft.com/library/cc233968.aspx) para converter esses valores (você precisará converter **varbinary** primeiro).<br /><br />Tipo de dados base: **int**|  
|**ComparisonStyle**|Estilo de comparação da ordenação do Windows. Retorna 0 para ordenações primárias – (\_BIN) e (\_BIN2) – bem como quando todas as propriedades são confidenciais – (\_CS\_AS\_KS\_WS), (\_CS\_AS\_KS\_WS\_SC) e (\_CS\_AS\_KS\_WS\_VSS). Valores de bitmask:<br /><br /> Ignorar maiúsculas e minúsculas: 1<br /><br /> Ignorar acento: 2<br /><br /> Ignorar Kana: 65536<br /><br /> Ignorar largura: 131072<br /><br /> Observação: a opção \_VSS (seletor sensível à variação) não é representada nesse valor, embora afete o comportamento da comparação.<br /><br />Tipo de dados base: **int**|  
|**Versão**|A versão da ordenação. Retorna um valor entre 0 e 3.<br /><br /> Ordenações com "140" no nome retornam 3.<br /><br /> Ordenações com "100" no nome retornam 2.<br /><br /> Ordenações com "90" no nome retornam 1.<br /><br /> Todas as outras ordenações retornam 0.<br /><br />Tipo de dados base: **tinyint**|  
  
## <a name="return-types"></a>Tipos de retorno
**sql_variant**
  
## <a name="examples"></a>Exemplos  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>Confira também
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  

