---
title: Propriedades do banco de dados (página Controle de Alterações) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.changetracking.f1
ms.assetid: 9b929640-bc62-449b-9b06-b5a77b8cf372
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 926f6227d5a3a2e11dffbf4b9f080b1fc5ec35a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62871849"
---
# <a name="database-properties-changetracking-page"></a>Propriedades do Banco de Dados (página Controle de Alterações)
  Use essa página para exibir ou modificar configurações de controle de alterações para o banco de dados selecionado. Para obter mais informações sobre as opções disponíveis nessa página, veja [Habilitar e desabilitar o controle de alterações &#40;SQL Server&#41;](../track-changes/enable-and-disable-change-tracking-sql-server.md).  
  
## <a name="options"></a>Opções  
 **Controle de alterações**  
 Use para habilitar ou desabilitar o controle de alterações para o banco de dados.  
  
 Para habilitar o controle de alterações, deve-se ter permissão para modificar o banco de dados.  
  
 Definindo-se o valor como **Verdadeiro** define-se uma opção de banco de dados que permite que o controle de alterações seja habilitado em tabelas individuais.  
  
 Pode-se também configurar o controle de alterações usando [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql).  
  
 **Período de Retenção**  
 Especifica o período mínimo para manter informações de controle de alterações no banco de dados. Os dados serão removidos somente se o valor **Auto Clean-Up**for **True**.  
  
 O valor padrão é 2.  
  
 **Unidades de Período de Retenção**  
 Especifica as unidades para o valor de período de retenção. Pode-se selecionar **Dias**, **Horas**ou **Minutos**. O valor padrão é **Dias**.  
  
 O período de retenção mínimo é de 1 minuto. Não há um período máximo de retenção.  
  
 **Auto Clean-Up**  
 Indica se as informações de controle de alterações são automaticamente removidas depois do período de retenção especificado.  
  
 Habilitar a opção **Auto Clean-Up** redefine qualquer período de retenção personalizado anterior ao período de retenção padrão de 2 dias.  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
