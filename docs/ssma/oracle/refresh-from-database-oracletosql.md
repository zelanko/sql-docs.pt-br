---
title: Atualização do banco de dados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: a346119111cc876bfb794e5361a22a5cc51e593b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="refresh-from-database-oracletosql"></a>Atualização do banco de dados (OracleToSQL)
O **de atualização do banco de dados** caixa de diálogo permite que você selecione quais objetos para atualização do banco de dados Oracle. Linhas na caixa de diálogo estão codificados por cores com base no estado de metadados:  
  
-   Se os metadados do objeto foi alterado localmente e no banco de dados Oracle, a linha azul.  
  
-   Se os metadados do objeto foi alterado no banco de dados Oracle, mas não no SSMA, a linha é amarela.  
  
-   Se os metadados do objeto foi alterado localmente, mas não no banco de dados Oracle, a linha é verde.  
  
-   Se o objeto for novo no banco de dados Oracle, a linha é rosa.  
  
Você pode especificar as configurações padrão do objeto atualização o **configurações de projeto** caixa de diálogo. Para obter mais informações, consulte [configurações de projeto&#40;sincronização&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
Para acessar o **de atualização do banco de dados** caixa de diálogo, o botão direito do mouse, um objeto no Gerenciador de metadados do Oracle e clique em **de atualização do banco de dados**.  
  
## <a name="options"></a>Opções  
**Recolher (-)**  
Recolha todos os grupos de objeto para ocultar objetos individuais.  
  
**Expandir (+)**  
Expanda todos os grupos de objeto para mostrar os objetos individuais.  
  
**Mostrar/ocultar objetos iguais**  
Oculta os objetos da lista se os metadados do objeto são o mesmo no banco de dados Oracle e no SSMA.  
  
**Atualização do banco de dados (botão de seta)**  
Use o botão de seta para especificar que os metadados para os objetos selecionados devem ser atualizados em SSMA.  
  
**Fazer a atualização não do banco de dados (botão X)**  
Use o botão X para especificar que os metadados para os objetos selecionados não devem ser atualizados em SSMA.  
  
**Legenda**  
Exibe um **legenda** caixa de diálogo. A legenda contém o mapeamento entre as cores de linha e estados de metadados.  
  
Para manter o **legenda** caixa de diálogo sobre o **de atualização do banco de dados** caixa de diálogo, selecione o **Mostrar na parte superior** caixa de seleção.  
  
