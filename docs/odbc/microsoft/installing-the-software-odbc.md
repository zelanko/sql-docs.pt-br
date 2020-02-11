---
title: Instalando o software (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], installing
- installing ODBC driver for Oracle [ODBC]
ms.assetid: dfac8ade-eebe-4ebe-a199-feb740ed5bae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3be4f2ce9a3388d53a4d8474e5c1ca172842b5c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085515"
---
# <a name="installing-the-software-odbc"></a>Instalar o software (ODBC)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O ODBC driver for Oracle é um dos componentes de acesso a dados. Ele acompanha outros componentes ODBC, como o administrador de fonte de dados ODBC, e já deve estar instalado. O driver também pode ser encontrado em "drivers e outros downloads" no site online do Microsoft Product Support Services em [www.Microsoft.com](https://www.microsoft.com).  
  
 O software de rede deve ser instalado de acordo com sua própria documentação. O ODBC driver for Oracle não requer nenhuma consideração especial de instalação, desde que o software de rede tenha suporte.  
  
 O software Oracle deve ser instalado de acordo com sua própria documentação. O ODBC driver for Oracle geralmente não requer nenhuma consideração especial de instalação, desde que o driver ofereça suporte à versão. No entanto, para manter os produtos compatíveis, instale o driver ODBC para Oracle por último para garantir que você tenha a versão mais recente do driver. A Oracle mantém um site de FTP público onde ele posta, entre outras coisas, patches para os produtos de servidor Oracle e o componente cliente que acompanha os produtos de servidor. Esses patches são necessários para o funcionamento adequado de vários produtos e tecnologias da Microsoft. Para obter mais informações sobre esse site, consulte [patches de software Oracle](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!CAUTION]  
>  A instalação do software Oracle sobre o DAC do MDAC/Windows pode substituir as versões atuais do MDAC. Se surgirem problemas usando componentes ODBC, reinstale o MDAC.
