---
title: Antecipando erros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91741ef8d6b0f7f984958837df3234b0bbc1e009
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727334"
---
# <a name="anticipating-errors"></a>Antecipar erros
Prevenção de erro é pelo menos tão importante quanto o tratamento de erros. Nesta seção final contém uma lista curta de precauções de que seu aplicativo pode adotar para ajudar a tornar erros menor probabilidade de ocorrer.  
  
 Verificar o estado dos objetos verificando o valor de **estado** propriedade antes de tentar executar uma operação usando esses objetos. Por exemplo, se seu aplicativo usa um global **Conexão**, verifique suas **estado** propriedade para ver se ele já está aberto antes de chamar o **abrir** método.  
  
-   Qualquer programa que aceita dados de um usuário deve incluir o código para validar que os dados antes de enviá-la para o armazenamento de dados. Você não pode contar o armazenamento de dados, o provedor, ADO ou até mesmo a linguagem de programação para notificá-lo de problemas. Você deve verificar cada byte inserido pelos usuários, certificando-se de que os dados são o tipo correto para seu campo e os campos obrigatórios não estão vazios.  
  
 Verifique os dados antes de tentar gravar dados no armazenamento de dados. A maneira mais fácil de fazer isso é lidar com o **eventos WillMove** eventos ou o **WillUpdateRecordset** eventos. Para obter uma discussão mais completa de manipulação de eventos ADO, consulte [manipulação de eventos ADO](../../../ado/guide/data/handling-ado-events.md).  
  
 Certifique-se de que **conjunto de registros** objetos não forem além dos limites do **Recordset** antes de tentar mover o ponteiro de registro. Se você tentar **MoveNext** quando **EOF** for True ou **MovePrev** quando **BOF** for True, ocorrerá um erro. Se você executar qualquer uma da **mova** métodos quando ambos **EOF** e **BOF** forem True, um erro será gerado.  
  
 Erros também ocorrerá se você tentar executar operações, como **Seek** e **localizar** em um vazio **conjunto de registros**.
