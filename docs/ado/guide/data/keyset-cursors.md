---
title: Cursores keyset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b349838788a3c442ea9c32fc5b8a7ebbd0240e37
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702091"
---
# <a name="keyset-cursors"></a>Cursores do conjunto de chaves
O cursor de conjunto de chaves fornece a funcionalidade entre um estático e um cursor dinâmico em sua capacidade de detectar alterações. Como um cursor estático, ele nem sempre detecta alterações à associação e à ordem do conjunto de resultados. Como um cursor dinâmico, ele detecta alterações aos valores de linhas no conjunto de resultados.  
  
 Os cursores controlados por conjuntos de chaves são controlados por um conjunto exclusivo de identificadores (chaves) conhecido como conjunto de chaves. As chaves são criadas a partir de um conjunto de colunas, que identificam exclusivamente as linhas no conjunto de resultados. O conjunto de chaves é o conjunto de valores de chave de todas as linhas retornadas pela instrução de consulta.  
  
 Com cursores controlados por conjunto de chaves, uma chave é criada e salva para cada linha do cursor e armazenada na estação de trabalho cliente ou no servidor. Quando você acessa cada linha, a chave armazenada é usada para buscar os valores de dados atual da fonte de dados. Em um cursor controlado por conjunto de chaves, a associação do conjunto de resultados é congelada quando o conjunto de chaves está completamente preenchido. Depois disso, adições ou atualizações que afetem a associação não farão parte do resultado definido até que ele seja reaberto.  
  
 Alterações nos valores de dados (feitas por outros processos ou o proprietário do conjunto de chaves) são visíveis como o usuário rola pelo conjunto de resultados. Inserções feitas fora do cursor (por outros processos) serão visíveis apenas se o cursor for fechado e reaberto. Inserções feitas de dentro do cursor são visíveis no final do conjunto de resultados.  
  
 Quando um cursor controlado por tenta recuperar uma linha que foi excluída, a linha é exibida como uma "brecha" no conjunto de resultados. A chave para a linha existe no conjunto de chaves, mas a linha não existe mais no conjunto de resultados. Se os valores de chave em uma linha forem atualizados, a linha é considerada foi excluído e, em seguida, inserida, para que essas linhas também aparecem como brechas no conjunto de resultados. Enquanto um cursor controlado por sempre pode detectar linhas excluídas por outros processos, ele pode, opcionalmente, remover as chaves para excluir a próprio de linhas. Cursores controlados por que isso não é possível detectar suas próprias exclusões porque a evidência foi removida.  
  
 Uma atualização para uma coluna de chave funciona como uma exclusão da chave antiga, seguida por uma inserção da nova chave. O novo valor de chave não é visível se a atualização não foi realizada pelo cursor. Se a atualização foi feita por meio do cursor, o novo valor de chave está visível no final do conjunto de resultados.  
  
 Há uma variação em cursores controlados por chamados de cursores controlados por cursores padrão. Em um cursor padrão controlado por conjunto de chaves, a associação de linhas no conjunto de resultados e a ordem das linhas são fixos no tempo de abertura do cursor, mas as alterações aos valores que são realizadas pelo proprietário do cursor e as alterações confirmadas feitas por outros processos estão visíveis. Se uma alteração desqualifica uma linha para a associação ou afeta a ordem de uma linha, a linha não desaparecem ou mover, a menos que o cursor for fechado e reaberto. Dados inseridos não aparecem, mas as alterações nos dados existentes aparecem como as linhas sejam buscadas.  
  
 O cursor controlado por conjunto de chaves é difícil de usar corretamente porque a sensibilidade a alterações de dados depende de muitas circunstâncias diferentes, conforme descrito acima. No entanto, se seu aplicativo não está preocupado com atualizações simultâneas, por meio de programação pode lidar com chaves ruins e deve acessar diretamente a determinadas linhas com chave, o cursor controlado por conjunto de chaves pode funcionar para você. Use o **adOpenKeyset CursorTypeEnum** para indicar que você deseja usar um cursor keyset no ADO.  
  
## <a name="see-also"></a>Consulte também  
 [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
