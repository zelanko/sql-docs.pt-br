---
title: Consultando e atualizando dados visuais foxpro do Microsoft Access | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292866"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Consultar e atualizar dados do Visual FoxPro do Microsoft Access
Você pode consultar e atualizar dados armazenados em um banco de dados Visual FoxPro a partir de um banco de dados do Microsoft Access usando a opção Tabela de Link.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Para vincular um banco de dados Visual FoxPro a um banco de dados do Microsoft Access  
  
1.  Abra um banco de dados do Microsoft Access.  
  
2.  Na guia Tabelas, clique em Novo.  
  
3.  Na caixa de diálogo Nova tabela, selecione Tabela de link e clique em OK.  
  
4.  Na caixa 'Diálogo de link', selecione ODBC Database na lista Arquivos da lista de tipos.  
  
5.  Na caixa de diálogo SQL Data Sources, selecione a fonte de dados que se conecta aos dados do Visual FoxPro que deseja consultar e clique em OK.  
  
6.  Na caixa de diálogo Tabelas de link, selecione as tabelas que deseja consultar e atualize e clique em OK. As tabelas Visual FoxPro vinculadas são exibidas na guia Tabelas do banco de dados Microsoft Access.  
  
 Agora você pode usar o Microsoft Access para consultar e atualizar dados nas tabelas do Visual FoxPro vinculadas. As alterações que você faz aos dados vinculados são enviadas de volta para a fonte de dados Visual FoxPro.  
  
 Se você não quiser que as alterações que você faz no Microsoft Access afetem os dados na fonte de dados do Visual FoxPro, consulte [Importar Dados Visual FoxPro para](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md)o Microsoft Access .
