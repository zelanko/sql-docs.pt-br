---
description: 'Solução alternativa para habilitar a cópia da janela Localizar e Substituir '
title: Habilitar cópia da janela Localizar e Substituir
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: seo-lt-2019
ms.date: 11/03/2020
ms.openlocfilehash: ea5ae3f9fa941e723d3bdf10de0ec900310cc28d
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328766"
---
# <a name="workaround-to-enable-copying-from-find-and-replace-window"></a>Solução alternativa para habilitar a cópia da janela Localizar e Substituir

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

É necessária uma solução alternativa para habilitar a cópia da janela Localizar e Substituir.  Se você observar que não é possível copiar da janela Localizar e Substituir no SQL Server Management Studio, siga a [solução alternativa](#workaround) abaixo.

## <a name="error-message"></a>Mensagem de erro

Ao tentar copiar texto da janela Localizar e Substituir no SQL Server Management Studio, você receberá uma mensagem de erro.

> Documentos não salvos não podem ser recortados nem copiados para a área de transferência do projeto de arquivos diversos. Você precisa salvar os documentos não salvos antes de recortá-los ou copiá-los.

![Caixa de diálogo de erro para: Documentos não salvos não podem ser recortados nem copiados para a área de transferência do projeto de arquivos diversos. Você precisa salvar os documentos não salvos antes de recortá-los ou copiá-los](../media/troubleshoot/unable-copy-find-replace-window.png)

## <a name="workaround"></a>Solução alternativa

Para habilitar a cópia de texto da janela Localizar e Substituir, siga estas etapas:

1. No menu **Ferramentas** , abra **Opções**.

2. Em **Ambiente**>**Documentos** , desmarque o item "Mostrar arquivos diversos no Gerenciador de Soluções"

3. Feche e reabra o SQL Server Management Studio

![Janela Opções com "Mostrar arquivos diversos no Gerenciador de Soluções" desmarcado](../media/troubleshoot/fix-copy-find-replace-window.png)

