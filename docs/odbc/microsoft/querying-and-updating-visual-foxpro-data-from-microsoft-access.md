---
title: Consultar e atualizar dados do Visual FoxPro do Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- querying Visual FoxPro data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], querying and updating
- updating Visual FoxPro data [ODBC]
ms.assetid: 2d314e78-9edf-44b2-bd8b-96784236bcbe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6eefdf130a261945a17c9ec557235b65ab7133fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Consultar e atualizar dados do Visual FoxPro do Microsoft Access
Você pode consultar e atualizar dados armazenados em um banco de dados do Visual FoxPro de um banco de dados do Microsoft Access, usando a opção de tabela do Link.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Para vincular um banco de dados do Visual FoxPro para um banco de dados do Microsoft Access  
  
1.  Abra um banco de dados do Microsoft Access.  
  
2.  Na guia tabelas, clique em novo.  
  
3.  Na caixa de diálogo nova tabela, selecione o Link de tabela e clique em Okey.  
  
4.  Na caixa de diálogo de Link, selecione o banco de dados ODBC nos arquivos da lista de tipo.  
  
5.  Na caixa de diálogo fontes de dados do SQL, selecione a fonte de dados que se conecta aos dados do Visual FoxPro que você deseja consultar e clique em Okey.  
  
6.  Na caixa de diálogo Vincular tabelas, selecione as tabelas que você deseja consultar, atualizar e clique em Okey. As tabelas vinculadas do Visual FoxPro são exibidas na guia tabelas do banco de dados Microsoft Access.  
  
 Agora você pode usar o Microsoft Access para consultar e atualizar dados em tabelas do Visual FoxPro. As alterações feitas aos dados vinculados são enviadas de volta para a fonte de dados do Visual FoxPro.  
  
 Se você não quiser que as alterações feitas no Microsoft Access para afetar os dados na fonte de dados do Visual FoxPro, consulte [importando Visual FoxPro dados para o Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
