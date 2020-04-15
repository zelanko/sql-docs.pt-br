---
title: Cursors orientados por keyset | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 814fca7d48f50aab51b6b4f7e34835be8c412e9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306201"
---
# <a name="keyset-driven-cursors"></a>Cursores controlados por conjunto de chaves
Um cursor orientado por chave fica entre um cursor estático e um cursor dinâmico em sua capacidade de detectar alterações. Como um cursor estático, ele nem sempre detecta alterações à associação e à ordem do conjunto de resultados. Como um cursor dinâmico, ele detecta alterações nos valores das linhas no conjunto de resultados (sujeito ao nível de isolamento da transação, conforme definido pelo atributo de conexão SQL_ATTR_TXN_ISOLATION).  
  
 Quando um cursor orientado por chaveé, ele salva as teclas para todo o conjunto de resultados; isso corrige a adesão aparente e a ordem do conjunto de resultados. À medida que o cursor percorre o conjunto de resultados, ele usa as teclas neste *conjunto de teclas* para recuperar os valores de dados atuais para cada linha. Por exemplo, suponha que um cursor orientado por keyset busque uma linha e outro aplicativo atualize essa linha. Se o cursor rebusca a linha, os valores que ele vê são os novos porque ele refetched a linha usando sua chave. Por causa disso, os cursores orientados por keyset sempre detectam alterações feitas por si mesmos e por outros.  
  
 Quando o cursor tenta recuperar uma linha que foi excluída, esta linha aparece como um "buraco" no conjunto de resultados: A chave para a linha existe no conjunto de chaves, mas a linha não existe mais no conjunto de resultados. Se os valores-chave em uma linha forem atualizados, a linha será considerada excluída e depois inserida, de modo que essas linhas também aparecem como furos no conjunto de resultados. Embora um cursor orientado por chave possa sempre detectar linhas excluídas por outros, ele pode, opcionalmente, remover as teclas para linhas que ele se exclua do conjunto de chaves. Os cursores orientados por chave que fazem isso não podem detectar suas próprias exclusões. Se um cursor específico orientado por chavedes detecta suas próprias exclusões é relatado através da opção SQL_STATIC_SENSITIVITY no **SQLGetInfo**.  
  
 As linhas inseridas por outros nunca são visíveis para um cursor orientado por chaves porque não existem teclas para essas linhas no conjunto de chaves. No entanto, um cursor orientado por chavepode adicionar opcionalmente as teclas para linhas que ele se insere no conjunto de chaves. Os cursores orientados por keyset que fazem isso podem detectar suas próprias inserções. Se um cursor específico orientado por chavedes detecta suas próprias inserções é relatado através da opção SQL_STATIC_SENSITIVITY no **SQLGetInfo**.  
  
 A matriz de status da linha especificada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO ou SQL_ROW_ERROR para qualquer linha. Ele retorna SQL_ROW_UPDATED, SQL_ROW_DELETED ou SQL_ROW_ADDED para linhas que detecta como atualizadas, excluídas ou inseridas.  
  
 Os cursores orientados por conjuntos de chaves são comumente implementados criando uma tabela temporária que contém as teclas para cada linha no conjunto de resultados. Como o cursor também deve determinar se as linhas foram atualizadas, esta tabela também contém uma coluna com informações de versão de linha.  
  
 Para percorrer o conjunto de resultados originais, o cursor orientado por keyset abre um cursor estático sobre a tabela temporária. Para recuperar uma linha no conjunto de resultados original, o cursor primeiro recupera a chave apropriada da tabela temporária e, em seguida, recupera os valores atuais para a linha. Se forem usados cursores de bloco, o cursor deve recuperar várias teclas e linhas.
