---
title: Consultando e atualizando dados do Visual FoxPro do Microsoft Access | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11b49ed099ba29d0e7e013af99a8ad96ca6825c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292866"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Consultar e atualizar dados do Visual FoxPro do Microsoft Access
Você pode consultar e atualizar dados armazenados em um banco de dado do Visual FoxPro de um banco de dados do Microsoft Access usando a opção vincular tabela.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Para vincular um banco de dados do Visual FoxPro a um banco de dados do Microsoft Access  
  
1.  Abra um banco de dados do Microsoft Access.  
  
2.  Na guia tabelas, clique em novo.  
  
3.  Na caixa de diálogo nova tabela, selecione Vincular tabela e clique em OK.  
  
4.  Na caixa de diálogo Vincular, selecione banco de dados ODBC na lista arquivos do tipo.  
  
5.  Na caixa de diálogo fontes de dados do SQL, selecione a fonte de dados que se conecta aos dados do Visual FoxPro que você deseja consultar e clique em OK.  
  
6.  Na caixa de diálogo Vincular tabelas, selecione as tabelas que você deseja consultar e atualizar e clique em OK. As tabelas vinculadas do Visual FoxPro são exibidas na guia tabelas do banco de dados do Microsoft Access.  
  
 Agora você pode usar o Microsoft Access para consultar e atualizar dados nas tabelas vinculadas do Visual FoxPro. As alterações feitas nos dados vinculados são enviadas de volta para a fonte de dados do Visual FoxPro.  
  
 Se você não quiser que as alterações feitas no Microsoft Access afetem os dados na fonte de dados do Visual FoxPro, consulte [importando dados do Visual FoxPro para o Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
