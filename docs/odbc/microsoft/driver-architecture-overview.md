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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 833c953df3502eb7e5d5676da8df057734174619
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071918"
---
# <a name="driver-architecture-overview"></a>Visão geral de arquitetura do driver
O driver ODBC do Microsoft Visual FoxPro é um driver de 32 bits que permite abrir e consultar um banco de dados do Microsoft Visual FoxPro ou tabelas do FoxPro por meio da interface ODBC (Open Database Connectivity). Você pode acessar dados do FoxPro usando os seguintes tipos de aplicativos:  
  
-   Um aplicativo Microsoft Office, como o Microsoft Excel ou o Microsoft Word, que usa o Microsoft Query para se comunicar com o ODBC.  
  
-   Um aplicativo escrito em Microsoft Visual C++ ou C que usa a API ODBC SDK.  
  
-   Um aplicativo escrito no Microsoft Visual Basic ou no Microsoft Visual Basic for Applications.  
  
 Em cada caso, a solicitação de informações usa a API ODBC. O Gerenciador de driver ODBC funciona com o driver ODBC do Visual FoxPro para abrir e recuperar dados de tabelas e bancos de dado do FoxPro.  
  
 A arquitetura é representada no diagrama a seguir:  
  
 ![Mostra a arquitetura do driver ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Terminologia do Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Instalando e Configurando o driver ODBC do Visual FoxPro](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Usar o driver ODBC do Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
