---
title: Visão geral da arquitetura do driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd55290e09fbd35f5a1559ce4209693ef8eaaf73
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303457"
---
# <a name="driver-architecture-overview"></a>Visão geral de arquitetura do driver
O Microsoft Visual FoxPro ODBC Driver é um driver de 32 bits que permite que você abra e consulte um banco de dados Microsoft Visual FoxPro ou tabelas FoxPro através da interface Open Database Connectivity (ODBC). Você pode acessar os dados do FoxPro usando os seguintes tipos de aplicativos:  
  
-   Um aplicativo do Microsoft Office, como o Microsoft Excel ou o Microsoft Word, que usa o Microsoft Query para se comunicar com o ODBC.  
  
-   Um aplicativo escrito no Microsoft Visual C++ ou C que usa a API ODBC SDK.  
  
-   Um aplicativo escrito no Microsoft Visual Basic ou Microsoft Visual Basic para aplicativos.  
  
 Em cada caso, a solicitação de informações utiliza a API ODBC. O Gerenciador de Driver sustal oDBC trabalha com o Visual FoxPro ODBC Driver para abrir e recuperar dados de tabelas e bancos de dados FoxPro.  
  
 A arquitetura está representada no seguinte diagrama:  
  
 ![Mostra a arquitetura do Driver ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Terminologia do Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Instalação e configuração do driver Visual FoxPro ODBC](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Usando o driver ODBC do Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
