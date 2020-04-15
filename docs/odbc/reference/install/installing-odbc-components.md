---
title: Instalação de componentes ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd0a6aeba8073ce14b08b8635396b1f231895fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298976"
---
# <a name="installing-odbc-components"></a>Instalar componentes ODBC
> [!NOTE]  
>  Começando com o Windows XP e o Windows Server 2003, o ODBC está incluído no sistema operacional windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 Esta seção descreve como os componentes ODBC são instalados e removidos. Como os desenvolvedores de drivers sempre instalam um componente ODBC (seu driver), eles precisam ler esta seção. Os desenvolvedores de aplicativos só precisam ler esta seção se enviarem componentes ODBC com seus aplicativos. Os componentes do ODBC incluem o Driver Manager, drivers, tradutores, o instalador DLL, a biblioteca do cursor e quaisquer arquivos relacionados. Para efeitos desta seção, as aplicações ODBC não são consideradas componentes ODBC.  
  
> [!NOTE]  
>  Esta seção é específica para as plataformas Microsoft Windows. A forma como os componentes ODBC são instalados em outras plataformas é específica da plataforma.  
  
 Os componentes ODBC são instalados e removidos em uma base componente por componente, não uma base de arquivo por arquivo. Por exemplo, se um tradutor consiste no próprio tradutor e em vários arquivos de dados, esses arquivos são instalados e removidos como um grupo; eles não devem ser instalados e removidos em uma base arquivo por arquivo. A razão para isso é ter certeza de que existem apenas componentes completos no sistema.  
  
 Para fins de instalação e remoção de componentes, os seguintes são definidos como componentes ODBC:  
  
-   **Componentes principais.** O Driver Manager, a biblioteca do cursor, o instalador DLL e quaisquer outros arquivos relacionados compõem os componentes principais e devem ser instalados e removidos em grupo.  
  
-   **Drivers.** Cada driver é um componente separado.  
  
-   **Tradutores.** Cada tradutor é um componente separado.  
  
 Com o suporte do Unicode no ODBC 3.5 e posterior, alguma consideração deve ser dada ao uso de componentes OLE DB com ODBC. A versão 1.1 do Provedor OLE DB para ODBC foi escrita para especificações unicode específicas dentro do ODBC 3.0. Como essas especificações mudaram no ODBC 3.5, é necessário ter a versão 1.5 ou posterior do provedor ao usar o ODBC 3.5 e posterior. Esta seção contém os seguintes tópicos.  
  
-   [Componentes de instalação](../../../odbc/reference/install/installation-components.md)  
  
-   [Contagem de uso](../../../odbc/reference/install/usage-counting.md)
