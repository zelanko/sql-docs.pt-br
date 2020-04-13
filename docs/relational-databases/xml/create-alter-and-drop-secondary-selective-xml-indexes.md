---
title: Criar, alterar e remover índice XML seletivo secundário | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: f86ff1eb81984414afaee99bd8fc76525825c219
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664618"
---
# <a name="create-alter-and-drop-secondary-selective-xml-indexes"></a>Criar, alterar e remover índices XML seletivos secundários
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Descreve como criar um novo índice XML seletivo secundário, ou como alterar ou remover um índice XML seletivo secundário.  
  
##  <a name="creating-a-secondary-selective-xml-index"></a><a name="create"></a> Criando um índice XML seletivo secundário  
  
### <a name="how-to-create-a-secondary-selective-xml-index"></a>Como: Criar um índice XML seletivo secundário  
 **Criar um índice XML seletivo secundário usando Transact-SQL**  
 Crie um índice XML seletivo secundário chamando a instrução CREATE XML INDEX. Para obter mais informações, veja [CREATE XML INDEX &#40;Índices XML Seletivos&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
 **Exemplo**  
  
 O exemplo a seguir cria um índice XML seletivo secundário no caminho `'pathabc'`. O caminho para o índice é identificado pelo nome atribuído a ele quando ele foi criado com a instrução CREATE SELECTIVE XML INDEX. Para obter mais informações, veja [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
```sql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="altering-a-secondary-selective-xml-index"></a><a name="alter"></a> Alterando um índice XML seletivo secundário  
 A instrução ALTER não oferece suporte a índices XML secundários seletivos. Para alterar um índice XML secundário, remova o índice existente e recrie-o.  
  
### <a name="how-to-alter-a-secondary-selective-xml-index"></a>Como: Alterar um índice XML seletivo secundário  
 **Alterar um índice XML seletivo secundário usando Transact-SQL**  
 1.  Remova o índice XML seletivo secundário existente chamando a instrução DROP INDEX. Para obter mais informações, veja [DROP INDEX &#40;Índices XML Seletivos&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md).  
  
2.  Recrie o índice com as opções desejadas chamando a instrução CREATE XML INDEX. Para obter mais informações, veja [CREATE XML INDEX &#40;Índices XML Seletivos&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
 **Exemplo**  
  
 O exemplo a seguir altera um índice XML seletivo secundário removendo-o e recriando-o.  
  
```sql  
DROP INDEX filt_sxi_index_c  
  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="dropping-a-secondary-selective-xml-index"></a><a name="drop"></a> Removendo um índice XML seletivo secundário  
  
### <a name="how-to-drop-a-secondary-selective-xml-index"></a>Como: Remover um índice XML seletivo secundário  
 **Remover um índice XML seletivo secundário usando Transact-SQL**  
 Remova um índice XML seletivo secundário chamando a instrução DROP INDEX. Para obter mais informações, veja [DROP INDEX &#40;Índices XML Seletivos&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md).  
  
 **Exemplo**  
  
 O exemplo a seguir mostra uma instrução DROP INDEX.  
  
```sql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
  
## <a name="see-also"></a>Consulte Também  
 [Índices XML Seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
