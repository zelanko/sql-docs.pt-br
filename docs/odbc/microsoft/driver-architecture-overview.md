---
title: "Visão geral da arquitetura driver | Microsoft Docs"
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
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6755e4b04c0d56995fb83f64891e5fcd7d765a49
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="driver-architecture-overview"></a>Visão geral de arquitetura de driver
O Driver ODBC do Microsoft Visual FoxPro é um driver de 32 bits que permite que você abra e consultar um banco de dados do Microsoft Visual FoxPro ou tabelas FoxPro através da interface do banco de dados ODBC (conectividade aberta). Você pode acessar dados FoxPro usando os seguintes tipos de aplicativos:  
  
-   Um aplicativo do Microsoft Office, como o Microsoft Excel ou Microsoft Word, que usa o Microsoft Query para se comunicar com o ODBC.  
  
-   Um aplicativo escrito em Microsoft Visual C++ ou C que usa a API do SDK do ODBC.  
  
-   Um aplicativo escrito em Microsoft Visual Basic ou Microsoft Visual Basic for Applications.  
  
 Em cada caso, a solicitação para obter informações usa a API ODBC. O Gerenciador de Driver ODBC funciona com o Driver de ODBC do Visual FoxPro para abrir e recuperar dados de bancos de dados e tabelas FoxPro.  
  
 A arquitetura é representada no diagrama a seguir:  
  
 ![Mostra a arquitetura do Driver ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Terminologia do Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Instalando e configurando o Driver ODBC do Visual FoxPro](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Usando o driver ODBC do Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
