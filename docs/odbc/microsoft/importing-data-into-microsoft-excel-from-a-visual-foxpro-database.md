---
title: Importando dados para o Microsoft Excel a partir de um banco de dados Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bfd86233e5a0a406febcb30bf7a4fae595e53d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287666"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importar dados para o Microsoft Excel de um banco de dados do Visual FoxPro
Você pode importar dados do Visual FoxPro para a planilha do Microsoft Excel se você tiver definido uma fonte de dados para ele. Para obter informações sobre como criar uma fonte de dados Visual FoxPro, consulte [Acessando uma fonte de dados Visual FoxPro do Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Para importar dados do Visual FoxPro em uma planilha do Microsoft Excel  
  
1.  Abra uma planilha do Microsoft Excel.  
  
2.  No menu Dados, escolha Obter dados externos. O Microsoft Query é aberto.  
  
3.  Na caixa de diálogo Selecionar fonte de dados, selecione uma fonte de dados Visual FoxPro e clique em Usar.  
  
4.  Se o banco de dados acessado pela sua fonte de dados incluir tabelas, selecione uma tabela na caixa de diálogo Adicionar tabelas. O Microsoft Query exibe a tabela adicionada na metade superior do designer de consulta.  
  
    > [!NOTE]  
    >  A lista Proprietário não está disponível nesta caixa de diálogo porque o driver não suporta proprietários. A lista de banco de dados não está disponível porque o driver não suporta vários bancos de dados em uma fonte de dados.  
  
5.  Selecione campos para sua consulta arrastando-os da tabela para a metade inferior do designer.  
  
6.  Feche a Consulta Microsoft. Os dados selecionados são importados para sua planilha do Microsoft Excel.
