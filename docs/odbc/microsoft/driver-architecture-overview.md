---
title: Visão geral da arquitetura de driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fdb1789c6640c072ec013c341bd4889b28bb469
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771864"
---
# <a name="driver-architecture-overview"></a>Visão geral de arquitetura do driver
O Driver ODBC do Microsoft Visual FoxPro é um driver de 32 bits que permite que você abra e consultar um banco de dados do Microsoft Visual FoxPro ou tabelas FoxPro por meio da interface do banco de dados ODBC (conectividade aberta). Você pode acessar dados FoxPro usando os seguintes tipos de aplicativos:  
  
-   Um aplicativo do Microsoft Office, como o Microsoft Excel ou Microsoft Word, que usa o Microsoft Query para se comunicar com o ODBC.  
  
-   Um aplicativo escrito em C que usa a API de SDK ODBC ou o Microsoft Visual C++.  
  
-   Um aplicativo escrito em Microsoft Visual Basic ou Microsoft Visual Basic for Applications.  
  
 Em cada caso, a solicitação para obter informações usa a API do ODBC. O Gerenciador de Driver ODBC funciona com o Driver de ODBC do Visual FoxPro para abrir e recuperar dados de bancos de dados e tabelas do FoxPro.  
  
 A arquitetura é representada no diagrama a seguir:  
  
 ![Mostra a arquitetura do Driver ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Terminologia do Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Instalando e configurando o Driver ODBC do Visual FoxPro](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Usando o driver ODBC do Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
