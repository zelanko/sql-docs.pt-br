---
title: "Criar, alterar e remover &#237;ndices XML seletivos secund&#225;rios | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 7
---
# Criar, alterar e remover &#237;ndices XML seletivos secund&#225;rios
  Descreve como criar um novo índice XML seletivo secundário, ou como alterar ou remover um índice XML seletivo secundário.  
  
##  <a name="create"></a> Criando um índice XML seletivo secundário  
  
### Como: Criar um índice XML seletivo secundário  
 **Criar um índice XML seletivo secundário usando Transact-SQL**  
 Crie um índice XML seletivo secundário chamando a instrução CREATE XML INDEX. Para obter mais informações, veja [CREATE XML INDEX &#40;Índices XML Seletivos&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
 **Exemplo**  
  
 O exemplo a seguir cria um índice XML seletivo secundário no caminho `'pathabc'`. O caminho para o índice é identificado pelo nome atribuído a ele quando ele foi criado com a instrução CREATE SELECTIVE XML INDEX. Para obter mais informações, veja [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
```tsql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
 [Neste tópico](#top)  
  
##  <a name="alter"></a> Alterando um índice XML seletivo secundário  
 A instrução ALTER não oferece suporte a índices XML secundários seletivos. Para alterar um índice XML secundário, remova o índice existente e recrie-o.  
  
### Como: Alterar um índice XML seletivo secundário  
 **Alterar um índice XML seletivo secundário usando Transact-SQL**  
 1.  Remova o índice XML seletivo secundário existente chamando a instrução DROP INDEX. Para obter mais informações, veja [DROP INDEX &#40;Índices XML Seletivos&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md).  
  
2.  Recrie o índice com as opções desejadas chamando a instrução CREATE XML INDEX. Para obter mais informações, veja [CREATE XML INDEX &#40;Índices XML Seletivos&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
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
  
 [Neste tópico](#top)  
  
##  <a name="drop"></a> Removendo um índice XML seletivo secundário  
  
### Como: Remover um índice XML seletivo secundário  
 **Remover um índice XML seletivo secundário usando Transact-SQL**  
 Remova um índice XML seletivo secundário chamando a instrução DROP INDEX. Para obter mais informações, veja [DROP INDEX &#40;Índices XML Seletivos&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md).  
  
 **Exemplo**  
  
 O exemplo a seguir mostra uma instrução DROP INDEX.  
  
```tsql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
 [Neste tópico](#top)  
  
## Consulte também  
 [Índices XML Seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  