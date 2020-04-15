---
title: Importação de dados visuais foxpro para o Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90ac16bbdbaf7f4dd29e14e66cf5b9dc666057f4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302438"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importar dados do Visual FoxPro para Microsoft Access
Você pode importar dados armazenados em um banco de dados Visual FoxPro em um banco de dados do Microsoft Access usando a opção Importar.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Para importar dados do Visual FoxPro em um banco de dados do Microsoft Access  
  
1.  Abra um banco de dados do Microsoft Access.  
  
2.  No menu Arquivo, escolha Obter dados externos e importar.  
  
3.  Na caixa de diálogo Importar, selecione Bancos de Dados ODBC na lista Arquivos da lista de tipos.  
  
4.  Na caixa de diálogo SQL Data Sources, selecione a fonte de dados Visual FoxPro que se conecta aos dados do FoxPro que você deseja consultar e clique em OK.  
  
5.  Na caixa de diálogo Importar objetos, selecione uma ou mais tabelas que deseja importar e clique em OK. Os nomes das tabelas Do Visual FoxPro que você importou são exibidos na guia Tabelas do banco de dados Microsoft Access.  
  
 Agora você pode usar o Microsoft Access para manipular os dados nas tabelas do Visual FoxPro importadas. Os dados que você importa são um instantâneo dos dados armazenados no Visual FoxPro; as alterações que você faz para dados importados não são enviadas de volta para a fonte de dados Visual FoxPro.  
  
 Se você quiser alterações que você faz no Microsoft Access para alterar os dados na fonte de dados do Visual FoxPro, consulte [Consultando e Atualizando os Dados Visuais FoxPro do Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).
