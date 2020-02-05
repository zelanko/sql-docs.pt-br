---
title: Usar a opção BINARY BASE64 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: eb192cdb9a7e9ffb43561b3b642f60144861c6df
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71199460"
---
# <a name="use-the-binary-base64-option"></a>Usar a opção BINARY BASE64

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

A opção BINARY BASE64 é especificada na consulta. Os dados binários são retornados no formato de codificação na base64.

Se a opção BINARY BASE64 não for especificada na consulta, o modo AUTO, por padrão, oferecerá suporte à codificação de URL de dados binários. Uma referência a uma URL relativa para a raiz virtual do banco de dados é retornada. Essa referência é para o banco de dados em que a consulta foi executada. A referência retornada pode ser usada para acessar os dados binários reais em operações subsequentes. Esse acesso é obtido usando a consulta a dbobject do SQLXML ISAPI. A consulta deve fornecer informações suficientes para identificar a imagem. Essas informações podem incluir as colunas da chave primária.

## <a name="column-alias"></a>Alias de coluna

Não use um alias para uma coluna binária ao consultar uma exibição e usar o modo FOR XML AUTO. Se você usar um alias, ele será retornado na codificação de URL dos dados binários. Em operações subsequentes, o alias não faz sentido. O alias sem sentido e a codificação de URL não podem ser usados para recuperar a imagem.

### <a name="cast-to-a-blob"></a>Converter em um BLOB

Em uma consulta SELECT, a conversão de qualquer coluna em um blob (objeto binário grande) torna a coluna uma entidade temporária. Sendo temporário, o blob perde seu nome de tabela e nome de coluna associados. Essa conversão faz com que as consultas em modo AUTO gerem um erro porque o sistema não sabe onde colocar esse valor na hierarquia XML.

Por exemplo, considere a tabela a seguir com sua única linha.

```sql
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)
INSERT INTO MyTable VALUES (1, 0x7);
```

A consulta a seguir produz um erro, causado pela conversão em um blob (objeto binário grande):

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO;
```

A solução é adicionar a opção BINARY BASE64 à cláusula FOR XML. Se você remover a conversão, a consulta produzirá bons resultados.

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO, BINARY BASE64;
```

Espere o seguinte bom resultado:

```console
<MyTable Col1="1" Col2="Bw==" />
```

## <a name="see-also"></a>Consulte Também

[Usar o modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)
