---
title: Consultar e atualizar dados do Visual FoxPro do Microsoft Access | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ef01b8c5a21d65fb99f5f190fd159d90f3ac78b2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
