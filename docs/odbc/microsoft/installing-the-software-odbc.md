---
title: Instalação do Software (ODBC) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9bddfd9947017cc94214e57948e495b06cccc1cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299976"
---
# <a name="installing-the-software-odbc"></a>Instalar o software (ODBC)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Driver ODBC para Oracle é um dos componentes de acesso a dados. Ele acompanha outros componentes da ODBC, como o Administrador de Fonte de Dados do ODBC, e já deve ser instalado. O driver também pode ser encontrado em "Drivers and Other Downloads" no site online da Microsoft Product Support Services online em [www.microsoft.com](https://www.microsoft.com).  
  
 O software de rede deve ser instalado de acordo com sua própria documentação. O Driver ODBC para Oracle não requer considerações especiais de instalação, desde que o software de rede seja suportado.  
  
 O software Oracle deve ser instalado de acordo com sua própria documentação. O Driver ODBC para Oracle geralmente não requer considerações especiais de instalação, desde que o driver suporte a versão. No entanto, para manter os produtos compatíveis, instale o Driver ODBC para Oracle por último para garantir que você tenha a versão mais recente do driver. A Oracle mantém um site público de FTP onde posta, entre outras coisas, patches para os produtos do servidor Oracle e o componente cliente que é fornecido com os produtos do servidor. Esses patches são necessários para o bom funcionamento de vários produtos e tecnologias da Microsoft. Para obter mais informações sobre este site, consulte [Oracle Software Patches](../../odbc/microsoft/oracle-software-patches.md).  
  
> [!CAUTION]  
>  A instalação do software Oracle sobre o MDAC/Windows DAC pode substituir as versões atuais do MDAC. Se surgirem problemas usando componentes ODBC, reinstale o MDAC.
