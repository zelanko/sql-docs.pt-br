---
title: Criar, alterar e remover índices XML seletivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c398f396-f630-4a2d-a264-f243c5346de1
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e8703669a5fb8a263452cc1dd1950ba895d88fad
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889892"
---
# <a name="create-alter-and-drop-selective-xml-indexes"></a>Criar, alterar e remover índices XML seletivos
  Descreve como criar um novo índice XML seletivo ou alterar ou remover um índice XML seletivo existente.  
  
 Para obter mais informações sobre índices XML seletivos, veja [Índices XML Seletivos &#40;SXI&#41;](selective-xml-indexes-sxi.md).  
  
##  <a name="create"></a> Criando um índice XML seletivo  
  
### <a name="how-to-create-a-selective-xml-index"></a>Como criar um índice XML seletivo  
 **Criar um índice XML seletivo usando Transact-SQL**  
 Crie um índice XML seletivo chamando a instrução CREATE SELECTIVE XML INDEX. Para obter mais informações, veja [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-selective-xml-index-transact-sql).  
  
 **Exemplo**  
  
 O exemplo a seguir mostra a sintaxe para criar um índice XML seletivo. Ele também mostra variações da sintaxe para descrever os caminhos a serem indexados, com dicas de otimização opcionais.  
  
```tsql  
CREATE SELECTIVE XML INDEX sxi_index  
ON Tbl(xmlcol)  
  
FOR(  
    pathab   = '/a/b' as XQUERY 'node()'  
    pathabc  = '/a/b/c' as XQUERY 'xs:double',   
    pathdtext = '/a/b/d/text()' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
    pathabe = '/a/b/e' as SQL NVARCHAR(100)  
)  
```  
  
  
  
##  <a name="alter"></a> Alterando um índice XML seletivo  
  
### <a name="how-to-alter-a-selective-xml-index"></a>Como alterar um índice XML seletivo  
 **Alterar um índice XML seletivo usando Transact-SQL**  
 Altere um índice XML seletivo existente chamando a instrução ALTER INDEX. Para obter mais informações, veja [ALTER INDEX &#40;Índices XML Seletivos&#41;](../indexes/indexes.md).  
  
 **Exemplo**  
  
 O exemplo a seguir mostra uma instrução ALTER INDEX. Essa instrução adiciona o caminho `'/a/b/m'` à parte XQuery do índice e exclui o caminho `'/a/b/e'` da parte SQL do índice criado no exemplo no tópico [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-selective-xml-index-transact-sql). O caminho a ser excluído é identificado pelo nome atribuído a ele quando foi criado.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
)  
```  
  
  
  
##  <a name="drop"></a> Removendo um índice XML seletivo  
  
### <a name="how-to-drop-a-selective-xml-index"></a>Como remover um índice XML seletivo  
 **Remover um índice XML seletivo usando Transact-SQL**  
 Remova um índice XML seletivo chamando a instrução DROP INDEX. Para obter mais informações, veja [DROP INDEX &#40;Índices XML Seletivos&#41;](/sql/t-sql/statements/drop-index-selective-xml-indexes).  
  
 **Exemplo**  
  
 O exemplo a seguir mostra uma instrução DROP INDEX.  
  
```tsql  
DROP INDEX sxi_index ON tbl  
```  
  
 
  
  
