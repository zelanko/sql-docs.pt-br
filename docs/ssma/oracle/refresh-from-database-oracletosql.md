---
title: Atualização do banco de dados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: decc6e25cc8480dfaf041a79baa0972bdd78e569
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62625856"
---
# <a name="refresh-from-database-oracletosql"></a>Atualização do banco de dados (OracleToSQL)
O **Refresh do banco de dados** caixa de diálogo permite que você selecione quais objetos de atualização do banco de dados Oracle. Linhas na caixa de diálogo são codificadas por cores com base no estado de metadados:  
  
-   Se os metadados do objeto foi alterado localmente e no banco de dados Oracle, a linha é azul.  
  
-   Se os metadados do objeto foi alterado no banco de dados Oracle, mas não no SSMA, a linha será amarela.  
  
-   Se os metadados do objeto foi alterado localmente, mas não no banco de dados Oracle, a linha está verde.  
  
-   Se o objeto é novo no banco de dados Oracle, a linha é rosa.  
  
Você pode especificar configurações de atualização do objeto padrão no **configurações do projeto** caixa de diálogo. Para obter mais informações, consulte [configurações do projeto&#40;sincronização&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
Para acessar o **atualização do banco de dados** caixa de diálogo, clique com botão direito um objeto no Gerenciador de metadados do Oracle e clique em **atualização do banco de dados**.  
  
## <a name="options"></a>Opções  
**Recolher (-)**  
Recolha todos os grupos de objeto para ocultar objetos individuais.  
  
**Expandir (+)**  
Expanda todos os grupos de objeto para mostrar objetos individuais.  
  
**Ocultar/Mostrar objetos iguais**  
Oculta os objetos da lista se os metadados do objeto são o mesmo no banco de dados Oracle e do SSMA.  
  
**Atualização do banco de dados (botão de seta)**  
Use o botão de seta para especificar que os metadados para os objetos selecionados devem ser atualizados no SSMA.  
  
**Fazer a atualização não do banco de dados (botão X)**  
Use o botão X para especificar os metadados para os objetos selecionados não devem ser atualizados no SSMA.  
  
**Legenda**  
Exibe uma **legenda** caixa de diálogo. A legenda contém o mapeamento entre os estados de metadados e as cores de linha.  
  
Para manter o **legenda** caixa de diálogo, na parte superior das **atualização do banco de dados** caixa de diálogo, selecione o **Mostrar na parte superior** caixa de seleção.  
  
