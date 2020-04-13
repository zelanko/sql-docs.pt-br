---
title: Modificar índices XML | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML indexes [SQL Server], modifying
- modifying indexes
ms.assetid: 24d50fe1-c6ec-49e6-91a3-9791851ba53d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: efe1b72c4cb98b51da065b8194432f4e8d9efa61
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665081"
---
# <a name="modify-xml-indexes"></a>Modificar índices XML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A instrução DDL [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] pode ser usada para modificar o XML existente e índices não XML. Porém, nem todas as opções de ALTER INDEX estão disponíveis para índices XML. As opções a seguir não são válidas ao modificar índices XML:  
  
-   A opção de recriação e definição IGNORE_DUP_KEY não é válida para índices XML. O opção de reconstrução ONLINE deve ser definida como OFF para índices XML secundários. O opção DROP_EXISTING não é permitida na instrução ALTER INDEX.  
  
-   As modificações de restrição de chave primária na tabela do usuário não são propagadas automaticamente para índices XML. O usuário deve descartar os índices XML primeiro e recriá-los.  
  
-   Se ALTER INDEX ALL for especificado, ele se aplicará a índices XML e não XML. Podem ser especificadas opções de indexação que não são válidas para os dois tipos de índices. Nesse caso, há falha em toda a instrução.  
  
## <a name="example-modifying-an-xml-index"></a>Exemplo: Modificando um índice XML  
 No exemplo a seguir, um índice XML é criado e, em seguida, modificado definindo a opção `ALLOW_ROW_LOCKS` como `OFF`. Quando `ALLOW_ROW_LOCKS` está `OFF`, as linhas não são bloqueadas e o acesso aos índices especificados é obtido usando bloqueios em nível de página e de tabela.  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create primary XML index.   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
  
-- Modify and set an index option.  
ALTER INDEX PIdx_T_XmlCol on T   
SET (ALLOW_ROW_LOCKS = OFF)  
```  
  
## <a name="example-disabling-and-enabling-an-xml-index"></a>Exemplo: Desabilitando e ativando um índice XML  
 Por padrão, um índice XML está habilitado. Se um índice XML for desabilitado, as consultas executadas na coluna XML não usarão o índice XML. Para habilitar um índice XML, use `ALTER INDEX` com a opção `REBUILD` .  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol ON T(XmlCol)  
GO  
ALTER INDEX PIdx_T_XmlCol on T DISABLE  
Go  
-- Verify index is disabled.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
-- Rebuild the index.  
ALTER INDEX PIdx_T_XmlCol on T REBUILD  
Go  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
