---
title: Prevendo erros | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b7642e4dabebe3db00cb4852d2efea43269cef8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="anticipating-errors"></a>Antecipando a erros
Prevenção de erro é pelo menos tão importante quanto o tratamento de erros. Esta seção final contém uma lista curta de precauções que seu aplicativo pode fazer para ajudar a tornar menos prováveis de erros.  
  
 Verifique o estado dos objetos verificando o valor de **estado** propriedade antes de tentar executar uma operação usando esses objetos. Por exemplo, se seu aplicativo usa um global **Conexão**, verifique seu **estado** propriedade para ver se ele já está aberto antes de chamar o **abrir** método.  
  
-   Qualquer programa que aceita dados de um usuário deve incluir o código para validar os dados antes de enviá-la para o repositório de dados. Você não pode depender o repositório de dados, o provedor, ADO ou até mesmo a linguagem de programação para notificá-lo de problemas. Você deve verificar cada byte inserido pelos usuários, certificando-se de que os dados são do tipo correto para seu campo e os campos obrigatórios não estão vazios.  
  
 Verifique os dados antes de tentar gravar todos os dados para o armazenamento de dados. A maneira mais fácil de fazer isso é manipular o **WillMove** evento ou **WillUpdateRecordset** eventos. Para obter uma discussão mais completa de manipulação de eventos de ADO, consulte [manipulando eventos de ADO](../../../ado/guide/data/handling-ado-events.md).  
  
 Verifique se **registros** objetos não estão além dos limites do **registros** antes de tentar mover o ponteiro do registro. Se você tentar **MoveNext** quando **EOF** é True ou **MovePrev** quando **BOF** for True, ocorrerá um erro. Se você executar qualquer uma da **mover** métodos quando ambos **EOF** e **BOF** for True, será gerado um erro.  
  
 Erros também ocorrerão se você tentar executar operações como **busca** e **localizar** em vazio **registros**.
