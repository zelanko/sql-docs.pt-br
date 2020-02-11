---
title: Modificar índices XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML indexes [SQL Server], modifying
- modifying indexes
ms.assetid: 24d50fe1-c6ec-49e6-91a3-9791851ba53d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67767ae7ec3bda62783281385333fef89481f45d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68195595"
---
# <a name="modify-xml-indexes"></a>Modificar índices XML
  A instrução DDL [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] pode ser usada para modificar o XML existente e índices não XML. Porém, nem todas as opções de ALTER INDEX estão disponíveis para índices XML. As opções a seguir não são válidas ao modificar índices XML:  
  
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
 [Índices XML &#40;SQL Server&#41;](xml-indexes-sql-server.md)  
  
  
