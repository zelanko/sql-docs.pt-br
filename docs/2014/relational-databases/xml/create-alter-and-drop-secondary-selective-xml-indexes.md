---
title: Criar, alterar e remover índices XML seletivos secundários | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e1b85ab8b80a8c488c768ace365ca1a3478a609e
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889222"
---
# <a name="create-alter-and-drop-secondary-selective-xml-indexes"></a>Criar, alterar e remover índices XML seletivos secundários
  Descreve como criar um novo índice XML seletivo secundário, ou como alterar ou remover um índice XML seletivo secundário.  
  
##  <a name="create"></a> Criando um índice XML seletivo secundário  
  
### <a name="how-to-create-a-secondary-selective-xml-index"></a>Como: Criar um índice XML seletivo secundário  
 **Criar um índice XML seletivo secundário usando Transact-SQL**  
 Crie um índice XML seletivo secundário chamando a instrução CREATE XML INDEX. Para obter mais informações, consulte [CREATE XML INDEX &#40;índices XML seletivos&#41;] (~ / t-sql/statements/create-xml-index-selective-xml-indexes.  
  
 **Exemplo**  
  
 O exemplo a seguir cria um índice XML seletivo secundário no caminho `'pathabc'`. O caminho para o índice é identificado pelo nome atribuído a ele quando ele foi criado com a instrução CREATE SELECTIVE XML INDEX. Para obter mais informações, veja [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-selective-xml-index-transact-sql).  
  
```tsql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="alter"></a> Alterando um índice XML seletivo secundário  
 A instrução ALTER não oferece suporte a índices XML secundários seletivos. Para alterar um índice XML secundário, remova o índice existente e recrie-o.  
  
### <a name="how-to-alter-a-secondary-selective-xml-index"></a>Como: Alterar um índice XML seletivo secundário  
 **Alterar um índice XML seletivo secundário usando Transact-SQL**  
 1.  Remova o índice XML seletivo secundário existente chamando a instrução DROP INDEX. Para obter mais informações, veja [DROP INDEX &#40;Índices XML Seletivos&#41;](../indexes/indexes.md).  
  
2.  Recrie o índice com as opções desejadas chamando a instrução CREATE XML INDEX. Para obter mais informações, consulte [CREATE XML INDEX &#40;índices XML seletivos&#41;] (~ / t-sql/statements/create-xml-index-selective-xml-indexes.  
  
 **Exemplo**  
  
 O exemplo a seguir altera um índice XML seletivo secundário removendo-o e recriando-o.  
  
```tsql  
DROP INDEX filt_sxi_index_c  
  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="drop"></a> Removendo um índice XML seletivo secundário  
  
### <a name="how-to-drop-a-secondary-selective-xml-index"></a>Como: Remover um índice XML seletivo secundário  
 **Remover um índice XML seletivo secundário usando Transact-SQL**  
 Remova um índice XML seletivo secundário chamando a instrução DROP INDEX. Para obter mais informações, veja [DROP INDEX &#40;Índices XML Seletivos&#41;](../indexes/indexes.md).  
  
 **Exemplo**  
  
 O exemplo a seguir mostra uma instrução DROP INDEX.  
  
```tsql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
  
## <a name="see-also"></a>Consulte também  
 [Índices XML Seletivos &#40;SXI&#41;](selective-xml-indexes-sxi.md)  
  
  
