---
title: Consultar e atualizar dados do Visual FoxPro do Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- querying Visual FoxPro data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], querying and updating
- updating Visual FoxPro data [ODBC]
ms.assetid: 2d314e78-9edf-44b2-bd8b-96784236bcbe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1097e03c414d919a606ffd21ae50ffddf51173b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316757"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Consultar e atualizar dados do Visual FoxPro do Microsoft Access
Você pode consultar e atualizar os dados armazenados em um banco de dados do Visual FoxPro de um banco de dados do Microsoft Access usando a opção de tabela de vínculo.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Para vincular um banco de dados do Visual FoxPro para um banco de dados do Microsoft Access  
  
1.  Abra um banco de dados do Microsoft Access.  
  
2.  Na guia tabelas, clique em novo.  
  
3.  Na caixa de diálogo nova tabela, selecione o Link de tabela e clique em Okey.  
  
4.  Na caixa de diálogo de Link, selecione o banco de dados ODBC nos arquivos da lista de tipos.  
  
5.  Na caixa de diálogo de fontes de dados SQL, selecione a fonte de dados que se conecta aos dados do Visual FoxPro que você deseja consultar e clique em Okey.  
  
6.  Na caixa de diálogo Vincular tabelas, selecione as tabelas que você deseja consultar e atualizar e clique em Okey. As tabelas vinculadas do Visual FoxPro são exibidas na guia de tabelas do banco de dados Microsoft Access.  
  
 Agora você pode usar o Microsoft Access para consultar e atualizar dados em tabelas vinculadas do Visual FoxPro. As alterações feitas aos dados vinculados são enviadas de volta para a fonte de dados do Visual FoxPro.  
  
 Se você não quiser que as alterações feitas no Microsoft Access para afetar os dados na fonte de dados do Visual FoxPro, consulte [importando Visual FoxPro dados para o Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
