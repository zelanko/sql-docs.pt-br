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
author: rothja
ms.author: jroth
ms.openlocfilehash: f28a6dc9d79ba59229609cbde94642e31274b9eb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761252"
---
# <a name="anticipating-errors"></a>Antecipar erros
A prevenção de erros é pelo menos tão importante quanto o tratamento de erros. Esta seção final contém uma pequena lista de precauções que seu aplicativo pode tomar para ajudar a tornar os erros menos prováveis.  
  
 Verifique o estado dos objetos verificando o valor na propriedade **State** antes de tentar executar uma operação usando esses objetos. Por exemplo, se seu aplicativo usar uma **conexão**global, verifique sua propriedade de **estado** para ver se ela já está aberta antes de chamar o método **Open** .  
  
-   Qualquer programa que aceite dados de um usuário deve incluir o código para validar esses dados antes de enviá-los para o armazenamento de dados. Você não pode contar com o armazenamento de dados, o provedor, o ADO ou até mesmo sua linguagem de programação para notificá-lo de problemas. Você deve verificar cada byte inserido por seus usuários, verificando se os dados são do tipo correto para seu campo e se os campos obrigatórios não estão vazios.  
  
 Verifique os dados antes de tentar gravar dados no armazenamento de dados. A maneira mais fácil de fazer isso é manipular o evento **WillMove** ou o evento **WillUpdateRecordset** . Para obter uma discussão mais completa sobre como lidar com eventos ADO, consulte [manipulando eventos ADO](../../../ado/guide/data/handling-ado-events.md).  
  
 Verifique se os objetos **Recordset** não estão além dos limites do **conjunto de registros** antes de tentar mover o ponteiro de registro. Se você tentar **MoveNext** quando **EOF** for true ou **MovePrev** quando **BOF** for true, ocorrerá um erro. Se você executar qualquer um dos métodos de **movimentação** quando **EOF** e **BOF** forem verdadeiros, um erro será gerado.  
  
 Os erros também ocorrerão se você tentar executar operações como **Seek** e **Find** em um conjunto de **registros**vazio.
